# IoT_Shared_Feed_KussieLove

# IoT - Adafruit IO - Arduino - Shared Feed KussieLove - Manual - Edward van Vliet

# How to send something with a NodeMCU 1.0 to another NodeMCU 1.0, by using Arduino IDE (2.0) software.

By Edward van Vliet - 500761369<br>
Last updated 13 October 2022

## Introduction
Using this manual you'll be able to send something from your NodeMCU 1.0 on Adafruit IO to another NODEMCU 1.0, by using Arduino IDE (2.0) software.

## Required hardware components
  - 2x Node MCU 1.0. (You'll need a partner to follow this manual and execute this exercise.)
  - 1x Push button
  - 3x Wire cables
  - 1x USB-C to USB-B microcable (https://www.allekabels.nl/usb-c-kabel/11518/4080378/usb-c-naar-usb-b-micro-kabel.html?gclid=Cj0KCQjw1vSZBhDuARIsAKZlijQllk1tmEmzDAyOpEEB6p9cz1rm71ymovd92VNrhihNyiu-eR0gt8saAvW9EALw_wcB)
  
  
## Step 1: Connecting the Node MCU 1.0 to your laptop, and connect your push button to the Node MCU 1.0
The first thing we want to do is connect our Node MCU to your laptop, using an USB-C to USB-B microcable. Then, we want to connect our bush button to the Node MCU, using Jumber Wires glued at the other end of the LED-strip. The image below shows which wires need to be connected to which pins on the board.

Leftmost pin to `3v3` (red wire)<br>
Second pin to `GND` (black wire)<br>
Right pin to `D0` (yellow wire)<br>

## Step 2: Installing the required libraries in Arduino IDE
For the LED-strip to properly function, we will first need to install the required libraries in the [Arduino IDE](https://www.arduino.cc/en/main/software). We can do this by going to the 'Sketch' dropdown menu, selecting 'Include Library' and then clicking on 'Manage Libraries'.<br>

1. Go to the libraries tab that is the third button on the left. If your IDE verion is lower than 2.0, you can find this in Sketch > Include library > Manage libraries.
2. Here you search for "Adafruit IO Arduino". Watch out because sometimes the right one is not the one that pops up first.
3. Find the right one and click "Install" and then "Install All".

### Step 3: Setting up Adafruit IO

1. Go to https://io.adafruit.com/, click on "Get started for free" and make your account.
2. When your account is ready, click on "IO" in the navigation menu at the top of the page.
3. Click on the button with the yellow key icon.
![Image of your key and username in Adafruit IO](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/01_ADAFRUIT_IO_KEY_USERNAME.png)
4. Copy your key and remember your username for later use.

### Step 4: Creating and sharing your Adafruit IO Feed

In Adafruit IO:
1. Go to Feeds > New Feed, give it a name and create the feed.
2. On Adafruit IO, set your feed to sharing.
![Image of sharing Feed in Adafruit IO](https://github.com/edwardvanvliet/IoT_Shared_Feed_KussieLove/blob/main/images/00_Sharing_your_feed.png)


### Step 6: Adjust your code

In Arduino IDE:
1. Go to File > Examples > Adafruit IO Arduino > Adafruitio_06_digital_in.

2. Then click on the tab "config.h" in Arduino IDE, fill in your username and key like the example below (in point 3).

```
#define IO_USERNAME "YOUR USERNAME HERE"
#define IO_KEY "YOUR KEY HERE"
```

3. Below that, you can fill in your WiFi SSID and Password.
(Advice: Use your phone's hotspot to prevent router problems, so you can use it everywhere. Also prevent using a 5GHz WiFi if possible.)<br>

```
#define WIFI_SSID "YOUR NETWORK NAME HERE"
#define WIFI_PASS "YOUR PASSWORD HERE"
```
![Image of adjusting Key and WIFI in code in Arduino IDE](https://github.com/edwardvanvliet/IoT_Shared_Feed_KussieLove/blob/main/images/05_Connecting_Key_WiFi.png)

4. Change the BUTTON_PIN to "D0", like the example below.

```
#define BUTTON_PIN     D0
```

5. Add the the following code to your Arduino. Both need to have this in their file.

```
#define FEED_OWNER "AIO_FEED_OWNER"
AdafruitIO_Feed *sharedFeed = io.feed("FEED-NAME", "feedOwner");
```

6. Upload your code by clicking on the button with the arrow icon pointing to the right. (Top left of your screen).


### Step 7: Upload your code

1. First, you could verify the code by clicking on the (when hovering on it - white) button with the check mark icon on it. When you click on it, the button will turn yellow, this means Arduino IDE is verifying/compiling the sketch as you can see below. You can also see what is happening on the right bottom corner: "Compiling sketch..."

2. Upload your code by clicking on the button with the arrow icon on the top left of your screen, right next to the check mark icon button (used for verifying).

3. Activate the "Serial Monitor" with the magnifying glass button on the top right. Open the "Serial Monitor" on the bottom of your screen.

![Image of opening the Serial Monitor in Arduino IDE](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/12_Activate_Open_the_Serial_Monitor.png)

4. Change the baud rate in the Serial Monitor to 115200 baud.

![Image of changing baud rate to 115200 baud in Arduino IDE](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/13_Set_to_115200_baud.png)

5. If everything worked as planned, you will see that you're connected in the Serial Monitor. If not, try to use your mobile Hotspot WiFi, that worked for me, as you can see below.

![Image of mobile hotspot WiFi connected](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/14_Device_is_connected_to_my_hotspot.png)

As you can see, my mobile hotspot is successfully connected to the device (ESP-296609).

### Step 7: Test your code

In the Serial Monitor you should see some (input) data coming up, if your partner pushes on the push button.


## Possible Errors:


## Error 1: Connection Error
If you keep seeing dots coming up on your Serial Monitor, it means something is wrong with the connection of your NodeMCU 1.0.
In my case the problem was the WiFi connection.
Because at first, I tried using my 5GHz (Home) WiFi throughout this whole process.
Unfortunately the Serial Monitor kept presenting me dots...

![Image of the connection error dots in the Serial Monitor](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/17_Connection_Error_dots.png)

The dots that are appearing every 1/2 a second on your Serial Monitor means that your hardware, in this case the NodeMCU 1.0, can't properly connect to a WiFi network.
That's why it is highly recommended to use an own mobile hotspot, PREVENT using a 5GHz WiFi or hotspot! (According to [this source](https://arduino.stackexchange.com/questions/49370/esp8266-not-connecting-to-wifi) on Arduino Stack Exchange.)

## Solution to Error 1: Connection Error
Seeing the dots keep coming up on my Serial Monitor, I directly knew there was something wrong with the connection.
And then I searched about this connection error, and I found out I was not the only one with this problem.
Apparently according to [this article post about ESP WiFi problems](https://arduino.stackexchange.com/questions/49370/esp8266-not-connecting-to-wifi), the ESP(-296609) is not able to connect with 5Ghz WiFi.

![Image of mobile hotspot WiFi connected](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/14_Device_is_connected_to_my_hotspot.png)

So then I tried connecting the ESP-296609 to my mobile hotspot WiFi, on my smartphone. And fortunately, it worked!
In the Serial Monitor you should see all the input data from your partner coming up, this means that the whole process of sharing a feed worked!
