# BFG_FewShot3D
Code for "Bidirectional Feature Globalization for Few-shot Semantic Segmentation of 3D Point Cloud Scenes".

## Installation
- Install `python` --This repo is tested with `python 3.6`.
- Install `pytorch` with CUDA -- This repo is tested with `torch 1.7`, `CUDA 11`. 
- Install dependencies
    ```
    pip install tensorboard h5py transforms3d
    ```

## Usage
### Data preparation
#### S3DIS
1. Download [S3DIS Dataset Version 1.2](http://buildingparser.stanford.edu/dataset.html).
2. Re-organize raw data into `npy` files by running
   ```
   cd ./preprocess
   python collect_s3dis_data.py --data_path $path_to_S3DIS_raw_data
   ```
   The generated numpy files are stored in `./datasets/S3DIS/scenes/data` by default.
3. To split rooms into blocks, run 

    ```python ./preprocess/room2blocks.py --data_path ./datasets/S3DIS/scenes/```
    
    One folder named `blocks_bs1_s1` will be generated under `./datasets/S3DIS/` by default. 


#### ScanNet
1. Download [ScanNet V2](http://www.scan-net.org/).
2. Re-organize raw data into `npy` files by running
	```
	cd ./preprocess
	python collect_scannet_data.py --data_path $path_to_ScanNet_raw_data
	```
   The generated numpy files are stored in `./datasets/ScanNet/scenes/data` by default.
3. To split rooms into blocks, run 

    ```python ./preprocess/room2blocks.py --data_path ./datasets/ScanNet/scenes/ --dataset scannet```
    
    One folder named `blocks_bs1_s1` will be generated under `./datasets/ScanNet/` by default. 


### Running 
#### Training
First, pretrain the segmentor which includes feature extractor module on the available training set:
    
    cd scripts
    bash pretrain_segmentor.sh

Second, train our method:
	
	bash train_BFG.sh


#### Evaluation
    
    bash eval_BFG.sh

## References
This repo is built based on [DGCNN (pytorch)](https://github.com/WangYueFt/dgcnn/tree/master/pytorch) and [attMPTI](https://github.com/Na-Z/attMPTI). Thanks for their great works!


## Citation
If you find our work and this repository useful. Please consider giving a star :star: and citation &#x1F4DA;.
