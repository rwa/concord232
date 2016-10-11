GE Concord 4 RS232 Automation Module Interface Library and Server
==================================================================

This is a tool to let you interact with your GE Concord 4 alarm panel via
the RS232 Automation module.

The goal of this project was to utilize my GE Concord 4 alarm panel with [Home Assistant](/home-assistant/home-assistant)

Following the framework of [kk7ds](/kk7ds]/[pynx584](/kk7ds/pynx584) to integrate the nx584 into Home Assistant, and [douglasdecouto](/douglasdecouto)/[py-concord](/douglasdecouto/py-concord)'s' work into building the base communication class as part of their integration into the Indigo platform, we now have a working Interlogix/GE Concord 4 Automation Modeul interface

To install::

 # sudo pip3 install concord232

The server must be run on a machine with connectivity to the panel,
which can be a local serial port

 # concord232_server --serial /dev/ttyS0 


Once that is running, you should be able to do something like this::

 $ concord232_client summary
 +------+-----------------+--------+--------+
 | Zone |       Name      | Bypass | Status |
 +------+-----------------+--------+--------+
 |  1   |    FRONT DOOR   |   -    | False  |
 |  2   |   GARAGE DOOR   |   -    | False  |
 |  3   |     SLIDING     |   -    | False  |
 |  4   | MOTION DETECTOR |   -    | False  |
 +------+-----------------+--------+--------+
 Partition 1 armed

 # Arm for stay with auto-bypass
 $ concord232_client arm-stay

 # Arm for exit (requires tripping an entry zone)
 $ concord232_client arm-exit

 # Auto-arm (no bypass, no entry zone trip required)
 $ concord232_client arm-auto

 # Disarm
 $ concord232_client disarm --master 1234


## Home Assistant
Home Assistant will automatically download and install the pip3 library, but it only utilizes the Client to connect to the server.  I used the instructions [found here](http://www.raspberrypi-spy.co.uk/2015/10/how-to-autorun-a-python-script-on-boot-using-systemd/)
