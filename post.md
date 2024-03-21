# Lab 5: Finite State Machine Design

# Overview and Motivation
Welcome to Lab 5 of CS281: Introduction to Computer Systems! <br>
In this lab we will get deeper into the sensors and actuators. Sensors are devices that gather information from the environment, 
and actuators use that information to physically change the environment. 
We'll explore how to connect these components to an Arduino.

# Objectives of the Lab
1. Understand the basic operation of various sensors and actuators.
2. Learn how to connect sensors and actuators to an Arduino.
3. Design and build a project using sensors and actuators, document your process, and showcase it through a video.
   
# Materials
- PB-503 Breadboard prototyping station (an integrated device with a number of electrical components like switches)
- Arduino Uno
- Wires
- Sensors (buzzer, ultrasonic sensor, photoresistor)
- Actuators (buzzer, servo motor)
- Multimeter 
- Resistors
- LED 
- Computer with Arduino IDE installed

# Overview: 

1. Buzzer: Learn how to control a buzzer using the Arduino to produce different tones.
2. Ultrasonic Sensor: Discover how to use an ultrasonic sensor to measure distances to objects and translate them into readings on the Arduino.
3. Distance Detector: Design a handheld device with an ultrasonic sensor that creates tones based on the distance to objects (low pitch for close, high pitch for far).



# Building the Lab: 
## 1. Buzzer

### 0 About
<br><img width="400" height="400" src="IMG_0407.JPG">

In this section, we will build a buzzer that generates sound. <br>
We will control the buzzer with a wave of pulses that we will generate. <br>

#### What we need
- Arduino Uno or compatible board
- Breadboard
- Wires
- buzzer
- Computer with Arduino IDE installed

 
### 1. Project Step

- We will connect 5 voltage to the + sign labeled pin in the buzzer and connect ground to the - sign labeled in the buzzer.
- The "+" and "-" signs represent the metallic membrane inside the buzzer
- By changing the voltage very frequently,  we can generate a sound 

#### Note: When a 5 voltage is applied to the input pins, the metallic membrane enters an excited state and without the voltage applied, it is contracted. This rotation creates audible click

### 2. Testing
#### Test 1
1. Plug the buzzer onto the breadboard so that the two pins span two distinct rows. Make sure the + pin is in
the higher row (up) and the - pin is in the lower row (down).
2. Use a wire to connect the - pin to the ground. Plug a longer test wire in the + pin.
3. Now take the other end of the + wire alternately touch it and release it to any +5V connection. You
should hear an audible “click” each time you touch or release the +5V.

<br><img width="400" height="400" src="table.jpeg">

#### Test 2
1. Plug the + end of the buzzer wire into the breadboard function generator (start with the TTL input).
2. Play with the frequency knobs or buttons. What do you observe about the buzzer as the frequency changes? <br>

https://github.com/mlcourses/lab-4-blog-post-AdvancedUno/assets/108073642/56b10f36-0d01-4c50-a025-fa821a7e2ca8


#### Test 3
1. Plug the + end of the buzzer wire into Arduino pin 13.
2. Wire the Arduino GND to the ground on the breadboard.
3. Type and upload the following program. What do you observe?
4. What happens if you alter the value for p? Try values between 1 and 5. Notice that the code has a flag to
prevent the buzzer segment from running more than once. For convenience, you can hit the reset button on
the Arduino to reboot it, which will rerun the program without having to reprogram the board.
##### Note: Copy the following code and test!
```
#define BUZZER 13
int once = 0;
void setup ()
{
   pinMode(BUZZER,OUTPUT);
   Serial.begin(9600);
   Serial.println("Start");
}
void loop ()
{
   int p = 3;
   int i;
   if ( !once )
   {
      Serial.println("Starting buzzer");
      for ( i = 0; i < 500; i++ )
      {
         digitalWrite(BUZZER,HIGH);
         delay(p);
         digitalWrite(BUZZER,LOW);
         delay(p);
      }
      once = 1;
      Serial.println("Stopping buzzer");
   }
}
```

https://github.com/mlcourses/lab-4-blog-post-AdvancedUno/assets/108073642/b6ee0366-96d4-41c3-9aa7-7172dc3394a9





#### Test 4
##### Note: Copy the following code and test!
```
#define BUZZER 13
void setup ()
{
   pinMode(BUZZER,OUTPUT);
   Serial.begin(9600);
   Serial.println("Start");
}
void loop ()
{
   int f1 = 3000;
   int f2 = 1000;
   tone(BUZZER,f1);
   delay(1000);
   tone(BUZZER,f2);
   delay(1000);
}
```

https://github.com/mlcourses/lab-4-blog-post-AdvancedUno/assets/108073642/0c54f736-18b1-4ddd-8571-a6a27108c60c

<br>
<br>

## 2. Ultrasonic Sensor


### 0 About
Before we start with the design challenge, it is important to understand each device we will use before we combine them. First, we will understand the ultrasonic sensor (aka sonar detector). This device records distance by sending out an ultrasonic ping and measures the time it takes for the ping to return.

#### Materials
- Arduino Uno or compatible board
- Breadboard
- Wires
- ultrasonic sensor
- Computer with Arduino IDE installed

 
### 1. Project Step
Begin by plugging in your sensor to the breadboard as such
<br><img width="400" src="IMG_0408.JPG">
<br> - After this you will then need to power it to the breadboard by plugging the + pin into the 5v pin on the breadboard and the - pin to the GRN pin on the breadboard.
<br><img width="400" src="IMG_0371.JPG">
<br> - After this we will connect the TRIG pin to pinhole 13 on the Arduino and the ECHO pin to pin 2 on the Arduino. TRIG is what turns on the sonar device and ECHO is what reads the echo.
<br><img width="400" src="IMG_0411.JPG">
<br> - After you have wired the sensor like this you are ready to test it.


