# Stable Diffusion text-to-image fine-tuning

## Running locally with MindSpore

| Ascend | MindSpore Version                                   | CANN Version                                                                                                      |
|--------|-----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| 910*   | [MS 2.3.0](https://www.mindspore.cn/versions#2.3.0) | [CANN 8.0.RC2.beta1](https://www.hiascend.com/developer/download/community/result?module=cann&cann=8.0.RC2.beta1) |

**Note**: You can use `cat /usr/local/Ascend/ascend-toolkit/latest/version.cfg` check the CANN version and you can see the specific version number `[7.3.0.1.231:8.0.RC2]`. If you have a custom installation path for CANN, find the `version.cfg` in your own CANN installation path to verify the version.

## Training

We trained on the [OnePiece dataset](https://huggingface.co/datasets/YaYaB/onepiece-blip-captions) and recorded the training speed as follows.

| Method  | NPUs | Global <br/>Batch size | Resolution   | Precision | Graph Compile | Speed <br/>(ms/step) | FPS <br/>(img/s) |
|---------|------|------------------------|--------------|-----------|-----------|----------------------|------------------|
| Vanilla | 1    | 1*1                    | 512x512      | FP16      | 1~5 min   | 260                  | 3.85             |
| Vanilla | 8    | 1*8                    | 512x512      | FP16      | 1~5 min   | 404                  | 19.8             |
| LoRA    | 1    | 1*1                    | 512x512      | FP16      | 1~5 min   | 200                  | 5.00             |
| LoRA    | 8    | 1*8                    | 512x512      | FP16      | 1~5 min   | 231                  | 34.63            |

## Inference

### Vanilla Fine-tuning

We trained 6k steps based on the [OnePiece dataset](https://huggingface.co/datasets/YaYaB/onepiece-blip-captions). Here are some of the results of the fine-tuning and the training details are recorded [here](https://github.com/liuchuting/mindone/blob/sd_doc/examples/diffusers/text_to_image/README.md#hardware).

|                                                                      a girl with a mask on her face                                                                      |                                                                 a man holding a book                                                                  |                                                                 a man holding a sword                                                                  |                                                                 a man sitting on top of a flower                                                                  |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_girl_with_a_mask_on_her_face.png?raw=true" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_man_holding_a_book.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_man_holding_a_sword.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_man_sitting_on_top_of_a_flower.png" width=224> |

|                                                                 a man with a beard and a shirt                                                                  |                                                                 a man with a knife in his hand                                                                  |                                                                 a smiling woman in a helmet                                                                  |                                                                 a woman in a white dress                                                                  |
|:---------------------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------:|
| <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_man_with_a_beard_and_a_shirt.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_man_with_a_knife_in_his_hand.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_smiling_woman_in_a_helmet.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_base_infer/a_woman_in_a_white_dress.png" width=224> |

### LoRA Fine-tuning

We trained 15k steps based on the [OnePiece dataset](https://huggingface.co/datasets/YaYaB/onepiece-blip-captions). Here are some of the results of the lora fine-tuning and the training details are recorded [here](https://github.com/liuchuting/mindone/blob/sd_doc/examples/diffusers/text_to_image/README.md#training).

|                                                                      a man in a hat and jacket                                                                      |                                                                 a man in a yellow coat                                                                  |                                                                 a man with a big smile on his face                                                                  |                                                                 a man with a hat and mustache                                                                  |
|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_lora_infer/a_man_in_a_hat_and_jacket.png?raw=true" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_lora_infer/a_man_in_a_yellow_coat.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_lora_infer/a_man_with_a_big_smile_on_his_face.png" width=224> | <img src="https://github.com/liuchuting/mindone/blob/image/examples/diffusers/text_to_image/images/sd_lora_infer/a_man_with_a_hat_and_mustache.png" width=224> |
