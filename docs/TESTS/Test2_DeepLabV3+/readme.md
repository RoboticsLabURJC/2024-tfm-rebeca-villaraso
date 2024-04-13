## TEST 2. DeepLabV3+ Semantic segmentation om Cityscapes dataset
- Dataset: Cityscapes https://www.cityscapes-dataset.com/
- Documentation: https://arxiv.org/abs/1811.12596
- Based on: https://github.com/fregu856/deeplabv3
- Jupyter Notebook Developed: see the following sections

------------------------------------------

#### 1. Pretrained model:
      pretrained_models/model_13_2_2_2_epoch_580.pth: Trained for 580 epochs on Cityscapes train and 3333 + 745 images from Berkeley DeepDrive.
---
#### 2. Dataset preprocesing:
      Run: 1_preprocess_data.ipynb   (ONLY NEED TO DO THIS ONCE!)
---
#### 3. Train model on Cityscapes:
      Run: 2_train.ipynb
---
#### 4. Evaluation
##### eval_on_val
      Run: 3_eval_on_val.ipynb
This will run the pretrained model on all images in Cityscapes val, compute and print the loss, and save the predicted segmentation images in deeplabv3/training_logs/model_eval_val.

##### eval_on_val_for_metrics
      Run: 4_eval_on_val_for_metrics.ipynb
This will run the pretrained model on all images in Cityscapes val, upsample the predicted segmentation images to the original Cityscapes image size (1024, 2048), and compute and print performance metrics

---
#### 5. Visualization
##### run_on_seq
      Run: 5_run_on_seq.ipynb
This will run the pretrained model (set on line 33 in run_on_seq.py) on all images in the Cityscapes demo sequences (stuttgart_00, stuttgart_01 and stuttgart_02) and create a visualization video for each sequence, which is saved to deeplabv3/training_logs/model_eval_seq. See Youtube video: https://www.youtube.com/watch?v=9e2x4dDRB-k&feature=youtu.be&themeRefresh=1

##### run_on_thn_seq
      Run: 6run_on_thn_seq.ipynb
This will run the pretrained model (set on line 31 in run_on_thn_seq.py) on all images in the Thn sequence (real-life sequence collected with a standard dash cam) and create a visualization video, which is saved to deeplabv3/training_logs/model_eval_seq_thn. See Youtube video:  https://www.youtube.com/watch?v=9e2x4dDRB-k&feature=youtu.be&themeRefresh=1
