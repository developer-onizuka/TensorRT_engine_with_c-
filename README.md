# 1. docker run
```
# xhost +; sudo docker run --gpus all -it --rm -v /mnt/docker/tlt-experiments:/workspace/tlt-experiments -v /tmp/.X11-unix:/tmp/.X11-unix --device /dev/video0:/dev/video0:mwr -e DISPLAY=$DISPLAY -p 8888:8888 nvcr.io/nvidia/tlt-streamanalytics:v3.0-dp-py3 /bin/bash
```

# 2. preparing for webcamera
see also https://github.com/developer-onizuka/webcamera.
```
----- in the container -----
root@52b289cd78c4:/workspace# export QT_X11_NO_MITSHM=1
```

# 3. install opencv3
see also https://github.com/developer-onizuka/install_opencv_3.x.
```
# dpkg -l | grep opencv
# sudo apt-get update
# sudo apt -y install libopencv-dev opencv-data
# sudo apt -y install libopencv-dev opencv-data --fix-missing
```



