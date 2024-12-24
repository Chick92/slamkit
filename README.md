# README #

Recon2 repository. 

This will eventually have a dockerfile and coker-compose.yaml file for ease of deployment. 

### permissions ###

The radeye needs access to the dialout group as its a serial device - 

sudo usermod -a -G dialout <username>

### Building in a catkin workspace ###


Some stuff that's required (this is lifted from a dockerfile i've been using accross multiple instances, some of this may not strictluy be needed or already installed on your machine) - 

pip3 install pyyaml rospkg
pip3 install pillow #also needed and not installed on ARM by default, but is on AMD64....
sudo apt-get install -y iputils-ping #THIS IS NEEDED BYTHE DRIVER BUT ISN'T MENTIONED ANYWHERE IN THE API
sudo apt-get install ffmpeg libsm6 libxext6  -y
sudo apt-get install ros-noetic-tf2* -y
sudo apt-get install ros-noetic-tf* -y
sudo apt-get install ros-noetic-interactive-markers -y
sudo apt-get install ros-noetic-pcl-conversions -y
sudo apt-get install ros-noetic-pcl-ros* -y
sudo apt-get install ros-noetic-laser-geometry* -y
sudo apt-get install ros-noetic-diagnostic-updater -y



ros_leica requires steps to install the underlying driver - 

The reason we're still using datastore when the V0.8.0 driver has some pointcloud accumulation stuff, is because the datastore compatible version is more stable as it's had more work put into it, and the none datastore version utilises open3d quite heavily. Open3d will likely install on all machines 9not had any issues with the install) but depending on the processor, your machine may not have a particular instruction which open3d relies on. you can build it from source with comiler flage, but this seemed like a lot of work for no gain.

Virtual envrionement - (This is the instructions for the older API, but it's largely the same. I think the path is just different. If it's not superuser, it's not worth doing so I have no course to test......)

* In the project root directory, set up a virtual environment with `python3.9 -m venv venv`, and source with `source venv/bin/activate` (you can also replace `venv` with the virtual environment name of your choice)
* Navigate to the [BLKARC API dependency]( ./deps/leica_blk/deps/BLKARC-Module-API_0.7.0/) and run the setup script with `./src/blk_arc_api/install.sh`
* Navigate to the [setup](./src/setup) directory and run the setup script [here](src/setup/setup_dependencies.sh)
* Go to the root of your Catkin workspace and build with `catkin_make -DCMAKE_BUILD_TYPE=Release`

system wide - 

* navigate to the 0.8 API - ros_leica/deps/leica_api/Leica_BLKARC-Module-API_v0.8.0
* python3 -m pip install -r requirements.txt
* navigate to src/ros_leica/deps/leica_blk/deps/leica_api/Leica_BLKARC-Module-API_v0.8.0/src/python_sample_wrapper/
* ./install.sh (maybe sudo it for a laugh.)

pip3 install deps/leica_blk/src/modules

* navigate back to catkin_ws and it should build.



### What is this repository for? ###


This repo hosts everything needed to get recon2 up and running. It will also be the basis for Alphabot, as that's pretty kuch recon2 but with a spot driver and some static transform publishers. 


### How do I get set up? ###

To do...

### Contribution guidelines ###

Update the readme!

### Who do I talk to? ###

Dr. Benjamin Bird# slamkit
