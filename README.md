The following steps are not only for Jetson but also workstations with Quadoro.

My hardware is
```
   (1) Optiplex 3050SFF  ... JPY 19,250
       Intel(R) Core(TM) i3-7100 CPU @ 3.90GHz
       DIMM slot1: DDR4 DIMM 4GB (Hynix)
       DIMM slot2: Empty
       HDD 500GB  ---> replace to SATA SSD(Windows10 pro)
       DVD DRIVE  ---> replace to SATA SSD(Ubuntu 20.04)
   (2) SATA SSD  ... JPY 2,000
       Transcend SSD 120GB
       P/N: TS120GSSD220S
   (3) Wifi 11n ... JPY 800
       P/N: WDC-150SU2MWH
   (4) DDR4 DIMM 4GB ... JPY 2,280
       Patriot Memory DDR4 2400MHz PC4-19200
       P/N: PSD44F24082
   (5) NVMe SSD ... JPY 3,980
       KLEVV SSD 256GB CRAS C710 M.2 Type2280 PCIe3x4 NVMe 3D TLC NAND Flash
       P/N: K256GM2SP0-C71
   (6) ETC
       -Sabrent 2.5in->3.5in ... JPY 599
       -Zheino 2nd 9.5mm Note PC drive mounter ... JPY 899
       -GLOTRENDS M.2 Heatsink ... JPY 650
   (7) NVIDIA Quadro P400 (GP107GL) ... JPY 5,948
   ----- Total JPY 36,406 -----
```

see also https://github.com/developer-onizuka/gpudirect_storage.


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
```

You might need the step below:
```
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
# pwd
/workspace/tlt-experiments/sample/Jetson-Edge-Vision-Example/build
# ./app
```
