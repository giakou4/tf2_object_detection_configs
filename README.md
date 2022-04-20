# TensorFlow 2.x Object Detection Configs

Repository of ```.configs``` for the [TensorFlow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection).

The repository aims on having the initial configuration, which lies at [here](https://github.com/tensorflow/models/tree/master/research/object_detection/configs/tf2). In addition, another ```.config``` file with the suffix ```_no_augmentation.config``` exist where all the augmentation is removed. This is done due to the fact that [Roboflow](https://roboflow.com/) includes augmentation is the ```.tfrecord``` file generated from the original dataset. However, all the augmentation options are included in the ```augmentations_all.config``` where one can manually add them in the ```.config``` file. Moreover, ```optimizers_all.config``` includes ADAM and Momentum optimizers where one can manually override in the ```.config``` file.

## Notes

### Faster R-CNN
All Faster R-CNN make use of the ```momentum_optimizer``` with ```cosine_decay_learning_rate```. Augmentation includes ```random_horizontal_flip```, ```random_adjust_hue```, ```random_adjust_contrast```, ```random_adjust_saturation```, and ```random_square_crop_by_scale```.

### CenterNet (Hourglass)
All CenterNet make use of the ```adam_optimizer``` with ```manual_step_learning_rate```. Augmentation includes ```random_horizontal_flip```, ```random_crop_image```, ```random_adjust_hue```, ```random_adjust_contrast```, ```random_adjust_saturation```, ```random_adjust_brightness```, and ```random_absolute_pad_image```.

### EfficientDet
All EfficientDet make use of the ```momentum_optimizer``` with ```cosine_decay_learning_rate```. Augmentation include ```random_horizontal_flip```, and ```random_scale_crop_and_pad_to_square```.

### SSD
All SSD (exluded EfficientDet) make use of the ```momentum_optimizer``` with ```cosine_decay_learning_rate```. Augmentation includes random_horizontal_flip, random_crop_image, ssd_random_crop, 
