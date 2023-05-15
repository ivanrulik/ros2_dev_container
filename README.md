# ROS 2 Dev Container
## Introduction
This project is based on the ROS 2 VS Code template developed by @athackst. As a reference here is the [original readme file ](docs/ref_README.md)</p>

## Objectives
Test and make this container work on mac os without any compromises

## Setup (Mac OS)
### GUI bridge
1. Install [XQuartz]( https://www.xquartz.org/)</p>
(optional) run `brew install --cask xquartz`
2. Enable X11 connections from localhost
   ```bash
   xhost +localhost
   ```
3. Modify the line `"DISPLAY": "${localEnv:0}"` on [.devcontainer/devcontainer.json](/.devcontainer/devcontainer.json)
4. Now the container based GUI apps will open under XQuartz

### VS Code container setup
1. Clone this repo:
   ```bash
   git clone https://github.com/ivanrulik/ros2_dev_container.git
   ```
2. Go to the File menu of VS Code and open the project folder
3. Press `Ctrl+P` or `Cmd+P` and type `>Dev Containers: Open Folder in Container...
4. After the image and container have been built VS code should show 
<p align="center">
  <img src="docs/figs/vs_dev_check.png", style="width: 170px;">
  <br>
  <b>Figure: Dev Container Indicator</b>
</p>

## Common Errors
Here is a detailed list of common error encountered while working on this project [READ](docs/errors.md)
