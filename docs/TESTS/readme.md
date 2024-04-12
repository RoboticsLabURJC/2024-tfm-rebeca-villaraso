- ### TEST 1. DeepLabV3+ on "instance_level_human_parsing" dataset
- ### TEST 2. DeepLabV3+ on "Cityscapes" dataset
    #### 1. Pretrained model:
      pretrained_models/model_13_2_2_2_epoch_580.pth: Trained for 580 epochs on Cityscapes train and 3333 + 745 images from Berkeley DeepDrive.
    #### 2. Dataset preprocesing:
      Run: 1_preprocess_data.ipynb   (ONLY NEED TO DO THIS ONCE!)
    #### 3. Train model on Cityscapes:
      Run: 2_train.ipynb
    #### 4. Evaluation
    1. Run: evaluation/eval_on_val.ipynb
  This will run the pretrained model on all images in Cityscapes val, compute and print the loss, and save the predicted segmentation images in deeplabv3/training_logs/model_eval_val.
