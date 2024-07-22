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
### 3. Edit package.xml

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
```

### 4. Build the Package
```bash
# Navigate to your ROS 2 workspace
cd ~/ros2_ws

# Build the packages
colcon build
```

### 5. Start the URDF File

Create the URDF file and necessary folders.
```bash
# Create folders for URDF and meshes
mkdir -p ~/ros2_ws/src/mycobot_ros2/mycobot_description/urdf/
mkdir -p ~/ros2_ws/src/mycobot_ros2/mycobot_description/meshes/mycobot_280/
```
Download and prepare mesh files for the robotic arm.

```bash
# Navigate to the directory where mesh files are stored
cd ~/Downloads/mycobot_ros/mycobot_description/urdf/280_arduino/

# Rename and copy mesh files
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install rename

rename 's/joint/link/' *.dae
rename 's/joint/link/' *.png

# Copy mesh files to your ROS 2 workspace
cp *.dae *.png ~/ros2_ws/src/mycobot_ros2/mycobot_description/meshes/mycobot_280/
```

Adjust file names in the mesh files as necessary.
### 6. Create mycobot_280_urdf.xacro

Navigate to the directory where we create the mycobot_280_urdf.xacro file:
```bash
cd ~/ros2_ws/src/mycobot_ros2/mycobot_description/urdf/
```
Now, create the mycobot_280_urdf.xacro file using your preferred text editor.

### 7. Configure CMakeLists.txt

Modify CMakeLists.txt for the mycobot_description package.

### 8. Build the Package

```bash
# Navigate to your ROS 2 workspace
cd ~/ros2_ws

# Build the packages
colcon build

# Source your setup.bash to set up the environment for the new package
source ~/.bashrc
```

### 9. Visualize the URDF File in RViz

![opening window](https://github.com/maduwanthasl/Model-a-Robotic-Arm-Ros2/blob/main/Images/opened%20view.png)

To visualize the URDF file in RViz, follow these steps:
```bash
# Install the necessary ROS 2 package for URDF visualization in RViz
sudo apt-get install ros2-urdf-tutorial

# Launch RViz with your URDF model
ros2 launch urdf_tutorial display.launch.py model:=/home/destro_username/ros2_ws/src/mycobot_ros2/mycobot_description/urdf/mycobot_280_urdf.xacro
```
### 10. Exploring in RViz
[final outcome.mp4](https://github.com/maduwanthasl/Model-a-Robotic-Arm-Ros2/blob/main/Modeled%20Arm.mp4)
- Axis Convention: By convention, the red axis represents the x-axis, the green axis represents the y-axis, and the blue axis represents the z-axis.
- Using Joint State Publisher: Utilize the Joint State Publisher GUI to interactively move the robotic arm links.
- Customizing Display: Experiment with different display options under the "Displays" panel on the left of RViz.

These steps will help you visualize and interact with your MyCobot 280 robotic arm model in RViz within your ROS 2 environment.

### 11. Generate Frames PDF

![frames](https://github.com/maduwanthasl/Model-a-Robotic-Arm-Ros2/blob/main/Images/frames.png)

To view the coordinate frames, generate and open the frames PDF:
```bash
# Generate the frames PDF
ros2 run tf2_tools view_frames

# Open the PDF file in Evince or navigate to your home folder to locate it
evince frames.pdf
```
These steps will help you visualize your MyCobot 280 robotic arm model in RViz and understand its coordinate frames using the frames PDF generated by tf2_tools.

## Reference

- This project was based on the tutorial from [Automatic Addison](https://github.com/automaticaddison/mycobot_ros2).

