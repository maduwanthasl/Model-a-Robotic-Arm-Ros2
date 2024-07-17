## Introduction

In this project, I modeled the MyCobot 280 robotic arm within a ROS2 workspace. The MyCobot 280 is a lightweight, collaborative robotic arm designed for various applications in research and education. Below, you'll find images of the robotic arm, both in its real-world setup and as modeled in simulation.

### Real Image
![Real Image](https://github.com/maduwanthasl/Model-a-Robotic-Arm-Ros2/blob/main/Images/mycobot%20280.png)

### Modeled Image
![Modeled Image](https://github.com/maduwanthasl/Model-a-Robotic-Arm-Ros2/blob/main/Images/Arm.png)


## Steps Followed

### 1. Create a Package

The first step is to create a ROS 2 package to store all your files.

```bash
# Navigate to your ROS 2 workspace source directory
cd ~/ros2_ws/src

# Create a new folder for the package
mkdir mycobot_ros2

# Navigate into the newly created folder
cd mycobot_ros2

# Create the package where we will store our URDF file
ros2 pkg create --build-type ament_cmake --license BSD-3-Clause mycobot_description

```

### 2. Create a Metapackage

A metapackage is used to group together related packages.
```bash
# Create the metapackage
ros2 pkg create --build-type ament_cmake --license BSD-3-Clause mycobot_ros2

# Navigate into the newly created folder
cd mycobot_ros2

# Remove default src/ and include/ folders if they exist
rm -rf src/ include/

# Edit package.xml to describe your package
gedit package.xml
```
### Edit package.xml

Update package.xml to describe your package.

```xml
<?xml version="1.0"?>
<?xml-model href="http://download.ros.org/schema/package_format3.xsd" schematypens="http://www.w3.org/2001/XMLSchema"?>
<package format="3">
  <name>mycobot_ros2</name>
  <version>0.0.0</version>
  <description>myCobot series robots by Elephant Robotics (metapackage).</description>
  <maintainer email="addyourmail@mail.com">destro_username</maintainer>
  <license>BSD-3-Clause</license>

  <buildtool_depend>ament_cmake</buildtool_depend>

  <exec_depend>mycobot_description</exec_depend>

  <test_depend>ament_lint_auto</test_depend>
  <test_depend>ament_lint_common</test_depend>

  <export>
    <build_type>ament_cmake</build_type>
  </export>
</package>
