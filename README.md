# Toward Characteristic-Preserving Image-based Virtual Try-On Network

Reimplemented code for eccv2018 paper 'Toward Characteristic-Preserving Image-based Virtual Try-On Network'. 
The results may have some differences with those of the original code.

## Data preprocessing

We convert the original data [VITON](https://github.com/xthan/VITON) into different directories for easily use. 
Run the matlab code ```convert_data.m ``` under the original data root ```VITON/data```, and get the new format.
We use the json format for pose info as generated by [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose).
Move these directories into our own dataroot ```data```.

## Geometric Matching Module

### training
We just use L1 loss for criterion in this code. 
TV norm constraints for the offsets will make GMM more robust.
An example training command is
```
python train.py --name gmm_train_new --stage GMM --workers 4 --save_count 5000 --shuffle
```
You can see the results in tensorboard, as show below.
<div align="center">
  <img src="examples/gmm_train_example.png" width="576px" />
    <p>Example of GMM train</p>
</div>

### eval

Choose the different source data for eval with the option ```--datamodel```.

An example training command is
```
python test.py --name gmm_traintest_new --stage GMM --workers 4 --datamode test --data_list test_pairs.txt --checkpoint checkpoints/gmm_train_new/gmm_final.pth
```

You can see the results in tensorboard, as show below.
<div align="center">
  <img src="examples/gmm_test_example.png" width="576px" />
    <p>Example of GMM test</p>
</div>

## Try-On Module
### training
An example training command is
```
python train.py --name tom_train_new --stage TOM --workers 4 --save_count 5000 --shuffle 
```
You can see the results in tensorboard, as show below.
<div align="center">
  <img src="examples/tom_train_example.png" width="576px" />
    <p>Example of TOM train</p>
</div>


### eavl
An example training command is
```
python test.py --name tom_test_new --stage TOM --workers 4 --datamode test --data_list test_pairs.txt --checkpoint checkpoints/tom_train_new/tom_final.pth
```
You can see the results in tensorboard, as show below.
<div align="center">
  <img src="examples/tom_test_example.png" width="576px" />
    <p>Example of TOM test</p>
</div>


## Citation
If this code helps your research, please cite our paper:

