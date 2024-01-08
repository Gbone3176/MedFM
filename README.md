# 2023MedFM
2023MedFM
## week1
## 环境安装
首先在conda中新建一个环境
```
conda create --name openmmlab python=3.9 -y
conda activate openmmlab
```
接着安装pytorch，注意尽量安装GPU版本，根据自己的电脑显卡型号选择相应的CUDA安装，再根据CUDA版本安装pytorch，若安装的是CPU版本之后运行代码使用mmcv库会报错显示没有用上CUDA，可能因为mmcv只能安装匹配gpu版本，可以查下有无匹配cpu的版本

将所给的MedFM git到自己电脑中，git安装指南：
<https://blog.csdn.net/Andone_hsx/article/details/87937329>
，遇到问题见评论区解决方案

确保pytorch安装成功后进行下一步安装：
```
pip install mmcls==0.25.0 openmim scipy scikit-learn ftfy regex tqdm
mim install mmcv-full==1.6.0
```
其中第二行代码可能会报错，因此去mmcv-full官网下载whl文件，官网网址:<https://mmcv.readthedocs.io/zh-cn/latest/get_started/installation.html#pip>，根据pytorch和cuda版本下载自己电脑适应的mmcv版本，接着在conda中pip install一下 安装完了mmcv-full之后跑代码依然会报错显示没有mmcv-full库，未解决

剩下的跟着比赛提供的readme文档走

其中config文件的阅读见<https://mmpretrain.readthedocs.io/zh-cn/latest/get_started.html>读懂配置即明白具体原理

## week 2
## 试运行第一个代码
```
export PYTHONPATH=$PWD:$PYTHONPATH
```
上述官网中代码用来将medfmc包保存到路径中从而可以使用，将$PWD改为medfmc上一层路径即可，比如改为/storage/MedFM

运行train.py

```
python MedFM-master/tools/train.py MedFM-master/configs/vit-b_vpt/1-shot_chest.py
```
或者直接将MedFM-master作为当前的PYTHONPATH，然后运行
```
python tools/train.py configs/vit-b_vpt/1-shot_chest.py
```
出现如下报错： TypeError: FormatCode() got an unexpected keyword argument 'verify'

说明yapf包版本过高，见<https://blog.csdn.net/ZZZZ_Y_/article/details/133902230>

后面的报错都是见```MedFM/configs/vit-b16_vpt/in21k-vitb16_vpt1_bs4_lr6e-4_1-shot_chest.py```所调用文件里面的代码，不难懂，改一下文件名就行

## week3
Master里的文件具有下载预训练模型的网络链接，因此运行它的config文件
使用MedFM-Master文件夹里的配置文件跑通一个程序，再使用验证命令（在下面）查看跑出来的模型的效果
再在[MMPretrain](https://mmpretrain.readthedocs.io/zh-cn/latest/user_guides/config.html "MMPretrain")里学习如何修改参数

## date:240108
修改了以下两个问题，以不成熟的方式跑通一次：
1.根据CUDA版本（11.1）（用nvcc -version）和torch版本（1.10）重新安装了mmcv，版本是2.0.0，不需要full
```
pip install mmcv==2.0.0 -f https://download.openmmlab.com/mmcv/dist/cu111/torch1.10/index.html
```
2.获取root权限运行上述代码，解决了对.pth文件的permision denied问题，获取root权限的方式：
```
sudo -i
```
