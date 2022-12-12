# CSWin Transformer with joint attention for image inpainting (ICME 2023)

標題+arxiv鏈結

The overview of our proposed model. The whole model structure is the main model of our proposed and show the detail of our joint attention between Global layer and Local layer. The input feature only Im and M, the Iedge won’t be trained in the model and be generated by Canny before training. Moreover, the right side show the CSWin Transformer Block. At last, the Residual Dense Block in local layer show at the top right corner of the whole model.
<img src="https://i.imgur.com/PWw3CpW.png" alt="https://i.imgur.com/PWw3CpW.png" title="https://i.imgur.com/PWw3CpW.png" width="1312" height="350">

# Environment
- Python 3.7.0
- pytorch
- opencv
- PIL  
- colorama

or see the requirements.txt

# How to try

## Download dataset (places2、CelebA、ImageNet)
[Places2](http://places2.csail.mit.edu/)  
[CelebA](https://mmlab.ie.cuhk.edu.hk/projects/CelebA.html)  
[ImageNet](https://www.image-net.org/download.php)

## Set dataset path

Edit txt/xxx.txt (set path in config)
```python

data_path = './txt/train_path.txt'
mask_path = './txt/train_mask_path.txt'
val_path = './txt/val_path.txt'
val_mask_path = './val_mask_file/' # path
test_path: './txt/test_path.txt'
test_mask_1_60_path: './test_mask_1+10_file/' # path

```

txt example
```python

E:/Places2/data_256/00000001.jpg
E:/Places2/data_256/00000002.jpg
E:/Places2/data_256/00000003.jpg
E:/Places2/data_256/00000004.jpg
E:/Places2/data_256/00000005.jpg
 ⋮

```

## Preprocessing  
In this implementation, masks are automatically generated by ourself. stroke masks mixed randomly to generate proportion from 1% to 60%.

strokes (from left to right 20%-30% 30%-40% 40%-50% 50%-60%)
<img src="https://imgur.com/m3CStkN.png" alt="https://imgur.com/m3CStkN.png" title="https://imgur.com/m3CStkN.png" width="1000" height="200">

## Run training
```python

python train.py 

```
1. set the config path ('./config/model_config.yml')
2. Set path and parameter details in model_config.yml

## Result

- Places2

<img src="https://imgur.com/P2XHsSA.jpg" width="700" height="600">

- CelebA 

<img src="https://imgur.com/ARzFFZv.jpg" width="700" height="600">

- COMPLEXITY COMPARISON

<img src="https://imgur.com/hjZB4k7.jpg" width="861" height="131">

All training and testing base on same 2080 Ti.

## Visual comparisons
- Places2

<img src="https://imgur.com/MXPw6V5.jpg" width="600" style="zoom:100%;">

- CelebA

<img src="https://imgur.com/kpLYqj3.jpg" width="600" style="zoom:100%;">

## Difference from original paper
Firstly, check [implementation FAQ](http://masc.cs.gmu.edu/wiki/partialconv)
1. C(0)=0 in first implementation (already fix in latest version)
2. Masks are generated using random walk by generate_window.py
3. To use chainer VGG pre-traied model, I re-scaled input of the model. See updater.vgg_extract. It includes cropping, so styleloss in outside of crop box is ignored.)
4. Padding is to make scale of height and width input:output=2:1 in encoder stage.  

other differences:  
- image_size=256x256 (original: 512x512)


## Acknowledgement
This repository utilizes the codes of following impressive repositories   
- [chainer-cyclegan](https://github.com/Aixile/chainer-cyclegan)  
- [partialconv](https://github.com/NVIDIA/partialconv)
- [chainer-partial_convolution_image_inpainting](https://github.com/SeitaroShinagawa/chainer-partial_convolution_image_inpainting)

---
## Contact
If you have any question, feel free to contact wiwi61666166@gmail.com
