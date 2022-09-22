# Fake Eastron SDM
 An ESP8266 project to emulate an Eastron SDM power meter

 ## Background

 I need to limit the power that my solar inverter exports to the grid.
 
 This is normally achieved by connecting an Eastron SDM230 power meter via modbus to the inverter's (Growatt MIN 3600TL-XE in my case) 2nd modbus port. Once installed the inverter acts as a master, polling the SDM230 slave device's input regisiters for data. If it detects that power is being exported to the grid, it limits the inverter's output power to maintain (approximately) zero export.

 I have a slightly more complex setup with a solar water heater diverter in the mix, this intercepts the unused power and uses it to heat my hot water tank. But once the talk is fully heated (usually around 2pm in the Summer) the power is exported to the grid - which I do not want. The real SDM230 power meter is not compatible with this process and half export before the solar diverter gets a chance to heat the water.

 My solution for this is to emulate the Eastron SDM230 and maintain full control of when the inverter limits is power output.

 ## Alpha software

 Heads up!
 - I am not a dev.
 - This is not yet tested as I'm away from home.
 - I started developing this project out of necesity and learned just enough C++ to get this working, my code is probably horrible!

 ## Required tools

 You will need:
-  ESP8266 device (I'm using a Wemos D1 mini clone 3.5 euros)
-  MAX485 TTL to RS-485 Interface Module (2 euros)
-  A calbe to connect the module to your inverter (I cut the ends of an Ethernet patch cable)
-  5 dupont cables

## Building the device

It's super easy. Connect the MAX485 module to your ESP8266 board:

D2	  ---> DI
D3	  ---> RO
D0	  ---> RE
D0	  ---> DE
Vcc	  ---> 3.3V
GND   ---> GND

Then connect your MAX485 module's A/B terminals to the A/B terminals on your inverter using two wires from your sacrificial ethernet patch cable - A links to A, B links to B. In my case, on the Growatt MIN 3600TL-XE I had to use pins 5 and 6 which is the power meter modbus.
