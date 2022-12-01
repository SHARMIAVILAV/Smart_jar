
# IOT based Smart Jar

In this ***Internet of Things (IoT) smart jar***, we will are using an ultrasonic sensor to monitor the level of a Jar and then email the user with a warning. Jar's level will also be shown on a website run by an ***ESP8266 NodeMCU***.

## Description
We can quickly access this smart Jar via the internet and use it to keep track of the stock prices. The Jar has an ***ultrasonic sensor*** at the top that measures how full the Jar is and how much room is still within using the *ultrasonic reflected waves*. The ***NodeMCU*** detects any changes in the volume of the contents in the jar, and updates the web server accordingly. This can be used to *keep track of supplies* and *make restocking plans* from any location in the world.


## Circuit Connection

Since we are only utilising the ultrasonic sensor and NodeMCU, the circuit is quite straightforward. The **HC-SR04 ultrasonic sensor requires 5V to operate**; if you connect it to 3.3V, it will not function. The ultrasonic sensor's VCC pin is linked to NodeMCU's VIN pin. The **NodeMCU's D5 and D6 pins are linked to the Trig and Echo pins**, respectively, while the sensor's GND pin is connected to the NodeMCU's GND pin. NodeMCU is powered by a ***5V*** power supply.


## IFTTT Setup for Smart Jar


1. First login to [*IFTTT*](https://ifttt.com/) and search for ‘Webhooks’
2. Now to get the Private key, click on ***`Documentation`***. Copy this key somewhere, it will be used in the code.
3. Create an applet using Webhooks and Email services. To create an applet, click on your profile and then click on ***`Create`*** from available options.
4. Now in the next window, select ***`If This Then That`***.
5. In ***`This`*** field we will use webhooks to get the web requests from the NodeMCU.
6. Now select ***`Receive a Web Request`***  trigger and then enter the event name as jar_event and then click on ***`Create Trigger.`*** 
7. After this, click on ***`Then That`***  and then click on Email.
8. Now in Email, click on ***`send me an email`***  and enter the email subject and body and then click on create action.
9. In the last step, click on ***`Finish`***  to complete the Applet setup.




## Code Explanation

By including all the required library files we can start our code. The ultrasonic sensor doesn’t require a library file, so we only need ESP8266WiFi.h library file.

`#include <ESP8266WiFi.h>`

After that, define the pins where you connected the Trig and Echo pins and also define two variables for calculating distance and duration.

`const int trigPin = D5;  
const int echoPin = D6;
long duration;
int distance;`

After that, make instances for Wi-Fi name, Wi-Fi password, IFTTT hostname, and private key.

`const char* ssid = "Wi-Fi Name";
const char* password = "Password";
const char *host = "maker.ifttt.com";
const char *privateKey = "Private key";`

Now to access the WiFiServer, we declared an object WifiServer library. 80 is the default port for HTTP.

`WiFiServer server(80);`

Now inside the void loop function, calculate the time between triggered and received signal. This time will be used to calculate the distance.

`duration = pulseIn(echoPin, HIGH);
distance = duration * 0.0340 / 2;`

After that, distance is converted into a percentage to show the Jar’s occupancy.

`level =((14-distance)/14.0)*100;`

Then we compared the jar’s occupancy, and if the occupancy level is less than 5, then it will trigger an IFTTT event to send warning Email.

`if ( level <= 10) {
        send_event("jar_event");
        }`
## Testing

Just use hands  to check its working capability after uploading the code. Now use the IP address that is given on Serial Monitor to inspect the website. It should display how full the Jar is. Additionally, if the Jar's occupancy level is below 10, a warning email will be sent to you. Here, the warning level is established based on how long my Jar is. It can be modified to fit your needs.

![smart_jar](https://user-images.githubusercontent.com/84708284/205092746-a87a41ff-0224-43c8-9adb-bfe887ddb30f.jpg)

![smart_jar2](https://user-images.githubusercontent.com/84708284/205092841-291242d4-de54-4f21-98d2-fef610a84922.jpg)


![smart_jar3](https://user-images.githubusercontent.com/84708284/205095007-5eac1122-8639-44f9-bedc-c9d78f05e20f.jpg)
