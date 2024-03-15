# TFM 2024 URJC Visión Artificial - Rebeca Villarraso

# Week 0
- TFM proposal study: development of a robot's perception in unstructured environments.
- Work planning:
  1. Contact Goose dataset developers to find out data availability. Study dataset structure.
  2. Obtain RELLIS-3D dataset and know its structure.
  3. Develop semantic segmentation algorithm for testing.
  4. Study other data sets (RUGD, FIRE, CITYSCAPES).
 
# Week 1
- DeepLabV3+ semantic segmentation with "instance-level_human_parsing" dataset.
  (DeepLabV3+ is a ResNet50 pretrained model variation based on enconder-decoder blocks).
- RELLIS-3D (a Multi-modal Dataset for Off-Road Robotics) (images and LIDAR) obtained and preprocessed from: https://gamma.umd.edu/publication.
- Reproduction of Ga-Nav Sematic Segmentation of Rellis-3D Images according to: https://github.com/unmannedlab/RELLIS-3D
- On going: adaptation the DeepLabV3+ model to train RELLIS-3D dataset.
- Work planning:
  1. Continue adapting DeepLabV3+ with the RELLIS-3D and RUGD datasets.
  2. GitHub Pages.
  3. Study the metrics and models proposed on the Cityscapes dataset website: https://www.cityscapes-dataset.com/benchmarks/
