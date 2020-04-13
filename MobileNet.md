# AI-learning-source
My AI Learning
### TF Slim: Fine Tune mobilenet v2 on custom dataset
I am trying to fine-tune Mobilenet_v2_1.4_224 model on my custom dataset for Image Classification task. I am following this tutorial [TensorFlow-Slim image classification library](https://stackoverflow.com/questions/49680440/tf-slim-fine-tune-mobilenet-v2-on-custom-dataset). I have already created the .tfrecord train and validation files. When I try to fine tune from an existing checkpoint I get the following error:
InvalidArgumentError (see above for traceback): Assign requires shapes of both tensors to match. lhs shape= [1,1,24,144] rhs shape= [1,1,32,192] [[Node: save/Assign_149 = Assign[T=DT_FLOAT, _class=["loc:@MobilenetV2/expanded_conv_2/expand/weights"], use_locking=true, validate_shape=true, _device="/job:localhost/replica:0/task:0/device:CPU:0"](MobilenetV2/expanded_conv_2/expand/weights, save/RestoreV2:149)]]
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
