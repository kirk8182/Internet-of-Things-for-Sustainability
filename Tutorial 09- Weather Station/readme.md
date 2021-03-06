
# Creating a WeatherStation
### Challenge Level: 4/5
![Final-WS](https://user-images.githubusercontent.com/22579849/32729554-0d581f54-c839-11e7-999c-7cc947be4bbe.jpg) <br />

## Introduction
### In this tutorial you will...
  1. Introduce the concept of IP addressing and networking
  2. Introduce and install the Wifi Card
  3. Build a working WeatherStation
  
## Explanation
In this tutorial, we will be creating a WeatherStation node. A weatherstation reports the current weather. The WeatherStation will report the current temperature (in Fahrenheit) and UVindex on an LCD screen. In addition our weather station will report these values on a webserver hosted on the weather node. In layman's terms, this wil allow us to connect a computer or cellphone and it will display some information on a website. In addition this website will display clothing suggestions based on the current weather conditions.
 
## Required Materials
 1. Intel Galileo board kit and PC with Arduino IDE installed (see Tutorial 1)
 2. Grove shield
 3. Grove LCD
 4. Grove temperature sensor
 5. UV sensor
 6 Mini PCI-e Wireless card (Intel Centrino Advanced N6230)
 7 Working WPA2 wireless network
 
## Networking
### IP Addressing
A network is defined as a series of nodes connected together for information sharing or other useful purposes. The internet is a great example of exactly how powerful and useful networks can be in our useful lives. For this reason, Internet of Things devices are almost always connected to a network of some kind (if not internet connected). In this tutorial we will introduce some basic network functionality. However in order to do so, one must understand how nodes communiate on a network.

Imagine a crowded room of people and you want to communicate with someone in particular. Simply shouting what you want to tell them might be sufficient. But in order for them to understand who you are talking to, you would usually state their name to get their attention. IP addresses are the names given to nodes on a network in order for them to talk to each other. IP addresses can come in a variety of forms. However, the IP addresses that we will be seeing/using come in the form of '192.168.xxx.xxx'. Simply using a machine's IP address will allow one to send data to them.

### Wireless 
Speaking of networking, let's talk about what sort of network we will be using for this tutorial (and future tutorials). We will be using a wireless router to create an access point for our Intel Galieo boards and other devices to connect to. This network will also allow a computer or cellphone to connect to the network and communicate with a board by using it's IP address. The wireless router should already be setup by your instructor(s). However, keep in mind that any network could be used in place. We simply wanted a network that was not connected to the internet.
 
## Wifi Card (Intel Centrino Advanced N6230)
![WifiCard-WS](https://user-images.githubusercontent.com/22579849/32729550-0d16439a-c839-11e7-83f1-66a7f27e87be.jpg) <br />
![WifiCard2-WS](https://user-images.githubusercontent.com/22579849/32729558-0dafd9ce-c839-11e7-904e-6ac32f2c28d9.jpg) <br />
In order for our Intel Galileo boards to connect to the wireless network, we will need a wireless card to do so. A wireless card is a device that will attach to our boards that will enable them to see and communicate on any wireless network. The Intel Centrino card is compatiable with the Galileo and is capable of communicating on a variety of common wireless protocols; Hence, why we chose to use it.

## Building a WeatherStation

### How it works
The basic logic involves taking information from the UV sensor and temperature sensor and reporting it to the LCD in a useful way. The real interesesting part of this project is making weather suggestions. Once UV index and temperature have been calculated, these values determine what suggestions are made. These come in the form of IF-STATEMENTS. For example, IF temperature > 80, then suggest the user wears shorts today. Please take this time to look at the WeatherStation and determine what suggestions can be made and what the requirements for each are.
 
### Assembly
#### Installing the WifiCard
To install the wireless card into the Galileo start by turning the Galileo upside down and find it's PCI port.
![WifiCard_Insertion1-WS](https://user-images.githubusercontent.com/22579849/32729557-0d9c7f50-c839-11e7-9fa2-3bbaffcdc19a.jpg) <br />
If the backplate is not already attached to the wireless card, please use a small screwdriver to do so. It is only 2 phillips head screws. Take the card and identify it's pin connectors. There should be a longer group of them and a shorter grouping. Line these up with the Galileo PCI connector. Firmly press the card into the Galileo board. The backplate can then be pressed into the locking plastic stubs located on the bottom of the Galileo board. It should look like the following when done correctly.
![WifiCard_Insertion2-WS](https://user-images.githubusercontent.com/22579849/32729551-0d2baff0-c839-11e7-9156-e5f137db6c7a.jpg) <br />
Take note of the wireless card's attenae. These have gold colored connectors at the non-antenna portions (see below).
![WifiCard_Insertion3-WS](https://user-images.githubusercontent.com/22579849/32729556-0d84536c-c839-11e7-84a9-56a9d17f2ed1.jpg) <br />
There should be 2 similarly shaped female connectors slots on the wireless card. Line up each antenna's connector with the female slot on the wireless card. Press firmly until both antenna are firmly connected.
![WifiCard_Insertion4-WS](https://user-images.githubusercontent.com/22579849/32729555-0d6f9c7e-c839-11e7-8e65-47c0a2633853.jpg) <br />


#### Installing the components
Install the UV sensor, temperature sensor, and LCD using the provided quick connect cables. The following table has been provided for your useage.<br />

Port | Component
--- | ---
A0  |  UV Sensor
A1  |  Temperature Sensor
I2C |  LCD 

The result should look something similar to the following. <br />
![SensorsAssembled1-WS](https://user-images.githubusercontent.com/22579849/32729560-0dda5410-c839-11e7-810a-ccec19ecb423.jpg) <br />

With the UV sensor, temperature sensor, and LCD attached to the Grove shield, it should look like the following.<br />
![SensorsAssembled2-WS](https://user-images.githubusercontent.com/22579849/32729552-0d4109fe-c839-11e7-8df7-85552b6d44b8.jpg) <br />

#### Update the IP address
As per usual, please connect your Grove shield to the Intel Galileo and connect the power supply to power the board on. When the USB light illuminates, connect a usb cable to your computer and Intel Galileo. Open the Arduino IDE and then the WeatherStation code. Once the board is recognized by the Arduino IDE, open a serial connection to your board. <br />
![getIP1-WS](https://user-images.githubusercontent.com/22579849/32729187-cb776078-c837-11e7-9592-d4ba1e33d384.JPG) <br />
Compile and upload the sketch to the Intel Galileo. If working correctly the Serial Connection should state that it connected to the network and provide the IP address of the board. If the connection is not established, ensure that the SSID and password in the code match your network's credentials. Remember the IP address, we will use it to connect to the board later on. <br />
![getIP2-WS](https://user-images.githubusercontent.com/22579849/32729188-cb8e560c-c837-11e7-9e5a-a0fd2dc080a6.JPG) <br />

### Results
After all of our work, the Intel Galileo should be displaying temperature and UVindex correctly on the LCD screen. <br />
![FinalAssembled-WS](https://user-images.githubusercontent.com/22579849/32729554-0d581f54-c839-11e7-999c-7cc947be4bbe.jpg) <br />
To test if the webserver is working, connect a device to the wireless network. Then open a web browser and enter the Galileo's IP address into the address bar. A website should be displayed, that looks something like this...<br />
![Connecting-WS](https://user-images.githubusercontent.com/22579849/32729189-cba41690-c837-11e7-9bc4-54398665a13c.JPG) <br />

### Exploratory Questions
 1.  How are the who are the server and client in this scenario? How can we be sure that a message made it to to it's intended recipient?
 2.  Why is it useful to be able to use conditionals (IF statements) in our code?

### In this tutorial we did the following.
 
 1. Learned about networking and IP addresses.
 2. Walked through the logic for a WeatherStation.
 3. Installed the physical components.
 4. Updated code after finding the IP address of the board and network credentials.
 6. Finished and tested the WeatherStation.
  
## BONUS CHALLENGE(S)

### A More Helpful Node
Modify the code of the server to add the following suggestions based on UV Index and Temperature.

 1. If the UV index is greater than 7, print the message: "Woah, it's bright. Wear sunglasses."
 2. If the UV index is between 5 and 10 and it is greater than 100 degrees outside, print the message: "Don't go outside!"
 3. If the temperature is between -20 and 28 degrees, print the message: "Freezing cold! Wear lots of layers."
