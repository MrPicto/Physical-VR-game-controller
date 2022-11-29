# Arduino design (earliest version)

In the original arduino design idea, the heart rate sensor reads the user's heart rate every second and transmits the data to the PC, while also receiving the string "0" from the computer to start the vibration for 0.5 seconds.

The data is transmitted via a Bluetooth sensor. Using the smaller Arduino Nano and the battery, the Arduino device can be made into a wearable sensor. But this design idea was modified later in the step-by-step tests, for reasons that will be explained at the end.

![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)
![Target](https://user-images.githubusercontent.com/92038037/204204410-50c088f9-62d6-4387-aeff-9df4c787888b.png)
![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)

# Reflections on the design process 
#### Q1. What is the best exercise to choose for VR sports？ 
#### Q2. Where to put the heart rate sensor？ 
#### Q3. What type of vibration modules should used? How many?   
![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)


# Q1：What is the best exercise to choose for VR sports？

### Choosing the type of sports game
Examining the VR games currently on the market, most of the games for sports are mainly boxing, rowing, cycling, golf, basketball and table tennis.
- Golf has low consumption (not selected)
- Basketball has high space requirements (not selected)
- Table tennis requires pairing with other players (not selected)
- Rowing and cycling, both of which tend to cause dizziness for the user (not selected)
  
Ultimately, the boxing game was chosen. because two things.
1. the player does not need to move his body much and the area of space used is small.
2. because it does not require frequent position changes, The player is not prone to 3D vertigo. 

![Oculus - Google Chrome 2022_11_28 3_44_55](https://user-images.githubusercontent.com/92038037/204189826-7601735e-7b8d-47fe-92b0-b027068823de.png)

![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)
    

### VR boxing game survey
An examination of 4 VR sports games summarizes several advantages of boxing games.
- Low learning difficulty
- Boxing can be aerobic (as it is inconvenient to do anaerobic exercises while wearing the Oculus and it is easy to sweat and affect your vision)
- The amount of boxing can be quantified and converted into game points to stimulate the user to exercise
Disadvantages of boxing games.
- The VR games currently on the market have a poor sense of combat
- Difficulty level varies, some games are high and some are too low
  
![VR wearable, Online Whiteboard for Visual Collaboration - Google Chrome 2022_11_28 3_51_08](https://user-images.githubusercontent.com/92038037/204190433-6184a0a3-e19d-4262-b178-f5f3384e26dc.png)
![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)



# Q2：Where to put the heart rate sensor？
### Which heart rate sensor to choose 
  
At the very beginning I chose a normal heart rate sensor for testing. But after testing I found that the sensor was not stable. So I chose the model MAX30102, a high precision heart rate sensor. The data test results were highly stable and less costly.
 
  
- [Common heart rate sensors Info](https://lastminuteengineers.com/pulse-sensor-arduino-tutorial/)
- [MAX30102 Sensor Info](https://lastminuteengineers.com/max30102-pulse-oximeter-heart-rate-sensor-arduino-tutorial/)  

![221128-TheBoxingRoom-Layout-04](https://user-images.githubusercontent.com/92038037/204201563-bc020b80-e5c6-40dd-a69c-ae2ef30988a2.png)
![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)
---
### Heart Rate test Coding
```C++
#include <Wire.h>
#include "MAX30105.h"

#include "heartRate.h"

MAX30105 particleSensor;

const byte RATE_SIZE = 4; //Increase this for more averaging. 4 is good.
byte rates[RATE_SIZE]; //Array of heart rates
byte rateSpot = 0;
long lastBeat = 0; //Time at which the last beat occurred

float beatsPerMinute;
int beatAvg;

void setup()
{
  Serial.begin(19200);
  Serial.println("Initializing...");

  // Initialize sensor
  if (!particleSensor.begin(Wire, I2C_SPEED_FAST)) //Use default I2C port, 400kHz speed
  {
    Serial.println("MAX30105 was not found. Please check wiring/power. ");
    while (1);
  }
  Serial.println("Place your index finger on the sensor with steady pressure.");

  particleSensor.setup(); //Configure sensor with default settings
  particleSensor.setPulseAmplitudeRed(0x0A); //Turn Red LED to low to indicate sensor is running
  particleSensor.setPulseAmplitudeGreen(0); //Turn off Green LED
}

void loop()
{
  long irValue = particleSensor.getIR();

  if (checkForBeat(irValue) == true)
  {
    //We sensed a beat!
    long delta = millis() - lastBeat;
    lastBeat = millis();

    beatsPerMinute = 60 / (delta / 1000.0);

    if (beatsPerMinute < 255 && beatsPerMinute > 20)
    {
      rates[rateSpot++] = (byte)beatsPerMinute; //Store this reading in the array
      rateSpot %= RATE_SIZE; //Wrap variable

      //Take average of readings
      beatAvg = 0;
      for (byte x = 0 ; x < RATE_SIZE ; x++)
        beatAvg += rates[x];
      beatAvg /= RATE_SIZE;
    }
  }

  Serial.print(beatAvg);

  if (irValue < 50000)
    Serial.print(" No finger?");

  Serial.println();
}
```
![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)
### Testing different parts of the hand 
After testing the front of the wrist, the back of the wrist and the fingertips, it was concluded that the fingertip data was the most stable.


![221128-TheBoxingRoom-Layout-06](https://user-images.githubusercontent.com/92038037/204210470-6bbf2869-7999-419b-ae7c-c891884edc9a.png)
![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)

# Q3：What type of vibration modules should used? How many?   
### Vibration test Coding 
In the test, the arduino vibrates the motor when the string "1" is sent. This is to feel the difference between the different types and amounts of vibrations.


```C++
char inChar;
int vb = 13;//震动接口 3

void setup() {
  pinMode(vb,OUTPUT);
  digitalWrite(vb,LOW);
  Serial.begin(38400);
}

void loop() {
  while(Serial.available())
  {
    inChar = Serial.read();
    Vibration();
    delay(100);
    digitalWrite(vb,LOW);
  }
}

void Vibration()
{
  if (inChar == '1')
  {
    Serial.println("Arduino says Hi!");
    digitalWrite(vb,HIGH);
    delay(500);
  }else if(inChar == '0')
  {
    Serial.println("Arduino says Bye!");
    digitalWrite(vb,LOW);
  }
}
```


![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)
### Vibration Sensor Vibro Testing 
I found two types of vibration sensors, strapped them to the back of my finger by extension and invited other users to test them together.


![221128-TheBoxingRoom-Layout-08](https://user-images.githubusercontent.com/92038037/204229180-a5dd21b7-2c5d-4141-add7-23df5814e0d7.png)
![221128-TheBoxingRoom-Layout-07](https://user-images.githubusercontent.com/92038037/204229200-06abbac3-6adf-4945-950d-6685f5064fa4.png)


![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)

### Final results 
The final result is that one linear resonant actuator works best, while two sensors cause too much vibration. According to the testers, the coreless vibration motor has a more intense vibration effect than the former, which does not feel like hitting the ball and is uncomfortable.



https://user-images.githubusercontent.com/92038037/204218325-973b99e1-1e5f-4413-8a8f-653ea36336d2.mp4
![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)

# Final Arduino Code
- [GitHub - Scource Code](https://github.com/MrPicto/Physical-VR-game-controller/tree/main/HeartRate_Vibration_Nano)
```C++
#include <Wire.h>
#include "MAX30105.h"
#include "heartRate.h"
MAX30105 particleSensor;

//////////////////////////////////////

const byte RATE_SIZE = 4; //Increase this for more averaging. 4 is good.
byte rates[RATE_SIZE]; //Array of heart rates
byte rateSpot = 0;
long lastBeat = 0; //Time at which the last beat occurred

char inChar;
int vb = 6;//Vibration

float beatsPerMinute;
int beatAvg;

//////////////////////////////////////

void setup()
{
  pinMode(vb,OUTPUT);
  digitalWrite(vb,LOW);
  Serial.begin(38400);
  Serial.println("Initializing...");

  // Initialize sensor
  if (!particleSensor.begin(Wire, I2C_SPEED_FAST)) //Use default I2C port, 400kHz speed
  {
    Serial.println("MAX30105 was not found. Please check wiring/power. ");
    while (1);
  }
  Serial.println("Place your index finger on the sensor with steady pressure.");

  particleSensor.setup(); //Configure sensor with default settings
  particleSensor.setPulseAmplitudeRed(0x0A); //Turn Red LED to low to indicate sensor is running
  particleSensor.setPulseAmplitudeGreen(0); //Turn off Green LED
}

void loop()
{
  long irValue = particleSensor.getIR();

  if (checkForBeat(irValue) == true)
  {
    //We sensed a beat!
    long delta = millis() - lastBeat;
    lastBeat = millis();

    beatsPerMinute = 60 / (delta / 1000.0);

    if (beatsPerMinute < 255 && beatsPerMinute > 20)
    {
      rates[rateSpot++] = (byte)beatsPerMinute; //Store this reading in the array
      rateSpot %= RATE_SIZE; //Wrap variable

      //Take average of readings
      beatAvg = 0;
      for (byte x = 0 ; x < RATE_SIZE ; x++)
        beatAvg += rates[x];
      beatAvg /= RATE_SIZE;
    }
  }

  Serial.print(beatAvg);

  while(Serial.available())
  {
    inChar = Serial.read();
    Vibration();
    delay(100);
    digitalWrite(vb,LOW);
  }
}

void Vibration()
{
  if (inChar == '0')
  {
    //Serial.println("Vibration");
    digitalWrite(vb,HIGH);
    delay(50);
  }
}
```

# Circuit Design 
![221128-TheBoxingRoom-Layout-09](https://user-images.githubusercontent.com/92038037/204229422-d27ca2ec-8b38-4981-987a-8414cd29b598.png)


### Battery 
The Arduino is currently tested at 5V and to power the wearable I compared AA, AAA and coin cell batteries.
In the end, I chose the CR2032 type of coin cell battery. Because of their small size, two coin cell batteries can deliver 9V, and with the addition of a mini560 buck module, the 9V can be reduced to 5V, and the batteries and buck module together are even smaller than two AAA batteries.

![221128-TheBoxingRoom-Layout-10](https://user-images.githubusercontent.com/92038037/204229356-6427478f-804e-4559-8050-df1c309db63d.png)
![221128-TheBoxingRoom-Layout-11](https://user-images.githubusercontent.com/92038037/204229446-ab4d981c-ee84-4774-ba61-f564091ced04.png)
![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)

# Reason for final circuit adjustment 
Later, during the testing of the link between Arduino and Unreal Engine, I found that the Unreal Engine plugin (SerialCOM) for linking to Arduino did not support Bluetooth links, only data port(COM). so I eventually changed the design of the project.

![串口 (2)](https://user-images.githubusercontent.com/92038037/204265019-7e1112ee-9577-4f05-b361-f1142a4e226f.png)
![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)
### Arduino designs(Current) 

![Arduino Xmind](https://user-images.githubusercontent.com/92038037/204230321-5551aca1-db2b-4a53-abe1-98a0e0c6dfb7.png)
![space](https://user-images.githubusercontent.com/92038037/204201699-c11c6809-0efb-486c-8dff-8ceeb41e9ff4.png)



