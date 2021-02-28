# 1. docker run
```
# xhost +; sudo docker run --gpus all -it --rm -v /mnt/docker/tlt-experiments:/workspace/tlt-experiments -v /tmp/.X11-unix:/tmp/.X11-unix --device /dev/video0:/dev/video0:mwr -e DISPLAY=$DISPLAY -p 8888:8888 nvcr.io/nvidia/tlt-streamanalytics:v3.0-dp-py3 /bin/bash
```

# 2. preparing for webcamera
see also https://github.com/developer-onizuka/webcamera.
```
----- in the container -----
# export QT_X11_NO_MITSHM=1
```

# 3. install opencv3
see also https://github.com/developer-onizuka/install_opencv_3.x.
```
----- in the container -----
# dpkg -l | grep opencv
# sudo apt-get update
# sudo apt -y install libopencv-dev opencv-data
# sudo apt -y install libopencv-dev opencv-data --fix-missing
```

# 4. git clone and build
see also https://github.com/fixstars/Jetson-Edge-Vision-Example.
```
----- in the container -----
# pwd
/workspace/tlt-experiments/sample
# git clone https://github.com/fixstars/Jetson-Edge-Vision-Example.git
# cd Jetson-Edge-Vision-Example/
# mkdir build
# cd build/
# cmake ..
# make
# ls
CMakeCache.txt  CMakeFiles  Makefile  app  cmake_install.cmake
```
# 5. copy engine which translated by tlt-converter
see also https://github.com/developer-onizuka/deepstream.
```
# pwd
/workspace/tlt-experiments
# cp -p model/tlt_facedetectir_vpruned_v1.0/resnet18_facedetectir_pruned.engine sample/Jetson-Edge-Vision-Example/build/trt.engine
```

# 6. run
```
# ./app
```
