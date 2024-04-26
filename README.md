# Autonomous Mobile Robot using ROS (noetic) on Ubuntu 20.04

This project focuses on the development of an Autonomous Mobile Robot using ROS (noetic), running on Ubuntu 20.04. The robot is designed to navigate within a simulated hospital environment. The project is divided into three main packages: `robot_description`, `robot_gazebo`, and `robot_navigation`.

## Packages Overview

### [robot_description](src/robot_description)
This package contains the [xacro](http://wiki.ros.org/xacro) files for defining the [robot's components](http://wiki.ros.org/urdf/Tutorials), properties, and [gazebo plugins](https://classic.gazebosim.org/tutorials?tut=ros_gzplugins). These files are essential for describing the robot's physical characteristics and behavior within the simulation environment.

### [robot_gazebo](src/robot_gazebo)
The `robot_gazebo` package utilizes the AWS Robotics provided hospital world simulation environment ([aws-robomaker-hospital-world](https://github.com/aws-robotics/aws-robomaker-hospital-world)) to spawn the robot described in `robot_description` within Gazebo. This package also includes [launch](http://wiki.ros.org/roslaunch) files for setting up and configuring the simulation environment.

### [robot_navigation](src/robot_navigation)
In the `robot_navigation` package, several ROS navigation packages are utilized to enable [autonomous navigation](http://wiki.ros.org/navigation) for the robot within the hospital environment. The process involves:

1. **Mapping:** Using [slam_gmapping](http://wiki.ros.org/gmapping) to generate a map of the hospital environment.
2. **[Localization](https://docs.ros.org/en/melodic/api/robot_localization/html/index.html):** Implementing [AMCL](http://wiki.ros.org/amcl) (Adaptive Monte Carlo Localization) for accurate localization of the robot within the mapped environment.
3. **[Navigation](http://wiki.ros.org/navigation):** Employing [move_base](https://wiki.ros.org/move_base) package for path planning and execution, enabling the robot to navigate autonomously to predefined goals.

## Navigation Parameter Tuning

To ensure optimal navigation performance, various navigation parameters have been tuned. These include:

- **[costmap_common_params](http://wiki.ros.org/costmap_2d):** Parameters governing the configuration of costmaps used for navigation.
- **[dwa_local_planner_params](http://wiki.ros.org/dwa_local_planner?distro=noetic):** Parameters specific to the DWA (Dynamic Window Approach) local planner.
- **global_costmap_params:** Parameters related to the global costmap configuration.
- **[global_planner_params](http://wiki.ros.org/global_planner?distro=noetic):** Parameters for configuring the global planner used by move_base.
- **local_costmap_params:** Parameters specific to the local costmap configuration.
- **[move_base_params](http://wiki.ros.org/move_base?distro=noetic):** Overall parameters governing the behavior of move_base, including recovery behaviors and controller settings.

## Installation and Usage

To utilize this project, follow these steps:
> Note: The building process may take some time to download models for AWS World.

1. Clone the repository:

```bash
git clone https://github.com/your_username/your_project.git
```

2. Navigate to the cloned directory and build the packages:

```bash
cd your_project
catkin_make
```

3. Source the setup file:

```bash
source devel/setup.bash
```

1. Launch simulation environment:

```bash
roslaunch robot_gazebo nomeer_robot.launch
```

5. Launch slam_gmapping to create map:

```bash
roslaunch robot_navigation slam_gmapping.launch
```
6. Launch amcl for localization:

```bash
roslaunch robot_navigation amcl.launch
```

7. Launch the navigation stack:

```bash
roslaunch robot_navigation navigation.launch
```

## Contributing

Contributions to this project are welcome! To contribute, please fork the repository, make your changes, and submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).
