# Indoor Drone Simulation

This project simulates an indoor drone using ROS, MAVROS, and Gazebo. It includes SLAM capabilities using RTAB-Map and autonomous navigation with custom `explore.launch` parameters.

## Features

- Indoor drone simulation with Gazebo
- Real-time SLAM using RTAB-Map
- Autonomous navigation with ROS explore package
- Customizable parameters for various environments

## Prerequisites

Before you begin, ensure you have met the following requirements:

- Docker installed on your machine using apt
- Install [nvidia-container-runtime](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) on your machine
- Git installed on your machine
- Ubuntu 20.04 recommended

## Installation

Follow these steps to set up the project locally:

1. Clone the repository:
   ```bash
   git clone https://github.com/mkuser608/AI-indoor-drone-sim.git
   cd indoor_autonomous_drone_simulation
2. Build the docker image:
   ```bash
   docker build -t indoor_autonomous_drone_simulation -f docker/Dockerfile .
   ```
   if the build appears to have crashed or stuck, reboot your machine and try running with a limit on memory usage
   ```bash
    docker build -m 2048m -t indoor_autonomous_drone_simulation -f docker/Dockerfile .
   ```
   
3. Run the simulation with the following commands: (Nvidia required, superuser required)
   ```bash
	./gazebo.sh       # Launch Gazebo environment
	./slam.sh         # Initialize RTAB-Map for SLAM
	./rviz.sh         # Open RViz for visualization
	./offboard.sh     # Start offboard control
	./explore.sh      # Initiate autonomous exploration
## Modification of Parameters

### Drone Motion Parameters:

Parameters related to the motion of the drone can be changed via: <br>
File: `/param/base_local_planner_params.yaml`

### Autonomous Exploration Parameters:
File: `/launch/explore.launch`

- **map_topic**: Topic for the occupancy grid map. Default: `/rtabmap/grid_map`.
- **odom_topic**: Topic for odometry data. Default: `/rtabmap/odom`.
- **costmap_topic**: Topic for the costmap. Default: `/rtabmap/grid_map`.
- **robot_base_frame**: Frame ID of the robot's base. Default: `base_link`.
- **planner_frequency**: Planner update frequency (Hz). Default: `0.07` (Range: `0.01-1.0`).
- **visualize**: Enable/disable RViz visualization. Default: `true` (Values: `true/false`).
- **min_frontier_size**: Minimum size of unexplored areas. Default: `1` (Range: `0.5-5.0`).
- **transform_tolerance**: Tolerance for transform lookups (s). Default: `0.7` (Range: `0.1-1.0`).
- **gain_scale**: Exploration gain factor. Default: `1` (Range: `0.5-10.0`).
- **progress_timeout**: Time to wait for progress (s). Default: `10` (Range: `5-60`).



	


