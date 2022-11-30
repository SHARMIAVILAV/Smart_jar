EXPLANATION:
Smart Jar allows us to keep track of the stocks, and it is easily accessible from using the internet. The Jar includes an ultrasonic sensor at the top of it and uses the ultra-sonic reflected waves to figure out at what extent the Jar is filled and how much space is left inside the jar. Whenever the amount of content changes in the jar, it is sensed by the NodeMCU, and the same is updated on the web server. This can be helpful to track supplies and plan for restocking from anywhere in the world. Previously we used Arduino and ESP8266-01 to build smart dustbin using the same methodology.
How does an Ultrasonic Sensor work?
Before we get any further, we should know how an Ultrasonic sensor works so that we can understand this tutorial much better. The ultrasonic sensor used in this project is shown below.
As you can see it has two circular eyes like projections and four pins coming out of it. The two eye-like projections are the Ultrasonic wave (hereafter referred as US wave) Transmitter and receiver. The transmitter emits an US wave at a frequency of 40Hz, this wave travels through the air and gets reflected back when it senses an object. The returning waves are observed by the receiver. Now we know the time taken for this wave to get reflected and come back and the speed of the US wave is also universal (3400 cm/s). Using this information and the below high school formulae we can calculate the distance covered.
Distance = Speed × Time
Now that we know how an US sensor works, let us how it can be interfaced with any MCU/CPU using the four pins. These four pins are Vcc, Trigger, Echo and Ground respectively. The module works on +5V and hence the Vcc and ground pin is used to power the module. The other two pins are the I/O pins using which we communicate to our MCU. The trigger pin should be declared as an output pin and made high for a 10uS, this will transmit the US wave into the air as 8 cycle sonic burst. Once the wave is observed the Echo pin will go high for the exact interval of time which was taken by the US wave to return back to the sensor module. Hence this Echo pin will be declared as input and a timer will be used to measure how long the pin was high.
The circuit is very simple as we are only using the ultrasonic sensor and NodeMCU. HC-SR04 ultrasonic sensor works on 5V, so if you connect it to 3.3V, it won’t work. VCC pin of the ultrasonic sensor is connected to the VIN pin of NodeMCU. Trig and Echo pins are connected to D5 and D6 pin of NodeMCU while the GND pin of the sensor is connected to the GND pin of NodeMCU. A 5V power supply powers NodeMCU.