# PID-pingpong
## Description 
For this project we were assigned to design, build, and program a device that uses PID feedback control. We decided that we would use PID to keep a ping-pong ball floating in a steady position. We are using a motor which works as a fan that will increase or decrease its speed depending on the distance from a sensor to keep it in one place.

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

## Code 
```
#Sahana Gupta 
#Ping-Pong 

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
 
 [Link to OnShapedocument](https://cvilleschools.onshape.com/documents/dff44fc98d8d4c4a7a1a7dcc/w/483d116250ae88e43d19ab31/e/f060f7d074c5ca5ca4689b35)

## Pictures

<img src="blob:chrome-untrusted://media-app/180b72b0-5fcc-4574-a353-9a86c5f4155a" alt="IMG-3467.jpg"/>
## Problems/Limitations 
Starting this porject we had a pretty set idea on what we wanted to do, originally we were gonna use a computer fan but we realized that it wouldn't be strong enough to lift the ping-pong ball. This wasn't a huge problem because Mr. Dierof gave us a fan that he made whihc was very strong. We did have to switch our CAD design a little bit but it wasn't terrible. On the code side of things I started with using old code that I had already used for past projects for the potentiometer and ultra-sonic sensor. This helped a lot and once I was able to get the fan working everything came pretty easy. It was our first time using PID so it ws a little hard to understand in the beginning but by the end we were able to get the correct values to keep the ball steady. 


## Reflection
