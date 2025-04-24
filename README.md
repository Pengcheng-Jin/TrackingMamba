# TrackingMamba

**TrackingMamba: Visual State Space Model for Object Tracking**

Qingwang Wang, Liyao Zhou, Pengcheng Jin, Xin Qu, Hangwei Zhong, Haochen Song, Tao Shen

![](https://github.com/KustTeamWQW/TrackingMamba/blob/main/img/trackingmamba_framework.JPG)

## News

[September 23, 2024]

Our paper "TrackingMamba: Visual State Space Model for Object Tracking" has been accepted and published in the IEEE Journal of Selected Topics in Applied Earth Observations and Remote Sensing. You can access the paper through the following DOI: 10.1109/JSTARS.2024.3458938.

[August 7, 2024]

Source code and weights are all released.

## Highlights

#### **Visual State Space Model for Object Tracking**

This paper proposes a new tracking framework based on the state space model, named TrackingMamba, which adopts a single-stream tracking architecture with Vision Mamba as the backbone. TrackingMamba not only rivals transformer-based trackers in global feature extraction and long-range dependency modeling but also maintains computational cost in a linear growth manner.  Compared to other advanced trackers, TrackingMamba achieves higher accuracy with a simpler model framework, fewer parameters, and lower FLOPs. Especially when compared with the baseline model OSTrack-256, TrackingMamba shows an improvement of 2.59\% in AUC and 4.42\% in Precision on the UAV123 benchmark.This paper also evaluates the performance and limitations of TrackingMamba and several current advanced trackers in the crucial and complex scenario of forests, and further contemplates and summarizes potential future research directions in the field of UAV object tracking in forest environments.

|       | UAV123 | DTB70 | OTMJ |
|:------|:------:|:-----:|:----:|
| AUC(%) | 70.89  | 66.21 | 65.54 |


**TrackingMamba achieves higher accuracy with a simpler model framework, fewer parameters, and lower FLOPs.**

![](https://github.com/KustTeamWQW/TrackingMamba/blob/main/img/AUC_params.png)


### 效果预览：
在 GitHub 上会显示为：

---

# Environment Settings

## Install environment using conda

```bash
# Create a new conda environment named 'trackingmamba' with Python 3.10.13
conda create -n trackingmamba python=3.10.13

# Activate the environment
conda activate trackingmamba
