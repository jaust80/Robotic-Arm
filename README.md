# Robotic-Arm

We will be documenting our progress throughout our project.


# Prototype designs

We originally settled on using carbon fiber for the rods on the arm, however it was much more expensive and ended up not being worth it because of the strength and price of the acrylic already in the lab. 

![download](https://user-images.githubusercontent.com/71342179/151813229-076533c0-4f9b-4cd5-8b17-451c890c152f.jpg)

# Servo Holder

## Onshape Model![servo holder](https://user-images.githubusercontent.com/71342179/151715472-0ab765e4-2eed-473a-b299-8699befc805a.PNG)
![servo](https://user-images.githubusercontent.com/71342179/151715729-b2421684-db5e-498a-9904-1c4eaa2ae02a.png)

## Information / Process

The first part we started to design was the servo holder. An immediate issue we faced is how we were going to insert the model of the servo into the actual design (this would be used for scaling.) We eventually achieved this by navigating to the shared parts and inserting the servo into the design. To get the correct dimensions we utilized the Use tool (The definition of the Use tool as stated on onshape is "Project edges or faces of an existing part or sketch onto the active sketch plane.) The next issue was how we were going to get the servo into the physical part. We decided on having the servo slide upwards into the part by removing slots where other components like wiring might get in the way (this is shown in the second picture above)


# Proof of concept

## Onshape Model 
![basic hook](https://user-images.githubusercontent.com/71342179/151715843-d2c4526a-2fc1-4f46-9648-94be1aae75da.png)
![IMG_1706](https://user-images.githubusercontent.com/71342179/151716107-035d8401-7f1f-4471-910f-bb83f82dabac.jpg)
![IMG_1708](https://user-images.githubusercontent.com/71342179/151716212-1a70c00b-2ffe-455c-a631-093550a1532f.jpg)

## Code
```python
import time
import board
import pwmio
import servo

# create a PWMOut object on Pin A2.
pwm = pwmio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50)

# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)

while True:
    for angle in range(0, 180, 5):  # 0 - 180 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.05)
    for angle in range(180, 0, -5):  # 180 - 0 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.05)

```
## Information / Process

On the last day of the quarter January 28 2022 we ran into a major problem of not having a proper proof of concept. We immediately rushed to put something together which consisted of a makeshift acrylic hook and old servo code. However the code we had used on the old servo project had become outdated and we had to find and download the newer correct libraries to get it to run again. When the code finally began to work the was another issue that was presented, there was not enough power going to the servo and we had to use a modified 6V battery pack to get it to run the way we had hoped. The next step was to see how much weight it could which was all but succesful. Initially we tested the strength of the hook with a bag and a 5.6 pound aluminum block. This caused the servo to stall out and we came to the conclusion that with the current design it could only hold up to about 3 pounds
