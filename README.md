# One-click installation (forgot to ask for Star, click before leaving~)

>### The tools you want can be found in [Wish List] (https://github.com/fishros/install/issues/2 ) Proposed in, maybe there will be a magician to fulfill your wish

## Tool list

List of supported tools：

-One-click installation: ROS (support ROS and ROS2, Raspberry Pi Jetson) [contribution@Xiaoyu] (https://github.com/fishros )
-One-click installation: VSCode (supports amd64 and arm64) [contribution@Xiaoyu] (https://github.com/fishros )
-One-click installation: github desktop version (Xiaoyu's commonly used github client) [contribute @Xiaoyu] (https://github.com/fishros )
-One-click installation: nodejs development environment (you can preview Xiaoyu's official website through nodejs) [contribution@Xiaoyu] (https://github.com/fishros )
-One-click configuration: rosdep (Xiaoyu's rosdepc, fast and easy to use) [contribution @Xiaoyu] (https://github.com/fishros )
-One-click configuration: ROS environment (quickly update ROS environment settings, automatically generate environment selection) [Contribution@Xiaoyu] (https://github.com/fishros )
-One-click configuration: system source (replace the system source, support the full version of Ubuntu system) [Contribution @Xiaoyu] (https://github.com/fishros )
-One-click installation: Docker (supports amd64 and arm64) [contribution @alyssa] (https://github.com/alyssa1024 )
-One-click installation: cartographer contribution [@Xiaoyu] (https://github.com/fishros ) & [@Catalpa](https://github.com/Y-zi )
-One-click installation: WeChat client [contribution@Xiaoyu] (https://github.com/fishros )



## How to use
```
wget http://fishros.com/install -O fishros && . fishros
```

## How to automatically select (used in Dockerfile)

Currently, one-click installation supports automatic input options from the configuration file. You need to manually run one-click installation at a time. After using it,`/tmp/fish_install.yaml`.

Use the following command to copy the configuration file to the current terminal.

```
cp /tmp/fish_install.yaml ./
```

## Used in # Dockerfile

Examples of use are as follows

```
RUN apt update \ 
    && apt install wget python3-yaml -y  \
    # Install melodic
    && echo "chooses:\n" > fish_install.yaml \
    &&echo"-{choose: 1, desc:'one-click installation: ROS (support ROS and ROS2, Raspberry Pi Jetson)'}\n">>fish_install.yaml \
    &&echo"-{choose: 1, desc: replace the source and continue the installation}\n">>fish_install.yaml \
    && echo"-{choose: 2, desc: clean up the three sources}\n">> fish_install.yaml \
    && echo "- {choose: 1, desc: melodic(ROS1)}\n" >> fish_install.yaml \
    &&echo"-{choose: 1, desc: melodic(ROS1) Desktop Version}\n">>fish_install.yaml \
    && wget http://fishros.com/install  -O fishros && /bin/bash fishros \
    # Perform the final cleanup
    && rm -rf /var/lib/apt/lists/*  /tmp/* /var/tmp/* \
    && apt-get clean && apt autoclean 
```
One-click source change

```
FROM ubuntu:22.04

# One-click source change
RUN apt update \
    && apt install wget python3 python3-yaml -y python3-distro\
    && echo "chooses:\n" > fish_install.yaml \
    &&echo"-{choose: 5, desc:'one-click installation: ROS (support ROS and ROS2, Raspberry Pi Jetson)'}\n">>fish_install.yaml \
    &&echo"-{choose: 2, desc: replace the source and continue the installation}\n">>fish_install.yaml \
    && echo"-{choose: 1, desc: clean up the three sources}\n">> fish_install.yaml \
    && wget http://fishros.com/install  -O fishros && /bin/bash fishros \
    # Perform the final cleanup
    && rm -rf fish_install.yaml \
    && rm -rf /var/lib/apt/lists/*  /tmp/* /var/tmp/* \
    && apt-get clean && apt autoclean 
```

## Contribution Guide

If you want to turn your common installation program into a one-click installation program, you can follow the contribution guide below.

### 1.fork project

Fork the project to your github, then clone the project locally

### 2.New file

Create a new py file in the tools directory of the local project

-If the installation tool is named:tool_install_xxx.py
- If the configuration tool is:tool_config_xxx.py

### 3.Write a program

Copy the template to your newly created file：

```
# -*- coding: utf-8 -*-
from .base import BaseTool
from .base import PrintUtils,CmdTask,FileUtils,AptUtils,ChooseTask
from .base import osversion
from .base import run_tool_file

class Tool(BaseTool):
    def __init__(self):
        self.type = BaseTool.TYPE_INSTALL
        self.name = "Template Project"
        self.author='Xiaoyu'

    def run(self):
        #Formal operation
        pass
```

Then modify the type, name, and author

Write logic in the run function, the tools that can be provided to you are：
1. PrintUtils print text
2. FileUtils operation file
3. AptUtils operation Apt
4. ChooseTask selection options
5. CmdTask runs the command line tool
6. run_tool_file to run other tools (need to install.Configure dep in py's tools)

information：
1. osversion system related information
2. osarch architecture information amd64/i386/arm

### 4.in install.Add a message to tools in py

### 5.Run the test


## Contribution list

-One-click installation of ROS [Xiaoyu] (https://github.com/fishros )
-One-click installation of github-deskto [Xiaoyu] (https://github.com/fishros )
-One-click configuration of rosdep [Xiaoyu] (https://github.com/fishros )
-One-click configuration of ros environment [Xiaoyu] (https://github.com/fishros )
-One-click configuration of system source [Xiaoyu] (https://github.com/fishros )
-One-click installation of nodejs [Xiaoyu] (https://github.com/fishros )
-One-click installation of vscode [Xiaoyu] (https://github.com/fishros )
-One-click installation: Docker (supports amd64 and arm64) [@alyssa] (https://github.com/alyssa1024 )
