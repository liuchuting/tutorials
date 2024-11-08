# Stable Diffusion text-to-image fine-tuning

## Requirements

| mindspore  | ascend driver  |  firmware   |cann toolkit/kernel |
|:----------:|:--------------:|:-----------:|:------------------:|
|   2.3.1    |    24.1.RC2    | 7.3.0.1.231 |   8.0.RC2.beta1    |

## Training

Experiments are tested on ascend 910* graph mode with a single card.

|  method | batch size | resolution | precision | jit level | graph compile | s/step | img/s |
|:-------:|:----------:|:----------:|:---------:|:---------:|:-------------:|:------:|:-----:|
| vanilla |     1      |  512x512   |   FP16    |    O0     |   1~5 mins    |  0.58  | 1.72  |
|  lora   |     1      |  512x512   |   FP16    |    O0     |   1~5 mins    |  0.29  | 3.45  |

## Inference

### Vanilla Fine-tuning

The training details are recorded [here](https://github.com/mindspore-lab/mindone/blob/master/examples/diffusers/text_to_image/README.md#hardware), we trained 6k steps based on the [OnePiece dataset](https://huggingface.co/datasets/YaYaB/onepiece-blip-captions) and here are some of results:

|                                                                      a girl with a mask on her face                                                                      |                                                                 a man holding a book                                                                  |                                                                 a man holding a sword                                                                  |                                                                 a man sitting on top of a flower                                                                  |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_girl_with_a_mask_on_her_face.png?raw=true" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_man_holding_a_book.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_man_holding_a_sword.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_man_sitting_on_top_of_a_flower.png" width=224> |

|                                                                 a man with a beard and a shirt                                                                  |                                                                 a man with a knife in his hand                                                                  |                                                                 a smiling woman in a helmet                                                                  |                                                                 a woman in a white dress                                                                  |
|:---------------------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------:|
| <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_man_with_a_beard_and_a_shirt.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_man_with_a_knife_in_his_hand.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_smiling_woman_in_a_helmet.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_woman_in_a_white_dress.png" width=224> |

### LoRA Fine-tuning

The training details are recorded [here](https://github.com/mindspore-lab/mindone/blob/master/examples/diffusers/text_to_image/README.md#training), we trained 6k steps based on the [OnePiece dataset](https://huggingface.co/datasets/YaYaB/onepiece-blip-captions) and here are some of results:

|                                                                      a man in a hat and jacket                                                                      |                                                                 a man in a yellow coat                                                                  |                                                                 a man with a big smile on his face                                                                  |                                                                 a man with a hat and mustache                                                                  |
|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_lora_infer/a_man_in_a_hat_and_jacket.png?raw=true" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_lora_infer/a_man_in_a_yellow_coat.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_lora_infer/a_man_with_a_big_smile_on_his_face.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_lora_infer/a_man_with_a_hat_and_mustache.png" width=224> |
