# AI-learning-source
My AI Learning
### TF Slim: Fine Tune mobilenet v2 on custom dataset
I am trying to fine-tune Mobilenet_v2_1.4_224 model on my custom dataset for Image Classification task. I am following this tutorial TensorFlow-Slim image classification library. I have already created the .tfrecord train and validation files. When I try to fine tune from an existing checkpoint I get the following error:
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
