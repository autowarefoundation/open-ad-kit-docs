# Performance and Data Bandwidth Requirements

This is a draft version.

## Overview

This page describes required performance for the perception accelerators and data bandwidth on each sensor interface and network.

## Perception Accelerators

| Functions                 | Network Model                                                      | Input resolution @ frame rate                              | Required performance |
| :------------------------ | :----------------------------------------------------------------- | :--------------------------------------------------------- | -------------------- |
| 3D Perception             | CenterPoint                                                        | 55000 voxels x 20 points x 10<br>features @10FPS per LiDAR | XX TOPS              |
| 2D Perception             | Yolov4                                                             | 608x608@10FPS per Camera                                   | XX TOPS              |
| Traffic Light Recognition | MobileNet v2 SSD Lite (Detection)<br>MobileNet v2 (Classification) | 300x300@10FPS<br>224x224@10FPS                             | XX TOPS              |

## Data Bandwidth

| Type            | Configurations                                                                                                                                                                         | Data type                                                 | Data Bandwidth |
| :-------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------- | -------------- |
| LiDAR Input     | Mid-range                                                                                                                                                                              | Point cloud                                               | 37 Mbps        |
|                 | Short-range                                                                                                                                                                            | Point cloud                                               | 26 Mbps        |
| Camera Input    | Perception Camera                                                                                                                                                                      | YUV422 16bit<br>1920x1280                                 | 393 Mbps       |
|                 | Traffic Light Recognition Camera                                                                                                                                                       | YUV422 16bit<br>2880x1860                                 | 857 Mbps       |
| Inter-ECU       | 2D Perception to Main Autoware                                                                                                                                                         | Recognition result &<br>Compressed image data for logging | 27 Mbps        |
|                 | TLR to Main Autoware                                                                                                                                                                   | Recognition result &<br>Compressed image data for logging | 59 Mbps        |
| Logging Storage | Mid-range LiDAR x 4<br>Short-range LiDAR x 4<br>Perception Camera x 6 (Compressed)<br>Traffic Light Recognition Camera x 1 (Compressed)<br>Main Autoware internat topics (272Mbps)<br> |                                                           | 745 Mbps       |
