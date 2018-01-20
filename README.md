# VoodooI2CUPDDEngine
This kext is used to inject a multitouch engine for use with touch-base's UPDD gestures.  A compatible version of
touch-base's UPDD driver must already be installed and configured.  Compatible means that your installed version
must have the capability of enumerating a virtual device interface.  For the Mac, this seems to be UPDD_6_00_235 or
higher (An even later version will be required for High Sierra).

# Setup
After installing UPDD, open a Terminal window and use the command line utility to configure / calibrate - 

//  Add the virtual device


upddutils adddevice 1

upddutils set virtual_device 1



//  Set the calibration by entering your *effective* resolution (for example - my physical screen resolution is
2736 x 1824, however, because it is *retina-ized*, the OS sees it as 1368 x 912 so that is what is used for calibration.  
To set calibration to 1368 x 912 - 


upddutils set calx1 1368

upddutils set caly1 912




Additional calibration points are calx0 and caly0, these should be set to zero by default.  You can check that everything 
is set up as needed by entering - 

upddutils get '*'

# Client

A userspace client utility is also need to transfer the finger data out of VoodooI2C (kernelspace).  You can either use the
binary or compile from source here - https://github.com/blankmac/voodooi2c-client-rewrite

The client can be run in the background without a terminal window by creating an automator document and setting it to 
execute a shell script on boot with the following commands --

nohup ~/Your/path/to/voodooi2c-updd-client &>/dev/null &

exit

