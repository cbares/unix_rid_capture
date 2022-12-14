# WiFi RID capture
A program that uses libpcap to capture ASTM F3411 / ASD-STAN 4709-002 UAV direct remote identification signals transmitted over WiFi.

Requires 
  * WiFi hardware capable of being put into monitor mode,
  * libpcap-dev,
  * opendroneid.c and opendroneid.h from [opendroneid](https://github.com/opendroneid/opendroneid-core-c/tree/master/libopendroneid).

The output is in json format. An perl script is provided which converts the json into gpx files suitable for Google Earth.

Tested using an rtl8812au based WiFi dongle.

If anybody runs this in the vicinity of an "Arrêté du 27 décembre 2019" French ID, I would appreciate the debug.txt.

## Getting Started

### Hardware and Driver

You need a WiFi card/dongle that can be put into monitor mode. If you are using an rtl8812au dongle you will need to build and install a third party driver which is a bit of a palaver. Modify the monitor.sh script as required until it is getting the hardware monitoring channel 6.

### Compile rid_capture

Install libpcap-dev if required, make sure that all the options at the top of `rid_capture.h` are set to 0 and type make. It may make things easier later on if you edit the default device name near the top of rid_capture.c to match your installation.

### Running rid_capture

You will probably need to run rid_capture as root or have root set rid_capture so that it runs as root (`chmod +s rid_capture`).

Run rid_capture. If it suggests that you use the -x option do so. You can override the device name on the command line. The first line that it outputs will show you what device it is using. Control C stops the program.

rid_capture defaults to writing json to stdout. Capture this json to a file, e.g. `rid_capture -x > rid_capture.txt` and then feed it to the rid2gpx.pl script (`rid2gpx.pl < rid_capture.txt`). If this works you will end up with a gpx file that Google Earth will display.

If nothing is transmitting WiFi RID, rid_capture will peridically put out debug reports saying how may WiFi packets it has seen.







