# pointgrey_overhead_camera

This code is for connecting to the Pointgrey camera above the air bearing table via Robot Raconteur and detecting Aruco tags. 
It may also be used for connecting to other Pointgrey cameras. 
Note that Pointgrey camera Python SDK must be downloaded and installed for this code to run properly. 
This code also requires Robot Raconteur for Python and openCV with Aruco. 

### overheadCamServiceFast.py
Python script for connecting to the camera via Robot Raconteur. 
Multi-threading is used to speed up resposne time (i.e., one thread performs tag detection continuously, another thread runs the Robot Raconteur code and allows for data to be read). 
However, there is still some delay in response time, likely due to the threads being locked by openCV or the Pointgrey code. 
If marker data cannot be read sufficiently fast using this code, use overheadCamHost.py to increase read speed. 
Note that the marker pose data may be read faster than it is updated - using overheadCamHost.py only increases the read speed, not the speed at which the markers are detected. 

### overheadCamServiceFast.robdef
Robot Raconteur robdef file for overheadCamServiceFast.py script.

### overheadCamHost.py
Allows for marker data to be read at a faster rate. 
Multi-threading used to continuously read data from overheadCamServiceFast.py (one thread) and allow Robot Raconteur to connect and read data (another thread). 
Note that this script does not increase the marker detection speed, but only allows data to be read at a faster rate. 
This script assumes both overheadCamServiceFast.py and overheadCamHost.py are being run from the same machine, and that default port designations are used. 
If this is not the case, the code can be changed to reflect where overheadCamServiceFast.py is being run and which tcp port is being used for communication. 
To use this code, run overheadCamServiceFast.py first and then run overheadCamHost.py. 
When shutting down, shut down overheadCamHost.py first and then overheadCamServiceFast.py.

### overheadCamHost.robdef
Robot Raconteur robdef file for overheadCamHost.py script.
