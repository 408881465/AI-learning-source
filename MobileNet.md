# AI-learning-source
My AI Learning
### TF Slim: [Fine Tune mobilenet v2 on custom dataset](https://stackoverflow.com/questions/49680440/tf-slim-fine-tune-mobilenet-v2-on-custom-dataset)
I am trying to fine-tune Mobilenet_v2_1.4_224 model on my custom dataset for Image Classification task. I am following this tutorial [TensorFlow-Slim image classification library](https://github.com/tensorflow/models/tree/546fd48ecb70635e5b086143c252649b217df59d/slim/#Tuning). I have already created the .tfrecord train and validation files. When I try to fine tune from an existing checkpoint I get the following error:
InvalidArgumentError (see above for traceback): Assign requires shapes of both tensors to match. lhs shape= [1,1,24,144] rhs shape= [1,1,32,192] [[Node: save/Assign_149 = Assign[T=DT_FLOAT, _class=["loc:@MobilenetV2/expanded_conv_2/expand/weights"], use_locking=true, validate_shape=true, _device="/job:localhost/replica:0/task:0/device:CPU:0"](MobilenetV2/expanded_conv_2/expand/weights, save/RestoreV2:149)]]
The fine-tuning script that I have used is:

DATASET_DIR=G:\Dataset

TRAIN_DIR=G:\Dataset\emotion-models\mobilenet_v2

CHECKPOINT_PATH=C:\Users\lenovo\Desktop\mobilenet_v2\mobilenet_v2_1.4_224.ckpt

I suspect that the error is due to the last 2 arguments "checkpoint_exclude_scopes" or "trainable_scopes".

I know that these 2 arguments are being used for transfer learning by removing the last 2 layers and creating our own softmax layer for custom dataset classficiation. But I'm not sure if I'm passing the right values for them.
```shell

python train_image_classifier.py \
--train_dir=${TRAIN_DIR} \
--dataset_dir=${DATASET_DIR} \
--dataset_name=emotion \
--dataset_split_name=train \
--model_name=mobilenet_v2 \
--train_image_size=224 \
--clone_on_cpu=True \
--checkpoint_path=${CHECKPOINT_PATH} \
#--checkpoint_exclude_scopes=MobilenetV2/Logits \
#--trainable_scopes=MobilenetV2/Logits

--checkpoint_exclude_scopes=MobilenetV2/Logits,MobilenetV2/Predictions,MobilenetV2/predics \
--trainable_scopes=MobilenetV2/Logits,MobilenetV2/Predictions,MobilenetV2/predics \

```
In mobilenet_v2.py, depth_multiplier=1 for both mobilenet and mobilenet_base, you should change that to 1.4
```shell
@slim.add_arg_scope 
def mobilenet_base(input_tensor, depth_multiplier=1.4, **kwargs): 
"""Creates base of the mobilenet (no pooling and no logits) .""" 
return mobilenet(input_tensor,
                 depth_multiplier=depth_multiplier,
                 base_only=True, **kwargs)

@slim.add_arg_scope 
def mobilenet(input_tensor,
                  num_classes=1001,
                  depth_multiplier=1.4,
                  scope='MobilenetV2',
                  conv_defs=None,
                  finegrain_classification_mode=False,
                  min_depth=None,
                  divisible_by=None,
                  **kwargs):
```
### [Mobilenet V2 on checkpoint inference Example.ipynb](https://colab.research.google.com/drive/1Acs79Ob0hy_cvlFIqQwAsZVPCkn9Dxe1#scrollTo=qSU2h5NRlN7V)
[AttributeError: module 'tensorflow._api.v1.compat' has no attribute 'v2' ](https://github.com/tensorflow/models/issues/8088)

[slim_walkthrough](https://colab.research.google.com/github/tensorflow/models/blob/master/research/slim/slim_walkthrough.ipynb#scrollTo=1KeLXG_ln2ga)
