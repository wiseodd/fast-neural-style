# fast-neural-style 
Based on Johnson, 2016's paper: [Perceptual Losses for Real-Time Style Transfer and Super-Resolution](https://arxiv.org/abs/1603.08155) along with [Instance Normalization](https://arxiv.org/pdf/1607.08022.pdf)

Original implementation: <https://github.com/abhiskk/fast-neural-style>.
Difference with the original implementation is that here, there are more options regarding training and evaluation, e.g. use BatchNorm, which layers to be used in the loss, etc.

## Requirements
1. PyTorch
2. MS COCO 2014 (if you want to train new style)

## Usage
Stylize image
```
python neural_style/neural_style.py eval --content-image </path/to/content/image> --model </path/to/saved/model> --output-image </path/to/output/image> --cuda 0
```
* `--content-image`: path to content image you want to stylize.
* `--model`: saved model to be used for stylizing the image (eg: `mosaic.pth`)
* `--output-image`: path for saving the output image.
* `--content-scale`: factor for scaling down the content image if memory is an issue (eg: value of 2 will halve the height and width of content-image)
* `--cuda`: set it to 1 for running on GPU, 0 for CPU.
* `--instancenorm`: add this flag to use InstanceNorm, otherwise BatchNorm is used.

Train model
```bash
python neural_style/neural_style.py train --dataset </path/to/train-dataset> --style-image </path/to/style/image> --vgg-model-dir </path/to/vgg/folder> --save-model-dir </path/to/save-model/folder> --epochs 2 --cuda 1
```

There are several command line arguments, the important ones are listed below
* `--dataset`: path to training dataset, the path should point to a folder containing another folder with all the training images. I used COCO 2014 Training images dataset [80K/13GB] [(download)](http://mscoco.org/dataset/#download).
* `--style-image`: path to style-image.
* `--vgg-model-dir`: path to folder where the vgg model will be downloaded.
* `--save-model-dir`: path to folder where trained model will be saved.
* `--cuda`: set it to 1 for running on GPU, 0 for CPU.
* `--instancenorm`: add this flag to use InstanceNorm, otherwise BatchNorm is used.
* `--max_imgs`: number of images used per epoch (useful for very large dataset and limited time).
* `--contentloss_layer`: available options are {0: relu1_2; 1: relu_2_2; 3: relu3_3; 4: relu4_3}, default is 1.
* `--styleloss_layers`: available options are {0: relu1_2; 1: relu_2_2; 3: relu3_3; 4: relu4_3}, default is `0 1 2 3`

Refer to ``neural_style/neural_style.py`` for other command line arguments.

## Models

Models for the examples shown below can be downloaded from [here](https://www.dropbox.com/s/gtwnyp9n49lqs7t/saved-models.zip?dl=0) or by running the script ``download_styling_models.sh`` (credit to original author <https://github.com/abhiskk/fast-neural-style>).
