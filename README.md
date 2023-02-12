# lora concepts template

This is a template that can be used for training multiple concepts and regularization images for lora (Low-rank Adaptation) models.

- lora: https://github.com/cloneofsimo/lora

- Based off of training scripts by [kohya-ss sd-scripts](https://github.com/kohya-ss/sd-scripts)

## Multiple concept loRA structure

| Directory                | Description                                                                                          |
|--------------------------|------------------------------------------------------------------------------------------------------|
| `image_dir`              | contains all input images and captioning files, prefixed by the total number of epoch per image      |
| `reg_dir`                | contains all regularations images per concept, prefixed by the total number of repeats per reg image |
| `log`                    | records of each training log                                                                         |
| `output`                 | the final output binary (safesensor, pt, etc)                                                        |
| `config_v1_example.json` | the config for the training session (rename to whatever you want)                                    |

## Balancing datasets

Balance the datasets so that the concept folders indicate the number of times they should be repeated during training.

For example, let's say you have four concepts and each of those has `14` images per concept, except for one, which has `28`.

To balance this for training steps per concept per epoch `5200`, you would divide the repeats by the total amount of images per concept:

```5200 / 14 = 371```
```5200 / 28 = 186```

In the example, the name of the concept directories would be:

- 186_conceptA
- 371_conceptB
- 371_conceptC
- 371_conceptD

### bmaltais utilities
The below utility will ensure that each concept folder in the dataset folder is used equally during the training process of the dreambooth machine learning model, regardless of the number of images in each folder:

https://github.com/bmaltais/kohya_ss/blob/cdf84e2f4b65517c396ffb72474616a57bc109b6/library/dataset_balancing_gui.py

- https://github.com/bmaltais/kohya_ss