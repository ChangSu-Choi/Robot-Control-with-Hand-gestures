# Robot-Control-with-Hand-gestures


This project aims to control excavation equipment and forklifts through hand gestures. The project adapt modern deep learning using hand gesture recognition and implemented tilt pose.
This project has tested on Jetsno NANO with the following environments:
 - python 3.6.9
 - trt_pose 0.0.1
 - Pytorch 1.0.0a0
 - sklearn 0.24.2
 - Jetson Nano Robot library.

The machine recognizes the following hand movements and performs the following functions.  
<details>
 <summary>Movement</summary>
 <div markdown="1">
  1. Fist = Stop<br>
  2. One finger (finger) = left<br>
  3. Palm = Go straight<br>
  4. Two Fingers (V) = Right<br>
  5. Okay = Back up<br>
 </div>
 </details>  
 
![](imgs/run.gif)
![](imgs/backward.jpg)

# co-workers  
- [SangHyun Park](https://parkmaker.github.io/)
- [Jongyeol Na](https://github.com/JongYeolb)

# Topic
- There are many deaths caused by industrial accidents in construction machinery.   
- It is caused by the lack of visibility of internal workers and the inability to look around.   
- It can be safely operated by checking the field of view through the hand motion detection robot control system from the outside and operating heavy equipment.
<img src="https://user-images.githubusercontent.com/77065758/206336403-a47f8949-ccc9-41cb-a192-da5e64474d3e.png"  width="200" height="160"/>


## Related technology
- "Samsung Electronics' All-in-One PC" that recognizes hand movements and works
<img src="https://user-images.githubusercontent.com/77065758/206336409-5f9e5879-4045-40f1-b15a-8c98d7de46c2.jpg"  width="200" height="160"/>

- Amazon AI Secretary Recognizing Sign Language "Alexa"
<img src="https://user-images.githubusercontent.com/77065758/206336405-0f2eb732-3d89-445a-b0ec-84d9551e9187.png"  width="200" height="160"/>

## Introduction to ideas
- Recognizing a person's hand movements through a camera
- Robot control for each movement, and various movements can be customized.





### Application of ideas
- a forklift truck
 - Basic behavior of forklifts
<img src="https://user-images.githubusercontent.com/77065758/206336412-f40b8390-aea4-4b23-88b1-cd1d6e1cc2b1.jpg"  width="200" height="160"/>
  <details>
  <summary>Movement</summary>
  <div markdown="1">
    1. Forward – Backward<br>
    2. Up – Down<br>
    3. In front of tilt – back<br>
  </div>
  </details>
		After matching the basic movements of the forklift with the hand movements, the forklift is controlled with the hand movements

- an excavator
 - How the Excavator Works
<img src="https://user-images.githubusercontent.com/77065758/206336595-c14de783-47d7-410f-9a50-d5371c5761db.png"  width="200" height="160"/>
  <details>
  <summary>Movement</summary>
  <div markdown="1">
   1. Boom Cylinder (Up – Down)<br>
		 2. Handle cylinder (upper – lower)<br>
		 3. Bucket cylinder (upper – lower)<br>
  </div>
  </details>
		The excavator operates each cylinder. It is complicated to control this with hand gestures. You have to come up with an idea to pump it automatically.

- a companion robot
 - High-five, stop, and take pictures. You can express various directions
<img src="https://user-images.githubusercontent.com/77065758/206336401-a56fdcad-7dc5-427c-9a91-fcf9950dbb07.jpg"  width="200" height="160"/>
 
 #### In addition to heavy equipment, I think it can be applied in various ways.

## Getting Started
### Environment
 - python 3.6.9
 - trt_pose 0.0.1
 - pytorch 1.0.0a0
 - sklearn 0.24.2
### Prerequisites
**Step 1 - Download PyTorch and Torchvision for Jetson nano. [link](https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048)**   
**Step 2 - Install [torch2trt](https://github.com/NVIDIA-AI-IOT/torch2trt)**
```
$git clone https://github.com/NVIDIA-AI-IOT/torch2trt
$cd torch2trt
$sudo python3 setup.py install --plugins
```
**Step 3 - Install other miscellaneous packages**
```
$sudo pip3 install tqdm cython pycocotools
$sudo apt-get install python3-matplotlib
```
**Step 4 - Install trt_poses**
```
$git clone https://github.com/NVIDIA-AI-IOT/trt_pose
$cd trt_pose
$sudo python3 setup.py install
```
**Step 5 - Install dependecies for hand pose**   
```
$pip install traitlets
```
**Step 6 -  Download model weight**
| Model | Weight |
|-------|---------|
| hand_pose_resnet18_baseline_att_224x224_A | [download model](https://drive.google.com/file/d/1NCVo0FiooWccDzY7hCc5MAKaoUpts3mo/view?usp=sharing) |
- Download the model weight using the link above.   
- Place the downloaded weight in the [model](model/) directory

**Step 7 -  Open and follow robot_control_with_hand_gestures.ipynb notebook**

## Issues
If you got TLS block issue when import the sklearn in ipynb, add this
```python
import os
os.environ['LD_PRELOAD']='<your sklearn path>/scikit_learn.libs/libgomp-d22c30c5.so.1.0.0'
```

## Customize
Moving the Robot in real world you should have to change the parameters of Robot movements  for adaptable real world
```python
if gesture_joints == 1: # stop
    robot.stop()
elif gesture_joints == 2: # left
    # at here
elif gesture_joints == 3: # forward
    # at here
elif gesture_joints == 4: # right
    # at this
elif gesture_joints == 5: # backward
    # at this
else:
    robot.stop()   
```

## References
- [JetCam](http://github.com/NVIDIA-AI-IOT/jetcam) - An easy to use Python camera interface for NVIDIA Jetson
- [JetBot](http://github.com/NVIDIA-AI-IOT/jetbot) - An educational AI robot based on NVIDIA Jetson Nano
- [trt_pose](https://github.com/NVIDIA-AI-IOT/trt_pose) - Real-time pose estimation accelerated with NVIDIA TensorRT
- [trt_pose_hand](https://github.com/NVIDIA-AI-IOT/trt_pose_hand) - Real-time hand pose estimation based on trt_pose
- [deepstream_pose_estimation](https://github.com/NVIDIA-AI-IOT/deepstream_pose_estimation) - [trt_pose](https://github.com/NVIDIA-AI-IOT/trt_pose) deepstream integration
- [ros2_trt_pose](https://github.com/NVIDIA-AI-IOT/ros2_trt_pose) - ROS 2 package for "trt_pose": real-time human pose estimation on NVIDIA Jetson Platform
- [torch2trt](http://github.com/NVIDIA-AI-IOT/torch2trt) - An easy to use PyTorch to TensorRT converter
