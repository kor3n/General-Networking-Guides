# Locating an end device on the network
This will show how to locate what switch an end device is connected to both from the core layer of the network and also at access layer.

**The commands shown are used from a cisco device.**

# Method One
First off you need to find the mac address of the end device. If you are able to get this from the user great if not you will need an IP address as a minimum.

Finding it from arp if you only have the IP. If you were given the MAC you can skip this step:

`switch# show ip arp | i x.x.x.x`

Now that you have the MAC address you need to see what interfaces have that MAC address on it on the MAC table:

`switch# show mac address-table address xxxx.xxxx.xxxx`

If you have more than one MAC on the same interface there is a good change that there is another switch in the path, with this you can use CDP to look to see what is connected:

`switch# show cdp neighbors`

or

`switch# show cdp neighbors gix/x/x`

The above will show if another switch is connected that has CDP enabled, if you dont know or have it to hand the IP required to get onto that switch that can be found by adding detail on the end of the second command

`switch# show cdp neighbors gix/x/x detail`

Now connect to that switch and repeat until you find the final switch that the end device is connected to.

# Method Two
If you or a member of a local site IT team is able to assist, install... 

1. Unplug the cable that the end device is connected to
2. connect to your laptop / end device
3. Open wireshark
4. Select the ethernet adaptor
5. Type `CDP` into the filter bar at the top
6. Wait for the CDP packets to come in
7. Review the CDP packets with where its connected
