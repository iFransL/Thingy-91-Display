# Adding a display to the Thingy:91

The Thingy:91 is a great tool to test or prototype your cellular applications. Aldo the tool is great often I missed some application feedback when testing in the field. Sure I could connect the usb port or make use of the nRF52840 to make a bluetooth connection. But sometimes a display is just the easiest way to get some information quickly.

[picture of the end solution]

In many of my proof of concept I used one of the many available small monochrome OLED display. As the Thingy:91 was not designed for adding your own break out board I had to be creative. Looking at the schematics I noticed that the I2C line are availble on the PCB as test points. That looked like the best starting point. The needed 1V8, 3V3 and GND are also available as test pins.

### **Schematics of Thingy:91**
<img src="https://github.com/iFransL/Thingy-91-Display/blob/main/images/2_Schematics_I2C_Lines.jpg" width="1000">
The test pins are easy accesable on the top layer of the Thingy:91. 

### **Top layer of Thingy:91 PCB**
<img src="https://github.com/iFransL/Thingy-91-Display/blob/main/images/3_PCB_TopLayer.jpg" width="1000">


The I2C lines in the Thingy:91 are on the 1V8 rail. There are different devices already on the line with either a VDD of 1V8 or 3V3. The SSD1306 used in the OLED is working on 3V3 and the I2C bus accept 1V8 logic bus. When testing it on the nRF9160DK with the I/O voltage switch on 1V8 it worked perfectly. Unfortnatly when connecting the display to the thingy:91 it worked the first time after loading the application into the thingy:91. But after a power cycle the display stays off. The PMIC in the thingy didn't startup when the display  is connected. After some searching it looks like it is caused by the pull-up to VDD (3V3) on the I2C bus in the OLED module. The easiest solution is to add a bidirectional level shifter fast enough for I2C bus. The first test I did with a simple FET based level shifter break out board showed a lot of errors on the I2C bus. I got the best results with a SparkFun PCA9306 based break out board.

### **Connection diagram**
<img src="https://github.com/iFransL/Thingy-91-Display/blob/main/images/4_ConnectionDiagram.jpg" width="1000">

Time to work on a holder for the display. Initaly I designed the holder without the space for the level shifter. This looked great but it was a challenge to mount the level shifter break out board. In the first test I put the level shifter on top of the battery. But I needed to cut some of the plastic of the housing to bring the wires to bottom. Also the holder needed to be mounted using bolts and nuts. This wasn't perfect as you need to remove this for changing the sim-card.

[picture first holder]

For the second prototype I made a change to the concept. I got rid of the bolts and nuts by makeing 3 pins to snap into the mounting holes. And I added a mini connector for the cables connecting to the Thingy:91. Now it is easy to remove the display and more important you can change the sim-card simply.
For creating the holder I used OpenScad. All files can be found within the github project. 

[picture second holder]

For the cable I used a pre-assembled cable set using the JST 2mm connector. I Created a small cable assembly using crimp wire. In the cable assembly I also splitted the GND and 3V3 to two wires for the OLED and the Level Shifter.  

[picture cable assembly]




