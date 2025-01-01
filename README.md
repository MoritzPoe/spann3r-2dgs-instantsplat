
<h2 align="center"> <a href="https://arxiv.org/abs/2403.20309">InstantSplat: Sparse-view SfM-free <a href="https://arxiv.org/abs/2403.20309"> Gaussian Splatting in Seconds </a>

<h5 align="center">

[![arXiv](https://img.shields.io/badge/Arxiv-2403.20309-b31b1b.svg?logo=arXiv)](https://arxiv.org/abs/2403.20309) [![Gradio](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-blue)](https://huggingface.co/spaces/kairunwen/InstantSplat) 
[![Home Page](https://img.shields.io/badge/Project-Website-green.svg)](https://instantsplat.github.io/) [![X](https://img.shields.io/badge/-Twitter@Zhiwen%20Fan%20-black?logo=twitter&logoColor=1D9BF0)](https://x.com/WayneINR/status/1774625288434995219)  [![youtube](https://img.shields.io/badge/Demo_Video-E33122?logo=Youtube)](https://youtu.be/fxf_ypd7eD8) [![youtube](https://img.shields.io/badge/Tutorial_Video-E33122?logo=Youtube)](https://www.youtube.com/watch?v=JdfrG89iPOA&t=347s)
</h5>

<div align="center">
This repository is the official implementation of InstantSplat, an sparse-view, SfM-free framework for large-scale scene reconstruction method using Gaussian Splatting.
InstantSplat supports 3D-GS, 2D-GS, and Mip-Splatting.
</div>
<br>

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Mesh Reconstruction](#mesh-reconstruction)
- [TODO List](#todo-list)
- [Get Started](#get-started)
  - [Installation](#installation)
  - [Usage](#usage)
- [Acknowledgement](#acknowledgement)
- [Citation](#citation)


## Mesh Reconstruction
![visualization](assets/mesh_recon.png)

## TODO List
- [x] Support 2D-GS
- [ ] Support Mip-Splatting

## Get Started

### Installation
1. Clone InstantSplat and download pre-trained model.
```bash
git clone --recursive -b instantsplat-2dgs https://github.com/NVlabs/InstantSplat.git
cd InstantSplat
mkdir -p mast3r/checkpoints/
wget https://download.europe.naverlabs.com/ComputerVision/MASt3R/MASt3R_ViTLarge_BaseDecoder_512_catmlpdpt_metric.pth -P mast3r/checkpoints/
```

2. Create the environment (or use pre-built docker), here we show an example using conda.
```bash
conda create -n instantsplat python=3.10.13 cmake=3.14.0 -y
conda activate instantsplat
conda install pytorch torchvision pytorch-cuda=12.1 -c pytorch -c nvidia  # use the correct version of cuda for your system
pip install -r requirements.txt
pip install submodules/simple-knn
pip install submodules/diff-surfel-rasterization
pip install submodules/fused-ssim
```

3. Optional but highly suggested, compile the cuda kernels for RoPE (as in CroCo v2).
```bash
# DUST3R relies on RoPE positional embeddings for which you can compile some cuda kernels for faster runtime.
cd croco/models/curope/
python setup.py build_ext --inplace
```

Alternative: use the pre-built docker image: pytorch/pytorch:2.1.2-cuda11.8-cudnn8-devel
```
docker pull dockerzhiwen/instantsplat_public:2.0
```
After setting up a new container, make sure to install the right library (e.g., diff-surfel-rasterization) for 2D-GS.


### Usage
1. Data preparation (download our pre-processed data from: [Hugging Face](https://huggingface.co/datasets/kairunwen/InstantSplat) or [Google Drive](https://drive.google.com/file/d/1K_xtwPKc7y8YAG78L0PH5ldR4PlfG-GR/view?usp=sharing))
```bash
  cd <data_path>
  # then do whatever data preparation
```

2. Command
```bash
  # InstantSplat train and output video (no GT reference, render by interpolation) using the following command.
  bash scripts/run_infer.sh

  # InstantSplat train and evaluate (with GT reference) using the following command.
  bash scripts/run_eval.sh
```

## Acknowledgement

This work is built on many amazing research works and open-source projects, thanks a lot to all the authors for sharing!

- [Gaussian-Splatting](https://github.com/graphdeco-inria/gaussian-splatting) and [diff-gaussian-rasterization](https://github.com/graphdeco-inria/diff-gaussian-rasterization)
- [DUSt3R](https://github.com/naver/dust3r)

## Citation
If you find our work useful in your research, please consider giving a star :star: and citing the following paper :pencil:.

```bibTeX
@misc{fan2024instantsplat,
        title={InstantSplat: Unbounded Sparse-view Pose-free Gaussian Splatting in 40 Seconds},
        author={Zhiwen Fan and Wenyan Cong and Kairun Wen and Kevin Wang and Jian Zhang and Xinghao Ding and Danfei Xu and Boris Ivanovic and Marco Pavone and Georgios Pavlakos and Zhangyang Wang and Yue Wang},
        year={2024},
        eprint={2403.20309},
        archivePrefix={arXiv},
        primaryClass={cs.CV}
      }
```