### 2. Testing
The following Arduino code will help you in your testing.
```
#define TRIG 13
#define ECHO 2
void setup ()
{
pinMode(TRIG,OUTPUT);
pinMode(ECHO,INPUT);
Serial.begin(9600);
Serial.println("Start");
}
void loop ()
{
Serial.println("Initiating Reading");
digitalWrite(TRIG,HIGH);
delay(10);
digitalWrite(TRIG,LOW);
int distance = pulseIn(ECHO,HIGH)/2;
distance = distance / 29; // tuning parameter
Serial.print("Distance in cm is ");
Serial.println(distance);
delay(2000); // wait 2 seconds before next reading
}
```

<br>This code is first defining the TRIG pin and the ECHO pins. We then set the TRIG as an input and ECHO as an output.
For this project, we tuned the sensor and adjusted the input signal value to read the accurate measurement in the unit of cm.

https://github.com/mlcourses/lab-4-blog-post-AdvancedUno/assets/108073642/ce3c92ad-c736-440a-9fc8-727ebc676e04



## Distance Detector
### 0 About
For this distance detector, we will be designing a device that detects how far away something is and changes pitch based on the distance. <br>
We will be combining the ultrasonic sensor and the buzzer together.<br>
### Project Step
The wiring for the ultrasonic sensor will not change. The TRIG pin will still be pin 13 and ECHO will stay pin 2. The Vcc and GND will have the same wiring on the Arduino as well.<br>
The buzzer from the first section will also be attached to the breadboard as well with its positive side wired to pin 10 and its ground wired to the same GND pin on the Arduino that the ultrasonic sensor. 
<br><img width="400" src="IMG_0424.JPG"><br>
<br>
This is the Arduino code that we will use.
```
#define TRIG 13
#define ECHO 2
#define BUZZER 4
void setup ()
{
pinMode(TRIG,OUTPUT);
pinMode(ECHO,INPUT);
pinMode(BUZZER,OUTPUT);
Serial.begin(9600);
Serial.println("Start");
}
void loop ()
{
Serial.println("Initiating Reading");
digitalWrite(TRIG,HIGH);
delay(10);
digitalWrite(TRIG,LOW);
int distance = pulseIn(ECHO,HIGH)/2;
distance = distance / 29; // tuning parameter
Serial.print("Distance in cm is ");
Serial.println(distance);
tone(BUZZER,distance*50);
delay(100);
```
<br>
This is the ultrasonic sensor code with the addition of pin 4 being a buzzer pin that has a tone function being applied to it based on the distance that the ultrasonic sensor is reading.<br>

### Testing 
Testing is almost the same as the regular ultrasonic sensor except that you're checking if the pitch increases and decreases correctly.<br>

https://github.com/mlcourses/lab-4-blog-post-AdvancedUno/assets/108073642/e0faec69-4cfa-4f30-b43f-e10c971b1be8

<br>

https://github.com/mlcourses/lab-4-blog-post-AdvancedUno/assets/108073642/69e6a3d6-d90c-482d-a196-a021a301e326

<br>

https://github.com/mlcourses/lab-4-blog-post-AdvancedUno/assets/108073642/38c2daf2-271b-4b9b-8fb1-391f7bd3b5e4

<br>

### Something Extra
Beyond just the base distance detector, we also built a similar detector that would play multiple tones one after another.<br>
To do this we wired up 4 more buzzers to pins 4, 6, 8, and 12 as well as 10.<br>

<br>
This is the code we used to make it run.<br>

```
#define TRIG 13
#define ECHO 2
#define BUZZER_1 4
#define BUZZER_2 6
#define BUZZER_3 8
#define BUZZER_4 10
#define BUZZER_5 12
void setup ()
{
pinMode(TRIG,OUTPUT);
pinMode(ECHO,INPUT);
pinMode(BUZZER_1,OUTPUT);
pinMode(BUZZER_2,OUTPUT);
pinMode(BUZZER_3,OUTPUT);
pinMode(BUZZER_4,OUTPUT);
pinMode(BUZZER_5,OUTPUT);
Serial.begin(9600);
Serial.println("Start");

}
void loop ()
{
Serial.println("Initiating Reading");
digitalWrite(TRIG,HIGH);
delay(10);
digitalWrite(TRIG,LOW);
int distance = pulseIn(ECHO,HIGH)/2;
distance = distance / 29; // tuning parameter
Serial.print("Distance in cm is ");
Serial.println(distance);
noTone(BUZZER_5);
tone(BUZZER_1,distance*100);
delay(100);
noTone(BUZZER_1);
tone(BUZZER_2,distance*80);
delay(100);
noTone(BUZZER_2);
tone(BUZZER_3,distance*60);
delay(100);
noTone(BUZZER_3);
tone(BUZZER_4,distance*40);
delay(100);
noTone(BUZZER_4);
tone(BUZZER_5,distance*20);
delay(100); 
}
```
<br>This code has 4 more buzzer pins and uses the noTone function to stop the previous tone before the next one starts.<br>

https://github.com/mlcourses/lab-4-blog-post-AdvancedUno/assets/108073642/13135ea7-bc68-4bf5-b28d-5b0b9f485ead

<br>


# Conclusion

This lab allowed us to get a deeper understanding of sensors and actuators such as buzzers and ultrasonic sensors.
By using an Arduino device and circuit, we created tools that may have practical use in our daily lives instead of just wiring circuits and testing. For the last component of the lab, we practiced how to combine two or more devices and tools to create more complex and useful devices that can be good practice for future labs and even for future careers. 













