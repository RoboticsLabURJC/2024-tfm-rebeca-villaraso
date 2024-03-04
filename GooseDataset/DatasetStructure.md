# Pytorch Dataset
The GOOSE Dataset is divided into three subcategories: train, test and validation. The first step is to read the data from the dataset folder.

In the following example this is achieved in two main steps:

Parse images from root folder into (three) python dictionaries with images paths and information.
Create Pytorch Dataset objects to load the images and use them to train models or inference.
Additionally, the dataset also has a mapping CSV File which contains information about the classes such as label id, class name or whether the class has instances or not (thing or stuff).

# Dataset Structure
All ROS bags in the GOOSE DB are organized in the hierarchical structure of setup, scenario and sequence. This hierarchy allows users to filter the recorded ROS bags according to their needs. The hiearachy levels are defined in the following way:

A setup describes a robotic platform with its sensor suite. The sensor setup remains consistent among all scenarios within the same setup. When the position and combination of sensors are changed on the same robotic platform, then the recordings done from there on should be grouped in a new setup.
A scenario contains all data recorded in the same measurement run. Global conditions like the weather and the amount of dynamic objects in the scene remain consistent among all sequences in the scenario.
A sequence corresponds to one ROS bag and includes a YAML file with metadata. The recording length of each sequence varies as well as the number of annotated frames in a sequence. Each sequence is categorized into one scenario and setup.
The directory tree of the GOOSE dataset could look at follows.

![image](https://github.com/RoboticsLabURJC/2024-tfm-rebeca-villaraso/assets/39853010/31b9f559-2182-4f6e-bd09-5ba915dfd229)

In addition, we provide ready-to-use-data for typical deep learning pipelines as described in the following sections.

2D Image Annotations
The directory tree for the image dataset is as follows:

![image](https://github.com/RoboticsLabURJC/2024-tfm-rebeca-villaraso/assets/39853010/bc7069cb-692c-40dc-83c8-1da4af80357a)

The ìmages directory contains one image per scene:

<date>_<title>_<framenumber>_<timestamp>_windshield_vis.png (RGB input Image)
In each of the folders in the labels directory, there are 3 files for each frame, named as follows:

<date>_<title>_<framenumber>_<timestamp>_color.png (RGB Image)
<date>_<title>_<framenumber>_<timestamp>_labelids.png (Class Labels)
<date>_<title>_<framenumber>_<timestamp>_instanceids.png (Instance Labels)
See our experiment section for an example on how to read the data.

3D Point Cloud Annotations
The directory tree for the point cloud dataset is as follows:

![image](https://github.com/RoboticsLabURJC/2024-tfm-rebeca-villaraso/assets/39853010/ee185333-d2a6-4d61-b136-3206bc340102)

The velodyne directory contains one point cloud per scene:

<date>_<title>_<framenumber>_<timestamp>_velodyne.bin (one LiDAR revolution)
In each of the folders in the labels directory, there is one label file:

<date>_<title>_<framenumber>_<timestamp>_velodyne.label (semantic and instance annotations)
The 3D point cloud dataset uses the SemanticKITTI format. The point cluod data can be accessed using the following numpy snippet:

import numpy as np

# reading a .bin file
scan = np.fromfile(filename, dtype=np.float32)
scan = scan.reshape((-1, 4))

# put in attribute
points = scan[:, 0:3]    # get xyz
remissions = scan[:, 3]  # get remission
The data of the .label files can be read in Python using the following numpy code:

import numpy as np

# reading a .label file
label = np.fromfile(filename, dtype=np.uint32)
label = label.reshape((-1))

# extract the semantic and instance label IDs
sem_label = label & 0xFFFF  # semantic label in lower half
inst_label = label >> 16    # instance id in upper half
