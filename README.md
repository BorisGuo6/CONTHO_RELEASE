<div align="center">

# <b>CONTHO</b>: Joint Reconstruction of 3D Human and Object via Contact-Based Refinement Transformer

<b>[Hyeongjin Nam*](https://hygenie1228.simple.ink/)<sup>1</sup></b>, <b>[Daniel Sungho Jung*](https://dqj5182.github.io/)<sup>1</sup></b>, <b>[Gyeongsik Moon](https://mks0601.github.io/)<sup>2</sup></b>, <b>[Kyoung Mu Lee](https://cv.snu.ac.kr/index.php/~kmlee/)<sup>1</sup></b>

<b><sup>1</sup>Seoul National University</b>, <b><sup>2</sup>Codec Avatars Lab, Meta</b>

<h2>CVPR 2024</h2>

<img src="./asset/teaser.gif" alt="Logo" width="100%">

</div>

_**CONTHO** jointly reconstructs **3D human and object** by exploiting human-object contact as a key signal in accurate reconstruction. To this end, we integrates **"3D human-object reconstruction"** and **"Human-object contact estimation"**, the two different tasks that have been separately studied in two tracks, with one unified framework._
<br/>


## Installation
* We recommend you to use an [Anaconda](https://www.anaconda.com/) virtual environment. Install PyTorch >=1.10.1 and Python >= 3.7.0. Our latest CONTHO model is tested on Python 3.9.13, PyTorch 1.10.1, CUDA 10.2.
* Setup the environment
``` 
    # Initialize conda environment
    conda create -n contho python=3.9
    conda activate contho 

    # Install PyTorch
    conda install pytorch==1.10.1 torchvision==0.11.2 torchaudio==0.10.1 cudatoolkit=10.2 -c pytorch

    # Install all remaining packages
    pip install -r requirements.txt
```


## Quick demo
* Prepare the `base_data` from [here](https://drive.google.com/drive/folders/1f0RYWHrCfaegEG24lcuP7-5PfsHGrchj?usp=sharing) and place it as `${ROOT}/data/base_data`.
* Download the pre-trained checkpoint from [here](https://drive.google.com/drive/folders/1Ow6N0L8b2DOTqXImuWaT2UELNpgWRi5v?usp=sharing).
* Lastly, please run
```
python main/demo.py --gpu 0 --checkpoint {CKPT_PATH}
```

## Data
You need to follow directory structure of the `data` as below.
```
${ROOT} 
|-- data  
|   |-- base_data
|   |   |-- annotations
|   |   |-- backbone_models
|   |   |-- human_models
|   |   |-- object_models
|   |-- BEHAVE
|   |   |-- dataset.py
|   |   |-- sequences
|   |   |   |-- Date01_Sub01_backpack_back
|   |   |   |-- Date01_Sub01_backpack_hand
|   |   |   |-- ...
|   |   |   |-- Date07_Sub08_yogamat
|   |-- InterCap
|   |   |-- dataset.py
|   |   |-- sequences
|   |   |   |-- 01
|   |   |   |-- 02
|   |   |   |-- ...
|   |   |   |-- 10
```
* Download Data01~Data07 sequences from [BEHAVE](https://virtualhumans.mpi-inf.mpg.de/behave/) dataset to `${ROOT}/data/BEHAVE/sequences`. <br/>
(Option 1) Directly download [BEHAVE](https://virtualhumans.mpi-inf.mpg.de/behave/) dataset from their [download page](https://virtualhumans.mpi-inf.mpg.de/behave/license.html). <br/>
(Option 2) Run the script below.
```
scripts/download_behave.sh
```
* Download RGBD_Images.zip and Res.zip from [InterCap](https://intercap.is.tue.mpg.de/) dataset to `${ROOT}/data/InterCap/sequences`. <br/>
(Option 1) Directly download [InterCap](https://intercap.is.tue.mpg.de/) dataset from their [download page](https://intercap.is.tue.mpg.de/download.php). <br/>
(Option 2) Run the script below.
```
scripts/download_intercap.sh
```
* Download [base_data](https://drive.google.com/drive/folders/1f0RYWHrCfaegEG24lcuP7-5PfsHGrchj?usp=sharing).
* (Optional) Download the released checkpoints for [BEHAVE](https://drive.google.com/file/d/1oD7r0ekvpYiWp_ysVkVFXBYJL9X4hZOS/view?usp=sharing) or [InterCap](https://drive.google.com/file/d/14Zd5iVhJuGCI2pvW5p_peRnabBGOEdY3/view?usp=sharing) dataset.


## Running CONTHO

### Train 
To train CONTHO on [BEHAVE](https://virtualhumans.mpi-inf.mpg.de/behave/) or [InterCap](https://intercap.is.tue.mpg.de/) dataset, please run
```
python main/train.py --gpu 0 --dataset {DATASET}
``` 

### Test
To evaluate CONTHO on [BEHAVE](https://virtualhumans.mpi-inf.mpg.de/behave/) or [InterCap](https://intercap.is.tue.mpg.de/) dataset, please run
```
python main/test.py --gpu 0 --dataset {DATASET} --checkpoint {CKPT_PATH}
```

### Results
Here, we report the performance of CONTHO. <br/>
CONTHO is a **fast** and **accurate** 3D human and object reconstruction framework!
<p align="center">  
<img src="./asset/results/contho_quant.png" style="width:100%">  
</p>
<p align="center">  
<img src="./asset/results/contho_speed.png" style="width:50%">  
</p>


## Technical Q&A
* RuntimeError: Subtraction, the `-` operator, with a bool tensor is not supported. If you are trying to invert a mask, use the `~` or `logical_not()` operator instead: Please check [reference](https://stackoverflow.com/questions/65637222/runtimeerror-subtraction-the-operator-with-a-bool-tensor-is-not-supported).
* bash: scripts/download_behave.sh: Permission denied: Please check [reference](https://askubuntu.com/questions/409025/permission-denied-when-running-sh-scripts).


## Acknowledgement
We thank:
* [Hand4Whole](https://github.com/mks0601/Hand4Whole_RELEASE) for 3D human mesh reconsturction.
* [CHORE](https://github.com/xiexh20/CHORE) for training and testing on BEHAVE.
* [InterCap](https://github.com/YinghaoHuang91/InterCap/tree/master) for download script of the dataset.
* [DECO](https://github.com/sha2nkt/deco) for in-the-wild experiment setup.


## Reference
```  
@inproceedings{nam2024contho,    
title = {Joint Reconstruction of 3D Human and Object via Contact-Based Refinement Transformer},
author = {Nam, Hyeongjin and Jung, Daniel Sungho and Moon, Gyeongsik and Lee, Kyoung Mu},
booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},  
year = {2024}  
}  
```