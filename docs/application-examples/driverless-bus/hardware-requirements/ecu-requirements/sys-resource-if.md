# System Resource & Interface

This is a draft version.

## Overview

The following tables describe the required system resource and interface for each computing unit.

## Main Autoware Unit

| Category           | Item                          | Requirement                                      |
| :----------------- | :---------------------------- | :----------------------------------------------- |
| Computing Resource | CPU                           | X86 8core/16thread @3.3GHz or more               |
|                    | Memory                        | Dual 16GB (Total 32GB), DDR4-2666 w/ ECC or more |
|                    | GPU                           | 9.4 TFLOPS@FP32 or more                          |
|                    | Storage                       | 256GB for System Volume<br>2TB for Logging data  |
|                    | LiDAR                         | 100BASE-TX, 1000BASE-T                           |
| Interfaces         | IMU                           | CAN or RS232C                                    |
|                    | GNSS                          | 100BASE-TX                                       |
|                    | Vehicle                       | CAN                                              |
|                    | Inter-ECU (2D Perception/TLR) | 1000BASE-T                                       |
| Power              | CPU                           | TDP 80 W                                         |
|                    | GPU                           | TDP 110 W                                        |
|                    | Total                         | Max 250 W                                        |

## 2D Perception Unit

This table shows requirements for one camera. For multiple camera configurations, it requires more hardware units. If the hardware unit has sufficient system resource and performance, it can be integrated on a single hardware unit.

| Category           | Item                      | Requirement                                                                        |
| ------------------ | :------------------------ | :--------------------------------------------------------------------------------- |
| Computing Resource | CPU                       | Arm v8.2 8core @2.26GHz or more                                                    |
|                    | Memory                    | 32GB Low-Power Double Data Rate 4x or more                                         |
|                    | GPU                       | 30 TOPS or more                                                                    |
|                    | Storage                   | 32GB or more                                                                       |
| Interfaces         | Camera                    | Gigabit Multimedia Serial Link 2 w/ frame sync trigger or 1000BASE-T (GigE Vision) |
|                    | Inter-ECU (Main Autoware) | 1000BASE-T                                                                         |
| Power              | CPU                       | TDP xxxW                                                                           |
|                    | GPU                       | TDP xxxW                                                                           |
|                    | Total                     | Max.xxxW                                                                           |

## Traffic Light Recognition Unit

This table shows requirements for one camera. For multiple camera configurations, it requires more hardware units. If the hardware unit has sufficient system resource and performance, it can be integrated on a single hardware unit.

| Category           | Item                      | Requirement                                                                        |
| ------------------ | :------------------------ | :--------------------------------------------------------------------------------- |
| Computing Resource | CPU                       | Arm v8.2 8core @2.26GHz or more                                                    |
|                    | Memory                    | 32GB Low-Power Double Data Rate 4x or more                                         |
|                    | GPU                       | 30 TOPS or more                                                                    |
|                    | Storage                   | 32GB or more                                                                       |
| Interfaces         | Camera                    | Gigabit Multimedia Serial Link 2 w/ frame sync trigger or 1000BASE-T (GigE Vision) |
|                    | Inter-ECU (Main Autoware) | 1000BASE-T                                                                         |
| Power              | CPU                       | TDP xxxW                                                                           |
|                    | GPU                       | TDP xxxW                                                                           |
|                    | Total                     | Max.xxxW                                                                           |
