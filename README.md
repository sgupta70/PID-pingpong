# PID-pingpong
## Description 
For this project we were assigned to design, build, and program a device that uses PID feedback control. We decided that we would use PID to keep a ping-pong ball floating in a steady position. We are using a motor which works as a fan that will increase or decrease its speed depending on the distance from a sensor to keep it in one place.

## Goal/Success Statement 
Our goal for this project was to use PID feedback to control a motor that would act like a fan, the fan would then blow a fan to a steady position and the PID feedback would control it giving the an the power it needed to stay at the set point. Our project is successful when we get a pingpong ball to stay in a steady, controlled position at the set point. 

## Plan/Schedule 
Week #1 (17-21): start code, get the sensor code working/start CAD                                                                                                       
Week #2 (24-28): figure out how to get the fan working/ continue working on CAD                                                                                           
Week #3 (1-5): continue code and CAD hopefully CAD is pretty much done                                                                                                   
Week #4 (8-12): hopefully print and start to assemble, make sure code is working                                                                                         
Week #5 (15-19): polish and clean up make sure everything is working well


## List of Materials 
- 3D printed parts
- Acrylic 
- Motor 
- Ultra-sonic Sensor 
- Wires
- Battery (battery pack) 
- Metro Express
- Clear Plastic Sheet 
- Screws

## Wiring 

![Screenshot (26)](https://github.com/sgupta70/PID-pingpong/assets/71406905/25d1695b-980b-4c63-9e12-51ca7de6ca46)

This is the project wiring. The black part with an N represents a large transistor. It is powered by a 9V battery pack.

## Code 
```
#Sahana Gupta 
#Ping-Pong 
#control a ping pong ball using PID to control a motor and a sensor 

import time
import adafruit_hcsr04
import simpleio
import analogio
import pwmio
import board
from PID_CPY import PID
pid = PID(-2000.0, -120.0, -600.0, setpoint=30.0)
pid.output_limits = (15000, 65000)

sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D5, echo_pin=board.D6)
pot = analogio.AnalogIn(board.A2)
motor = pwmio.PWMOut(board.D8)
while True:
        try:
            distance = sonar.distance

        except RuntimeError:
            distance = 0
            print("Retrying!")
        time.sleep(0.01)
        motor_speed = int(pid(distance))
        #motor_speed = pot.value # both of these values are 16 bit so no mapping is needed
        #print(f"Speed: {motor_speed}")
        p,i,d = pid.components
        print("Distance: ", distance, " \t Speed: ",motor_speed, p, i, d)
        motor.duty_cycle = motor_speed

```


## Design 
 <img src="https://github.com/sgupta70/PID-pingpong/assets/71406905/65cda6bc-3e93-4228-a363-448829e8bec3.png" style ="width:35%">
 <img src="https://github.com/sgupta70/PID-pingpong/assets/71406905/7cac6e90-337f-4b94-970d-05e035b17bbe.png" style ="width:35%">
 <img src="https://github.com/sgupta70/PID-pingpong/assets/71406905/ca4ff236-7ea3-4e36-bf20-3890e58e26d8.png" style ="width:35%">
 <img src="https://github.com/sgupta70/PID-pingpong/assets/71406905/3f73d7a6-bd4f-4708-8dad-660b59d8a7e2.png" style ="width:35%">
 
 These are pictures of the final OnShape design from different angles. 
 
 [Link to OnShape document](https://cvilleschools.onshape.com/documents/dff44fc98d8d4c4a7a1a7dcc/w/483d116250ae88e43d19ab31/e/f060f7d074c5ca5ca4689b35)

## Pictures

 <img src="https://github.com/sgupta70/PID-pingpong/assets/71406905/d5d351da-aad7-45b3-ad70-eadce99d5755.png" style ="width:50%">
 
 This is a picture of the full design printed, wired, and put together.
 
![ezgif com-gif-maker (1)](https://github.com/sgupta70/PID-pingpong/assets/71406905/c0947d23-c654-4633-b2e8-995993a2d52a)

This is a video of the design, code, and wiring working to keep the ball in a steady position. The position is marked by the two orange rings around the outside of the tube.

## Problems/Limitations

Starting this porject we had a pretty set idea on what we wanted to do, originally we were gonna use a computer fan but we realized that it wouldn't be strong enough to lift the ping-pong ball. This wasn't a huge problem because Mr. Dierof gave us a fan that he made whihc was very strong. We did have to switch our CAD design a little bit but it wasn't terrible. On the code side of things I started with using old code that I had already used for past projects for the potentiometer and ultra-sonic sensor. This helped a lot and once I was able to get the fan working everything came pretty easy. It was our first time using PID so it ws a little hard to understand in the beginning but by the end we were able to get the correct values to keep the ball steady. 


## Reflection

This project was pretty simple to design and build, but our first main issue was not having a fan that was strong enough to lift the ball. This was fixed with [Mr.Deirof's fan design](https://cvilleschools.onshape.com/documents/a12315ff8814f391ded597a0/w/01d64ee189f5fd2a55fd9170/e/7d11469ab6277ca4e45af74b) on Onshape, and creating a custom nosel to attach the tube to the fan. Due to the tube causing the fan to not be able to balance and stand on its own, we designed a base with feet to help support and stablize it. The hardest part of this assignment was the code. After figuring out how to get the DC motor (the fan motor) to change speed using a potentiometer, we attached an untrasonic sensor to the top, reading and printing the distance of the ball. The hardest part was figuring out how to connect the motor speed with the read distance using PID. After getting lots of help from the internet and our teachers, we were able to get the PID added. This code prints the fan speed adn the distance of the ball in the tube. With all of the knowlage we gained on this project, making something similar to it again will be much easier. We are overall very happy with how presise this project turned out. 

