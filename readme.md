Welcome to hueAndMe
===================

The intention of this Python script is to provide an easily implemented Hue Hub emulator w/ UPnP for interfacing with the Amazon Echo (or whatever else may want to speak to a Hue Hub - the original version). 

It is of possible interest to Indigo (https://www.indigodomo.com) users, as it can directly import your Indigo devices (assuming you have web services turned on) and make them available via hueAndMe and the Echo.

It is also of interest for Domoticz (https://www.domoticz.com/) users as it imports devices and makes them available to Alexa.

How to use
-
1. Download a copy of the repository.
2. Edit the hueAndMe.cfg file to include devices, and/or point to your Indigo or Domoticz server. (This should be about as self-explanatory as it gets.)
3. Run the script: <pre>
python hueAndMe.py</pre>
4. Run device discovery on your Amazon Echo (or other device).
5. Enjoy.

Some notes of interest
-
1. If you add URL-based devices in the config file, the dimming URL gets a value between 0-254 passed via substitution of a parameter called {dim}. The examples in the config file show this.
2. There is some weird limit on Hue devices allowed by the Echo. I don’t know if this is TOTAL devices, or per-hub.  I have a real hub, and this simulated hub, and am showing 44 devices total. I’ve set an arbitrary limit of 25 devices pulled from Indigo. This limit is set at the top of devicehandlers/indigoconfig.py.  I suspect you could create multiple virtual hubs (multiple copies of this app, bound to different IPs) to get past this limit.
3. To help with the device limit, you can exclude devices using the exclusions setting for Indigo in the config file. This is just a comma delimited list of device names to ignore. Device names must be in quotes. To disable a device defined in the config file, just add a # before its name. The example devices are both disabled.
3. If you JUST configure the Indigo URL, username and password, then run this app without changing anything else in the config, it will probably work. Don’t overthink it.
4. If you want to support something complex on your Indigo server, create a virtual on/off device.  Yes, I could update this to look at the groups and whatnot, but I didn’t really see a point when virtual devices work fine and we can’t do much besides on and off with the Echo anyway.
5. No real error handling currently. Why? Because I’ve got other things to do, but this is likely useful to 1 or 2 people in its current state. It does exactly what I originally wanted it to do, so there :)  If I have time, I’ll try to make it prettier.

Running as a service Example for Raspberry Pi
-
1. Place the hueAndMe folder in /home/pi
2. Make sure hueAndMe.py is executable <pre>
sudo chmod +x /home/pi/hueAndMe/hueAndMe.py</pre>
3. Copy the systemd service file to the systemd service folder<pre>
sudo cp /home/pi/hueAndMe/hueAndMe.service /lib/systemd/system</pre>
4. Enable start on boot <pre>
sudo systemctl enable hueAndMe.service</pre>
5. Start the service <pre>
sudo systemctl start hueAndMe.service</pre>

Support
-
I created a Nest plugin years ago for Indigo. It required far too much support. I will try to fix bugs, but no promises. Contact me if you need assistance and I’ll do what I can.


Credit
-

This project was originally based on hue-upnp by sagen (https://github.com/sagen/hue-upnp). It bears little resemblance to that project at this point.

