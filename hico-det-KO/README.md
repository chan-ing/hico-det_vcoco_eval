# HO-RCNN's HICO-DET eval process

Code for reproducing the results in the following paper:

**Learning to Detect Human-Object Interactions**  
Yu-Wei Chao, Yunfan Liu, Xieyang Liu, Huayi Zeng, Jia Deng  
IEEE Winter Conference on Applications of Computer Vision (WACV), 2018  

Check out the [project site](https://umich-ywchao-hico.github.io/) for more details.


### Acknowledgements

Some of the instructions in this README are modified from the [fast-rcnn](https://github.com/rbgirshick/fast-rcnn) repo created by [Ross Girshick](https://github.com/rbgirshick).

### Clone the Repository

This repo relies on two submodules (`fast-rcnn` and `caffe`), so make sure you clone with `--recursive`:

  ```Shell
  git clone --recursive https://github.com/ywchao/ho-rcnn.git
  ```


## Evaluation

This demo runs the MATLAB evaluation script and replicates our results in the paper.

1. Download HICO-DET (7.5G):

    ```Shell
    1. If you have not downloaded the dataset before, run the following script.
        ```bash
        cd /path/to/hico-det-KO/data
        bash download.sh
        ```
    2. If you have previously downloaded the dataset, simply create a soft link.
        ```bash
        cd /path/to/hico-det-KO/data
        ln -s /path/to/hicodet_20160224_det ./hico_20160224_det
        ```
    
    ```

    This will populate the `data` folder with `hico_20160224_det`.

2. Download pre-computed HOI detection on the HICO-DET test set (2.0G):

    ```Shell
    ./scripts/fetch_hoi_detection.sh
    ./scripts/setup_symlinks_detection.sh
    ```

    This will populate the `output` folder with `precomputed_hoi_detection` and set up a set of symlinks.

"YOU NEED MATLAB tools"
check your local
    ```Shell
    which matlab
    
    #to start matlab, just type
    matlab
    ```
    
    
3. Evaluating on 600 classes is tedious, so we use `parfor` to speed up. Uncomment and set `poolsize` in `config.m` according to your need, or leave it commented out if you want MATLAB to set it automatically.

4. Start MATLAB `matlab` under `ho-rcnn`. You should see the message `added paths for the experiment!` followed by the MATLAB prompt `>>`.

cached file direction : hico-det-KO/output/pvic/hico_det_test_2015/detections_01.mat ... detections_80.mat
.mat files come from your own model


5. Run **`eval_run`**. This will run the evaluation for the experiment **HO**, under the Default and Known Object setting sequentially. The results will be printed and also saved under the folder `evaluation/result`. **If you want restart the other experiments remove 'result' folder**

6. You can run the evaluation for other experiments (which appear in the paper) by editing `eval_run.m` and rerunning it. 
For example, comment the line started with `exp_name = 'rcnn_caffenet_ho_pconv_ip1_s';` and uncomment the line started with `exp_name = 'rcnn_caffenet_ho_pconv_ip1';`.



