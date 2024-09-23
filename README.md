# TrackingMamba

**TrackingMamba: Visual State Space Model for Object Tracking**

Qingwang Wang, Liyao Zhou, Pengcheng Jin, Xin Qu, Hangwei Zhong, Haochen Song, Tao Shen

![](https://github.com/KustTeamWQW/TrackingMamba/blob/main/img/trackingmamba_framework.JPG)

## News

[August 7, 2024]

Source code and weights are all released.

## Highlights

#### **Visual State Space Model for Object Tracking**

This paper proposes a new tracking framework based on the state space model, named TrackingMamba, which adopts a single-stream tracking architecture with Vision Mamba as the backbone. TrackingMamba not only rivals transformer-based trackers in global feature extraction and long-range dependency modeling but also maintains computational cost in a linear growth manner.  Compared to other advanced trackers, TrackingMamba achieves higher accuracy with a simpler model framework, fewer parameters, and lower FLOPs. Especially when compared with the baseline model OSTrack-256, TrackingMamba shows an improvement of 2.59\% in AUC and 4.42\% in Precision on the UAV123 benchmark.This paper also evaluates the performance and limitations of TrackingMamba and several current advanced trackers in the crucial and complex scenario of forests, and further contemplates and summarizes potential future research directions in the field of UAV object tracking in forest environments.

|              | UAV123 | DTB70 | [OTMJ](https://github.com/KustTeamWQW/OTMJ_Dataset) |
| ------------ | ------ | ----- | --------------------------------------------------- |
| AUC(%)       | 70.89  | 66.21 | 65.54                                               |
| Precision(%) | 92.54  | 86.00 | 87.39                                               |

**TrackingMamba achieves higher accuracy with a simpler model framework, fewer parameters, and lower FLOPs.**

![](https://github.com/KustTeamWQW/TrackingMamba/blob/main/img/AUC_params.png)

## Environment Settings

**Install environment using conda**

```
conda create -n trackingmamba python=3.10.13
conda activate trackingmamba
```

**Install the package for [Vim](https://github.com/hustvl/Vim)**

```
conda install cudatoolkit==11.8 -c nvidia
pip install torch==2.1.1 torchvision==0.16.1 torchaudio==2.1.1 --index-url https://download.pytorch.org/whl/cu118
conda install -c "nvidia/label/cuda-11.8.0" cuda-nvcc
conda install packaging
pip install -r vim_requirements.txt
```

**Install the mamba-1.1.1 and casual-conv1d-1.1.3 for mamba**

Download the [mamba-1.1.1](https://github.com/state-spaces/mamba/releases/download/v1.1.1/mamba_ssm-1.1.1+cu118torch2.1cxx11abiFALSE-cp310-cp310-linux_x86_64.whl) and [source code](https://github.com/Dao-AILab/causal-conv1d/archive/refs/tags/v1.1.3.zip) and place it in the project path of TrackingMamba. Go to source code and install the corresponding environment.

```
cd mamba-1.1.1
pip install .
```

Download the [casual-conv1d-1.1.3](https://github.com/Dao-AILab/causal-conv1d/releases/download/v1.1.3/causal_conv1d-1.1.3+cu118torch2.1cxx11abiFALSE-cp310-cp310-linux_x86_64.whl) and [source code](https://github.com/Dao-AILab/causal-conv1d/archive/refs/tags/v1.1.3.zip) and place it in the project path of TrackingMamba. Go to source code and install the corresponding environment.

```
cd ..
cd causal-conv1d-1.1.3
pip install .
```

**Install the package for TrackingMamba**

```
bash install.sh
```

**Run the following command to set paths for this project**

```
python tracking/create_default_local_file.py --workspace_dir . --data_dir ./data --save_dir ./output
```

**After running this command, you can also modify paths by editing these two files**

```
lib/train/admin/local.py  # paths about training
lib/test/evaluation/local.py  # paths about testing
```

## Data Preparation

**Put the tracking datasets in `./data` It should look like this:**

```
${PROJECT_ROOT}
 -- data
     -- lasot
         |-- airplane
         |-- basketball
         |-- bear
         ...
     -- got10k
         |-- test
         |-- train
         |-- val
     -- coco
         |-- annotations
         |-- images
     -- trackingnet
         |-- TRAIN_0
         |-- TRAIN_1
         ...
         |-- TRAIN_11
         |-- TEST
```

**OTMJ(Object Tracking in Mountain Jungle) Dataset**

The OTMJ dataset is an RGB dataset used for object tracking in mountainous jungle scenes. Compared to traditional datasets, OTMJ dataset features a wide range of challenging situations such as object occlusion, disappearance, camera shake, large-scale changes in object size, and low light. To more realistically simulate special conditions encountered in the jungle, we applied military camouflage to objects in some sequences.

For more specific information about OTMJ and how to obtain the dataset via [OTMJ](https://github.com/KustTeamWQW/OTMJ_Dataset).

Put OTMJ like this:

```
${PROJECT_ROOT}
 -- data
     -- OTMJ
         |-- 01
         |-- 02
         |-- 03
```



## Download Trained Weights for Model

Download [pre-trained](https://pan.baidu.com/s/1-5q4hK2LWj16K6R2PHSdPw?pwd=AHUT) and put it under `$/pretrained_models`.

## Training

```
python tracking/train.py --script trackingmamba --config trackingmamba --save_dir ./output --mode single --nproc_per_node 1 --use_wandb 0
```

## Test

Download the model weights from [[Baidu Netdisk](https://pan.baidu.com/s/1nqiHEmr0yKuaMsQtEfqnNQ?pwd=3msn)], extract code: 3msn.

Put the downloaded weights on  `$PROJECT_ROOT$/output/checkpoints/train/trackingmamba`

Change the corresponding values of `lib/test/evaluation/local.py` to the actual benchmark saving paths

```
python tracking/test.py trackingmamba --dataset otmj --threads 1 --num_gpus 1
```

Run `analysis_desults. py` for performance evaluation, including AUC, PR, NPR.

```
python tracking/analysis_results.py # need to modify tracker configs and names
```

## Acknowledgments

Thanks for the [OSTrack](https://github.com/botaoye/OSTrack), [Mamba](https://github.com/state-spaces/mamba) and [Vim](https://github.com/hustvl/Vim) library.
