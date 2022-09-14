# How to run Autoware

This page explains how to run Autoware on the development platform that are set up in [the Installation chapter](../installation/index.md).

## Minimum requirements

- Developer Platform: TODO
- In-Vehicle Development Platform [^1]: TODO
- Software Tool: TODO
- Container Image: TODO

[^1]: This is optional if you do NOT need a vehicle-edge platform.

## 1. Run Autoware on the developer platform

### Run Autoware.Auto on AVA platform or PCU

1. Open terminal window for each module on you host.

1. Access AVA platform or PCU via SSH in each terminal window.

1. Find docker image id.

```console
docker image ls
REPOSITORY                                    TAG                                                           IMAGE ID       CREATED       SIZE
public.ecr.aws/k7o9k6q7/tier4/autoware.auto   open_ad_kit-autoware-auto-20211111234534-88ea1196cdc0-2zv2o   48a4503b4fe4   11 days ago   6.65GB
```

You can find id such as `48a4503b4fe4`.

1. Launch modules.

   Replace `48a4503b4fe4` with your docker image id.

   **Terminal 1 (map)**

   ```console
   docker run --rm -it --net host -v ~/map:/map -v ~/cyclonedds:/etc/cyclonedds 48a4503b4fe4 /bin/bash -c "export CYCLONEDDS_URI=file:///etc/cyclonedds/cyclonedds.xml; export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp; source install/setup.bash; ros2 launch scenario_simulator_launch autoware_auto_mapping.launch.py map_path:=/map/kashiwanoha"
   ```

   **Terminal 2 (perception)**

   ```console
   docker run --rm -it --net host -v ~/cyclonedds:/etc/cyclonedds 48a4503b4fe4 /bin/bash -c "export CYCLONEDDS_URI=file:///etc/cyclonedds/cyclonedds.xml; export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp; source install/setup.bash; ros2 launch scenario_simulator_launch autoware_auto_perception.launch.py"
   ```

   **Terminal 3 (planning)**

   ```console
   docker run --rm -it --net host -v ~/cyclonedds:/etc/cyclonedds 48a4503b4fe4 /bin/bash -c "export CYCLONEDDS_URI=file:///etc/cyclonedds/cyclonedds.xml; export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp; source install/setup.bash; ros2 launch scenario_simulator_launch autoware_auto_planning.launch.py"
   ```

   **Terminal 4 (vehicle)**

   ```console
   docker run --rm -it --net host -v ~/cyclonedds:/etc/cyclonedds 48a4503b4fe4 /bin/bash -c "export CYCLONEDDS_URI=file:///etc/cyclonedds/cyclonedds.xml; export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp; source install/setup.bash; ros2 launch autoware_auto_launch autoware_auto_vehicle.launch.py"
   ```

## 2. Run Autoware on the in-vehicle development platform

!!! note "If you do NOT need a vehicle-edge platform, please skip this step."

TODO

## 3. Run simulators on the development platform

Please refer to the [How to run simulators](../how-to-run-simulators/index.md) section.
