# RobotOD


Needed Packages:
  pandas
  glob3
  argparse
  tensorflow
  Pillow

Put /train and /test into a /images folder in this repository after cloning it 
https://github.com/tensorflow/models/tree/master/research/object_detection

from there run this command after downloading tensorflow to the jetson:

python generate_tfrecord.py --csv_input=images\train_labels.csv --image_dir=images\train --output_path=train.record
python generate_tfrecord.py --csv_input=images\test_labels.csv --image_dir=images\test --output_path=test.record

copy config file you want into the training folder
Change a few lines in the config file you want to use:
line 106 to path of model.ckpt
line 123 path of train.record
line 135 to test.records
line 125-137 to path of label map
130 number of images in test folder 

python model_main.py --logtostderr --train_dir=training/ --pipeline_config_path=training/faster_rcnn_inception_v2_pets.config

tensorboard --logdir=training


python export_inference_graph.py --input_type image_tensor --pipeline_config_path training/faster_rcnn_inception_v2_pets.config --trained_checkpoint_prefix training/model.ckpt-XXXX --output_directory inference_graph

replace XXXX with higest step number in model.ckpt
