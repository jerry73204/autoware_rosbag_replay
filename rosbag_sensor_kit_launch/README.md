# rosbag_sensor_kit_launch

Custom sensor kit for the Autoware [rosbag replay simulation tutorial](https://autowarefoundation.github.io/autoware-documentation/main/demos/rosbag-replay-simulation/).

## Why This Exists

The sample rosbag from the tutorial contains only **3 LiDARs** (top, left, right), but `sample_sensor_kit` expects **4 LiDARs** (including rear). This package provides a sensor configuration matching the actual rosbag data.

## Differences from sample_sensor_kit

| Component | sample_sensor_kit          | rosbag_sensor_kit                     |
|-----------|----------------------------|---------------------------------------|
| LiDARs    | 4 (top, left, right, rear) | 3 (top, left, right)                  |
| IMU       | tamagawa                   | Same (delegates to sample_sensor_kit) |
| GNSS      | ublox                      | Same (delegates to sample_sensor_kit) |

### Modified Files

Based on `sample_sensor_kit_launch` from Autoware 1.5.0 with these changes:

- `config/concatenate_and_time_sync_node.param.yaml`: 3 lidar topics instead of 4
- `launch/lidar.launch.xml`: Removed rear LiDAR definition
- `launch/pointcloud_preprocessor.launch.py`: Points to local config file
- `launch/sensing.launch.xml`: Includes IMU/GNSS from `sample_sensor_kit_launch`

## Usage

Set `sensor_model:=rosbag_sensor_kit` when launching:

```bash
ros2 launch autoware_launch logging_simulator.launch.xml \
  sensor_model:=rosbag_sensor_kit \
  ...
```

## Related Packages

- `rosbag_sensor_kit_description`: URDF/calibration files for this sensor kit
- `individual_params/config/default/rosbag_sensor_kit/`: Sensor calibration parameters
