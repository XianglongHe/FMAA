# Feature-Momentum Adversarial Attack(FMAA)
Official Tensorflow implementation for "Improving Transferable Adversarial Attack via Feature-Momentum".

**[Improving Transferable Adversarial Attack via Feature-Momentum](https://www.sciencedirect.com/science/article/abs/pii/S0167404823000457)**

## Requirements

- Python 3.6.8
- Keras 2.2.4
- Tensorflow 1.14.0
- Numpy 1.16.2
- Pillow 6.0.0
- Scipy 1.2.1

## Experiments

#### Introduction

- `attack.py` : the implementation for FMAA attack along with baseline attacks.

- `verify.py` : the code for evaluating generated adversarial examples on different models.

  You should download the pretrained models from ( https://github.com/tensorflow/models/tree/master/research/slim, https://github.com/tensorflow/models/tree/archive/research/adv_imagenet_models) before running the code. Then place these model checkpoint files in `./models_tf`.

#### Example Usage

##### Generate adversarial examples:

+ FMAA

```
python attack.py --attack_method FMAA --model_name vgg_16 --layer_name vgg_16/conv3/conv3_3/Relu --ens 30 --ens2 30 --batch_size 20 --probb 0.6 --probb2 0.9 --beta 1.1 --output_dir ./adv/FMAA_vgg16/
```

+ FMAA+VIM

```
python attack.py --attack_method FMAAVIM --model_name inception_resnet_v2 --layer_name InceptionResnetV2/InceptionResnetV2/Conv2d_4a_3x3/Relu --ens 30 --ens2 30 --batch_size 20  --image_size 299 --image_resize 330 --probb 0.6 --probb2 0.9 --beta 1.1 --vn 20 --vb 1.5 --output_dir ./adv/FMAAVIM_incresv2/
```

- FIA

```
python attack.py --attack_method FMAA --model_name vgg_16 --layer_name vgg_16/conv3/conv3_3/Relu --ens 30 --ens2 -1 --batch_size 20 --probb 0.6 --probb2 0.9 --beta 1.1 --output_dir ./adv/FIA_vgg16/
```

- PIM:

```
python attack.py --model_name vgg_16 --attack_method PIM --amplification_factor 10 --gamma 1 --Pkern_size 3 --output_dir ./adv/PIM/
```

- FIA+PIDIM

```
python attack.py --model_name vgg_16 --attack_method FIAPIM --layer_name vgg_16/conv3/conv3_3/Relu --ens 30 --probb 0.7 --amplification_factor 2.5 --gamma 0.5 --Pkern_size 3 --image_size 224 --image_resize 250 --prob 0.7 --output_dir ./adv/FIAPIDIM/
```

Different attack methods have different parameter setting, and the detailed setting can be found in our paper. 

##### Evaluation

```
python verify.py --ori_path ./dataset/images/ --adv_path ./adv/FMAA_vgg16/ --output_file ./log.csv
```

## Acknowledgment

Code heavily refers to: [Feature Importance-aware Attack](https://github.com/hcguoO0/FIA)

## Citation

If you find this work is useful in your research, please consider citing:

```
@article{he2023improving,
  title={Improving transferable adversarial attack via feature-momentum},
  author={He, Xianglong and Li, Yuezun and Qu, Haipeng and Dong, Junyu},
  journal={Computers \& Security},
  volume={128},
  pages={103135},
  year={2023},
  publisher={Elsevier}
}
```