Dataset Structure
All ROS bags in the GOOSE DB are organized in the hierarchical structure of setup, scenario and sequence. This hierarchy allows users to filter the recorded ROS bags according to their needs. The hiearachy levels are defined in the following way:

A setup describes a robotic platform with its sensor suite. The sensor setup remains consistent among all scenarios within the same setup. When the position and combination of sensors are changed on the same robotic platform, then the recordings done from there on should be grouped in a new setup.
A scenario contains all data recorded in the same measurement run. Global conditions like the weather and the amount of dynamic objects in the scene remain consistent among all sequences in the scenario.
A sequence corresponds to one ROS bag and includes a YAML file with metadata. The recording length of each sequence varies as well as the number of annotated frames in a sequence. Each sequence is categorized into one scenario and setup.
The directory tree of the GOOSE dataset could look at follows.

├── setups
    ├── mucar3
    ├── metadata.yml
    │   ├── scenario01
    │   │   ├── metadata.yml
    │   │   ├── sequence01
    │   │   │   ├── 2adccef9-e281-4a47-9ade-16e49efa4007.bag
    │   │   │   └── metadata.yml
    │   │   ├── sequence02
    │   │   │   ├── 3e1edb48-5f18-48e8-a86d-11351fdb9d0c.bag
    │   │   │   └── metadata.yml
    │   │   ├── sequence03
    │   │   │   ├── b142123d-9c9b-46ce-8c02-5cd407dc9712.bag
    │   │   │   └── metadata.yml
    │   ├── scenario02
    │   │   ├── metadata.yml
    │   │   ├── sequence03
    │   │   │   ├── 901b5784-8a23-42d7-8dcd-e0fc9c28bd53.bag
    │   │   │   └── metadata.yml
In addition, we provide ready-to-use-data for typical deep learning pipelines as described in the following sections.

2D Image Annotations
The directory tree for the image dataset is as follows:

├── goose_label_mapping.csv
├── images
│   ├── test
│   │   ├── 2022-07-07_campus
│   │   ├── ...
│   │   └── 2023-07-03_campus
│   ├── train
│   │   ├── 2022-07-22_touareg_flight
│   │   ├── ...
│   │   └── 2023-05-24_touareg_neubiberg_cloudy
│   └── val
│       ├── 2022-07-22_flight
│       ├── ...
│       └── 2023-05-17_neubiberg_sunny
└── labels
    ├── test
    │   ├── 2022-07-07_campus
    │   ├── ...
    │   └── 2023-07-03_campus
    ├── train
    │   ├── 2022-07-22_touareg_flight
    │   ├── ...
    │   └── 2023-05-24_touareg_neubiberg_cloudy
    └── val
        ├── 2022-07-22_flight
        ├── ...
        └── 2023-05-17_neubiberg_sunny
The ìmages directory contains one image per scene:

<date>_<title>_<framenumber>_<timestamp>_windshield_vis.png (RGB input Image)
In each of the folders in the labels directory, there are 3 files for each frame, named as follows:

<date>_<title>_<framenumber>_<timestamp>_color.png (RGB Image)
<date>_<title>_<framenumber>_<timestamp>_labelids.png (Class Labels)
<date>_<title>_<framenumber>_<timestamp>_instanceids.png (Instance Labels)
See our experiment section for an example on how to read the data.

3D Point Cloud Annotations
The directory tree for the point cloud dataset is as follows:

├── goose_label_mapping.csv
├── velodyne
│   ├── test
│   │   ├── 2022-07-07_campus
│   │   ├── ...
│   │   └── 2023-07-03_campus
│   ├── train
│   │   ├── 2022-07-22_touareg_flight
│   │   ├── ...
│   │   └── 2023-05-24_touareg_neubiberg_cloudy
│   └── val
│       ├── 2022-07-22_flight
│       ├── ...
│       └── 2023-05-17_neubiberg_sunny
└── labels
    ├── test
    │   ├── 2022-07-07_campus
    │   ├── ...
    │   └── 2023-07-03_campus
    ├── train
    │   ├── 2022-07-22_touareg_flight
    │   ├── ...
    │   └── 2023-05-24_touareg_neubiberg_cloudy
    └── val
        ├── 2022-07-22_flight
        ├── ...
        └── 2023-05-17_neubiberg_sunny
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
