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

## Optimizers

### ADAM with Manual Step
```
 optimizer {
    adam_optimizer: {
      epsilon: 1e-7  # Match tf.keras.optimizers.Adam's default.
      learning_rate: {
        manual_step_learning_rate {
          initial_learning_rate: 1e-3
          schedule {
           step: 90000
           learning_rate: 1e-4
          }
          schedule {
            step: 120000
            learning_rate: 1e-5
          }
        }
      }
```

### ADAM with Cosine Decay
```
  optimizer {
    adam_optimizer: {
      epsilon: 1e-7  # Match tf.keras.optimizers.Adam's default.
      learning_rate: {
        cosine_decay_learning_rate {
          learning_rate_base: 1e-3
          total_steps: 50000
          warmup_learning_rate: 2.5e-4
          warmup_steps: 5000
        }
      }
    }
    use_moving_average: false
  }
```
# Momentum with Cosine Decay
```
optimizer {
    momentum_optimizer: {
      learning_rate: {
        cosine_decay_learning_rate {
          learning_rate_base: .04
          total_steps: 25000
          warmup_learning_rate: .013333
          warmup_steps: 2000
        }
      }
      momentum_optimizer_value: 0.9
    }
    use_moving_average: false
  }
```
## Augemtations
```
data_augmentation_options {
    random_horizontal_flip {
    }
  }

  data_augmentation_options {
    random_adjust_hue {
    }
  }

  data_augmentation_options {
    random_adjust_contrast {
    }
  }

  data_augmentation_options {
    random_adjust_saturation {
    }
  }

  data_augmentation_options {
    random_adjust_brightness {
    }
  }

  data_augmentation_options {
     random_square_crop_by_scale {
      scale_min: 0.6
      scale_max: 1.3
    }
  }

  data_augmentation_options {
    random_crop_image {
      min_aspect_ratio: 0.5
      max_aspect_ratio: 1.7
      random_coef: 0.25
    }
  }

  data_augmentation_options {
    random_absolute_pad_image {
       max_height_padding: 200
       max_width_padding: 200
       pad_color: [0, 0, 0]
    }
  }

  data_augmentation_options {
    ssd_random_crop {
    }
  }
```
