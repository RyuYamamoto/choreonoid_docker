# choreonoid_docker
## How to run
1. install rocker
```
sudo apt install python3-rocker
```
2. build docker image
```
./build choreonoid:noetic Dockerfile
```
3. run docker image
```
./run choreoniod:noetic
```
4. launch choreonoid ros sample
```
roslaunch choreonoid_ros_samples tank.launch
```
