
# HouLEAP

Easy Leap Motion integration for Houdini

No listening server nor panel needed, only a simple set of nodes to handle all your Leap Motion needs.

![alt text](https://user-images.githubusercontent.com/6809654/44048510-d25513dc-9f31-11e8-83bb-347051798b1f.PNG)

An example hip file is included to get you started.

# Setup

First, you obviously have to install the Leap Motion drivers.

Then, simply copy the content of the **/houdini16.x** folder to your houdini home/hsite folder.

Alternatively, keep them in your GitHub local repo, and link it from your **houdini.env** config file :
```
LEAP = C:\Path\To\GitHub\HouLEAP\houdini16.x
HOUDINI_PATH = $LEAP;&
```
This hasn't been tested under a version of houdini below 16.0 and another OS than Windows. 

Copying unix leap binaries to **/houdini/python/scripts/** might do the trick.

# Nodes

### LEAP_Initialize
![alt text](https://user-images.githubusercontent.com/6809654/44050321-ec5f41c6-9f36-11e8-9c17-dc630f99b9ec.PNG)

Drop this node at the begining of your network to handle the activation of the leap device.

From the parameters you can enable/disable the leap, or re initialize the session.

### LEAP_Track
![alt text](https://user-images.githubusercontent.com/6809654/44050908-a6c7b632-9f38-11e8-97b1-ba14dd4b814c.PNG)

This is the main node of this process that does all the magic.

It reads the data frame from the leap device and creates all the basic geo, groups and attributes that represents the detected hands motions.

### LEAP_HandsGeometry
![alt text](https://user-images.githubusercontent.com/6809654/44050966-d5e0eee8-9f38-11e8-9d23-276ca88973de.PNG)

This node is here to build a basic hand geometry setup.

You can get simple mesh shapes with custom sizes / colors, or smoother versions from VDB conversion.

![alt text](https://user-images.githubusercontent.com/6809654/44051411-12c98c88-9f3a-11e8-9693-b5512be7d538.PNG)*Mesh*
![alt text](https://user-images.githubusercontent.com/6809654/44051414-144a728e-9f3a-11e8-9649-7cc2aadd9738.PNG)*Smooth*
![alt text](https://user-images.githubusercontent.com/6809654/44676337-3ee43f80-aa33-11e8-873e-7638a4f394c0.PNG)*PointCloud*

### LEAP_DummyHands
![alt text](https://user-images.githubusercontent.com/6809654/44050968-d6ff2588-9f38-11e8-9914-164bc0a41819.PNG)

This node generates a static representation of the hands gotten from the tracking.

This can be helpful to work on later logic of the network without needing any tracking data.

All the groups & attributes included.

### LEAP_Debug
![alt text](https://user-images.githubusercontent.com/6809654/44050970-d84760d6-9f38-11e8-8323-3edfc30b8516.PNG)

This nodes adds lots of visualizers in the viewport to better understand the attributes stored on points & primitives of the tracked data.

![alt text](https://user-images.githubusercontent.com/6809654/44051758-02fb063c-9f3b-11e8-8d25-41c2146b6e31.PNG)

You can use it before or after using the **LEAP_HandsGeometry** sop.

# For Devs

All the leap data is stored into the python **hou.session**.

**hou.session.leap** is a class (Hou) packing everything you'll need :
```
hou.session.leap.is_connected()    # defines the leap motion device state
hou.session.leap.get_frame()       # get current frame tracking data
hou.session.leap.enable()          # enable leap controller interface
hou.session.leap.disable()         # disable leap controller interface
```

# Updates

### 27/08/2018
- new python session code
- arms tracking
- changing device state actually change device pause state
- LEAP_HandsGeometry : added point cloud output
- .gitignore

### 17/08/2018
- LEAP_DummyHands : fix missing prim attributes
- LEAP_Initialize : fix comments typo
- LEAP_HandsGeometry : add packing option
- Fix houdini.env example in readme

# Author

- Gratien Vernier - https://www.linkedin.com/in/gratien-vernier/
