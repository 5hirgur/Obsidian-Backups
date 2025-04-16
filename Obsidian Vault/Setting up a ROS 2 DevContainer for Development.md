#programming #linux #robotics 

# What is a DevContainer?

A **DevContainer** is a Docker-based isolated development environment.  
You define it with:

- A **Dockerfile** (to build the environment)
    
- A **`devcontainer.json`** (to connect it to VSCode)
    

When you open your project in VSCode, it **automatically builds and runs** your container, mounts your project, and sets up your tools.

Perfect for ROS 2 projects: no polluting your system, easy GUI, and repeatable builds.

# Why Use a DevContainer for ROS 2 Jazzy?

- Isolated and reproducible ROS 2 environment
    
-  No clutter on your local system
    
-  Runs ROS 2 Jazzy (Ubuntu Noble) even if your host is Ubuntu 22.04
    
-  GUI support (RViz2, MoveIt)
    
-  Ready for VSCode extensions and debugging

# Project Structure 

```css 
my-ros2-project/
├── .devcontainer/
│   ├── Dockerfile
│   └── devcontainer.json
├── src/
├── README.md
``` 

The Dockerfile (pulled form DockerHub):
```dockerfile
# This is an auto generated Dockerfile for ros:ros-base

# generated from docker_images_ros2/create_ros_image.Dockerfile.em

FROM ros:jazzy-ros-core-noble

  

# install bootstrap tools

RUN apt-get update && apt-get install --no-install-recommends -y \

build-essential \

git \

python3-colcon-common-extensions \

python3-colcon-mixin \

python3-rosdep \

python3-vcstool \

&& rm -rf /var/lib/apt/lists/*

  

# bootstrap rosdep

RUN rosdep init && \

rosdep update --rosdistro $ROS_DISTRO

  

# setup colcon mixin and metadata

RUN colcon mixin add default \

https://raw.githubusercontent.com/colcon/colcon-mixin-repository/master/index.yaml && \

colcon mixin update && \

colcon metadata add default \

https://raw.githubusercontent.com/colcon/colcon-metadata-repository/master/index.yaml && \

colcon metadata update

  

# install ros2 packages

RUN apt-get update && apt-get install -y --no-install-recommends \

ros-jazzy-ros-base=0.11.0-1* \

&& rm -rf /var/lib/apt/lists/*
```

devcontainer.json:
```json
{

"name": "ROS 2 Jazzy Full DevContainer",

"build": {

"dockerfile": "Dockerfile"

},

"customizations": {

"vscode": {

"extensions": [

"ms-iot.vscode-ros",

"ms-python.python",

"ms-vscode.cpptools"

],

"settings": {

"terminal.integrated.shell.linux": "/bin/bash"

}

}

},

"postCreateCommand": "rosdep update",

"mounts": [

"source=${localWorkspaceFolder},target=/workspace,type=bind"

],

"workspaceFolder": "/workspace",

"runArgs": [

"--net=host",

"-e", "DISPLAY=${env:DISPLAY}",

"-v", "/tmp/.X11-unix:/tmp/.X11-unix"

]

}
```

