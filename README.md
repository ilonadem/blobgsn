## BlobGSN: Generative Scene Networks with Mid-Level Blob Representations
**Unconstrained Scene Generation with Locally Conditioned Radiance Fields and Mid-Level Blob Representations**<br>
Allen Zhang, David Fang, Ilona Demler<br>

### [Project Page](https://ilonadem.github.io/blobgsn-demo/) |  | [Data](#datasets)

We combined Blob GAN with Generative Scene Networks architecture to generate editable 3D scenes. Namely, we use Gaussian Blobs to map to a 2-D floorplan that is then used to locally condition a radiance field that represents a 3D scene. By moving, shifting, scaling, removing, and adding the blobs in the mid-level latent space representation we are able to make corresponding changes in the rendered scene. The result is a customizable + editable 3D scene.

### Moving blobs in a scene 

### Walking through a scene
## Requirements
This code was tested with Python 3.6 and CUDA 11.1.1, and uses Pytorch Lightning. A suitable conda environment named `gsn` can be created and activated with:
```
conda env create -f environment.yaml python=3.6
conda activate gsn
```
If you do not already have CUDA installed, you can do so with:
```
wget https://developer.download.nvidia.com/compute/cuda/11.1.1/local_installers/cuda_11.1.1_455.32.00_linux.run
sh cuda_11.1.1_455.32.00_linux.run --toolkit --silent --override
rm cuda_11.1.1_455.32.00_linux.run
```
Custom CUDA kernels may not work with older versions of CUDA. This code will revert to a native PyTorch implementation if the CUDA version is incompatible, although runtime may be ~25% slower.

## Datasets
We provide camera trajectories for two datasets that we used to trained our model: Vizdoom and Replica. These datasets are composed of different sequences with corresponding rgb+depth frames and camera parameters (extrinsiscs and intrinsics).

Dataset | Size | Download Link
--- | :---: | :---:
Vizdoom | 2.4 GB | [download](<https://docs-assets.developer.apple.com/ml-research/datasets/gsn/vizdoom.zip>)
Replica | 11.0 GB | [download](<https://docs-assets.developer.apple.com/ml-research/datasets/gsn/replica.zip>)

Datasets can be downloaded by running the following scripts:  
**VizDoom**<br>
```
python scripts/download_vizdoom.py
```
**Replica**<br>
```
python scripts/download_replica.py
```

## Interactive exploration demo
We provide a [Jupyter notebook](notebooks/walkthrough_demo.ipynb) that allows for interactive exploration of scenes generated from a pre-trained model. Use the WASD keys to freely navigate through the scene! Once you are done, the notebook interpolates the camera path to render a continuous trajectory. Note: You need to download the Replica dataset before via this [script](scripts/download_replica.py) before running the notebook.

Explore scene with WASD to set keypoints | Rendered trajectory
:---: | :---:
<img src="./assets/keyframes.gif" width=256px> | <img src="./assets/camera_trajectory.gif" width=256px>

## Training models
Download the training dataset (if you have not done so already) and begin training with the following commands:  
**VizDoom**<br>
```
bash scripts/launch_gsn_vizdoom_64x64.sh
```

**Replica**<br>
```
bash scripts/launch_gsn_replica_64x64.sh
```

Training takes about 3 days to reach 500k iterations with a batch size of 32 on two A100 GPUs.


