
# Hand Emotion Recognition 
presented by JoChien Wang,MIS Lab
## Project Description
Hand Emotion Recognition aims to identify the emotional expressions of pianists through hand movements captured in images. 


This project seeks to deeply analyze musical pieces, exploring how the same composition can result in different interpretations by different performers using image recognition technology to capture and analyze emotional changes in hand dynamics.

Official implementation of [ACTION-Net: Multipath Excitation for Action Recognition](https://arxiv.org/abs/2103.07372) (CVPR'21)

By [Zhengwei Wang](https://villawang.github.io/), [Qi She](https://qi-she.net/) and [Aljosa Smolic](https://scholar.google.ch/citations?user=HZRejX4AAAAJ&hl=de)

<p align="center"><img src="fig/backbone2.png" width="800" /></p>

<p align="center"><img src="fig/heatmap_10_compressed.png" width="800" />

## Acknowledgment
Our codes are built based on previous repos [TSN](https://github.com/yjxiong/temporal-segment-networks), [TSM](https://github.com/mit-han-lab/temporal-shift-module) and [TEA](https://github.com/Phoenix1327/tea-action-recognition)

## Installation 
Use [Anaconda](https://www.anaconda.com/) is recommended !

Open Anaconda Prompt and enter the followings prompts:
```bash
# Create a environment for this project (Open Anaconda Prompt)
conda create -n ACN python=3.8
```
```bash
# To get into the Virtual Environment
conda activate ACN
```
install these dependencies with the following command : 
```bash
# pytorch
conda install pytorch==2.1.0 torchvision==0.16.0 torchaudio==2.1.0 pytorch-cuda=11.8 -c pytorch -c nvidia

# other components
pip install tqdm numpy seaborn pandas pillow
pip install scikit-image
pip install -U scikit-learn
pip install tensorboardX

```
### Mediapipe Module
For details, please view page [/mediapipe/README.md](/mediapipe/README.md)

## Annotation files
Annotation files are at this [link](https://www.dropbox.com/sh/hry7o1iri8tebri/AADmotYF-PFY14ueVIdtc1-pa?dl=0). Please follow the annotation files to construct the frame path.

( You can use Annotation file as reference to establish your data path )

### Pretrained models
[EgoGesture using 8f](https://www.dropbox.com/sh/v9373sopxmf3vwh/AACDx4E3exxR_gbHgFK7rsGXa?dl=0): RGB + Depth 

[Jester using 8f](https://www.dropbox.com/sh/77d5qn31wxwpqw8/AAB-1JZVAb1MuQfnOaKtz4Lya?dl=0) : RGB


## Usage
You can Change the parameter EgoGesture to Jester to change the type of Training
### Train
```bash
# for Training (ref in train_ego_8f.sh)
python 6train.py --is_train --is_shift --dataset EgoGesture --clip_len 8 --shift_div 8 --wd 5e-4 --dropout 0.5  --batch_size 4 --lr_steps 5 10 15 --lr 1e-2 --base_model resnet50 --epochs 20 --num_workers 5 
```
Optional add parameter (to load pretrain)
```bash
--pretrain 'imagenet' --pretrained [pretrain_weight (you can download it on above link)] 
```
for finetuning (to freeze fc layer)
```bash
--freeze_pretrained
```

### Test
```bash
# for Training (ref in train_ego_8f.sh)
python 6test.py --is_shift --dataset EgoGesture --clip_len 8 --shift_div 8 --batch_size 1 --test_crops 1 --scale_size 256 --crop_size 256 --clip_num 10 --num_workers 5
```
## Custom Data Preparation
For Custom Data, please view page [/data/README.md](/data/README.md)

## Citation

[V-Sense/ACTION-Net](https://github.com/V-Sense/ACTION-Net) (Github)
```
@InProceedings{Wang_2021_CVPR,
author = {Wang, Zhengwei and She, Qi and Smolic, Aljosa},
title = {ACTION-Net: Multipath Excitation for Action Recognition},
booktitle = {IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
month = {June},
year = {2021}
}
```
## License
This project is licensed under the [MIT License](LICENSE).

#
