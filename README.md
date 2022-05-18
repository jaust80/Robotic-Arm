# Robotic-Arm

We will be documenting our progress throughout our project.


Link to, or description of the planning that went into the project, design decisions, and engineering details
Materials used (as a Bill Of Materials)
Wiring diagram of your circuit
Commented code
Captioned CAD renderings
Actual photos and/or video (well lit and in focus)
Your process or a schedule of how you spent your time
Discussion of problems, errors, miscalculations, and missteps and how you overcame them
Remember to pass on the big nuggets of wisdom you picked up as you did this project
The goal of these nuggets is to help the reader have an easier time than you did, or do a better project than yours.
If you didn't finish, please add an obituary, detailing what you'd do if you picked this project back up, and anything you'd have done differently.


# Prototype designs

We originally settled on using carbon fiber for the rods on the arm, however it was much more expensive and ended up not being worth it because of the strength and price of the acrylic already in the lab. 

![download](https://user-images.githubusercontent.com/71342179/151813229-076533c0-4f9b-4cd5-8b17-451c890c152f.jpg)

# Servo Holder

## Description

This part will be used as a case that fits over the servo to hold it and all its wiring in place while the arm is in use.

## Criteria & Constraints



## Bill of Materials

    •Screws for securing the holder
    •Metal gear servos

## Documentation/Design
The first part we started to design was the servo holder. An immediate issue we faced is how we were going to insert the model of the servo into the actual design (this would be used for scaling.) We eventually achieved this by navigating to the shared parts and inserting the servo into the design. To get the correct dimensions we utilized the Use tool (The definition of the Use tool as stated on onshape is "Project edges or faces of an existing part or sketch onto the active sketch plane.) The next issue was how we were going to get the servo into the physical part. We decided on having the servo slide upwards into the part by removing slots where other components like wiring might get in the way.

## Onshape Model

### Front view of the Onshape model![servo holder](https://user-images.githubusercontent.com/71342179/151715472-0ab765e4-2eed-473a-b299-8699befc805a.PNG)

### Side view of the Onshape model![servo](https://user-images.githubusercontent.com/71342179/151715729-b2421684-db5e-498a-9904-1c4eaa2ae02a.png)


# Hook/Rod

## Description

Rod attached to the servo horn that is used to hold the grocery bags

## Criteria & Constraints


## Bill of Materials

    •Servo holder that was designed previously
    •Properly fitted horn for the servo
    •Screws to secure the hook to the servo

## Documentation/Design

The rod and hook took a little time to get a good model of, but in the end we ended up being happy with the design. We started the hook with rectangular sketch on the servo double horn, then extruded it so it was a rectangular box. In the middle of the box, we sketched a circle and extruded that out 160mm. At the end of the circle extrude we sketched the hook and morphed it into what we thought was the best design. After this, we sketched circles on the rectangular box for the screw holes. We made the dimensions of the circles the same as the holes on the horn in order to get even screw holes. Though we did have trouble sketching the circles, we got around it by using the hook's rectangular box as the sketch face and not the servo horn. If we used the servo horn as the sketch face, the extrude would not work and ended up causing more problems. The second picture listed above is what the hook looks like when it is attached to the servo. The design is what we think is the best fit for us. 

## Onshape Model

### Hook by itself![Rod With Hook](https://user-images.githubusercontent.com/90460146/154286836-ec5ebedf-9471-4f4b-84d3-3f1958a75f24.png)

### Hook with servo![Servo with Rod and Hook](https://user-images.githubusercontent.com/90460146/154290177-98077028-bf19-4b5e-8d3f-016543fdb93e.png)






# Proof of concept

## Onshape Model 
![basic hook](https://user-images.githubusercontent.com/71342179/151715843-d2c4526a-2fc1-4f46-9648-94be1aae75da.png)

![Rod With Hook](https://user-images.githubusercontent.com/90460146/154286836-ec5ebedf-9471-4f4b-84d3-3f1958a75f24.png)
![Servo with Rod and Hook](https://user-images.githubusercontent.com/90460146/154289474-ed0a2591-a316-402f-8238-1119df357bf3.png)
![IMG_1706](https://user-images.githubusercontent.com/71342179/151716107-035d8401-7f1f-4471-910f-bb83f82dabac.jpg)
![IMG_1708](https://user-images.githubusercontent.com/71342179/151716212-1a70c00b-2ffe-455c-a631-093550a1532f.jpg)

## Code
```python
# Robot arm program
import time
import board
import pwmio
from adafruit_motor import servo
import digitalio

closedPos = 5
openPos = 130

openState = True
closedState = False

state = closedState
lastButtonState = state

button = digitalio.DigitalInOut(board.D1)
button.direction = digitalio.Direction.INPUT
button.pull = digitalio.Pull.DOWN

# create a PWMOut object on Pin A2.
pwm = pwmio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50)

# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)

def closeServo():
    print("closing")
    global state
    my_servo.angle = closedPos
    state = closedState

def openServo():
    print("opening")
    global state
    my_servo.angle = openPos
    state = openState

while True:
    buttonState = button.value
    print(buttonState, ", servo's state is", state)


    if buttonState is True and lastButtonState is False:

        if state is True:
            print("closing")
            closeServo()
        else:
            print("opening")
            openServo()

    time.sleep(0.1)
    lastButtonState = buttonState
    
```

## Code Description

The code above makes the servo switch from an open to close state with the press of a button. It also prints out the value of the state, meaning if the state is false, it prints out that its false, if it's true, it prints out that its true. If you press the button, the servo horn will move 120° and will be represented by the openState. Once we press it again, it will go back to 0° and be represented by closedState.

## Code Infortmation / Process

While we were trying to figure out the code, we ran into many problems with the code itself. The code was somehow interfering with the wiring and making it so when we pressed the button, it wouldn't switch states. 


## Information / Process

On the last day of the quarter January 28 2022 we ran into a major problem of not having a proper proof of concept. We immediately rushed to put something together which consisted of a makeshift acrylic hook and old servo code. However the code we had used on the old servo project had become outdated and we had to find and download the newer correct libraries to get it to run again. When the code finally began to work the was another issue that was presented, there was not enough power going to the servo and we had to use a modified 6V battery pack to get it to run the way we had hoped. The next step was to see how much weight it could which was all but succesful. Initially we tested the strength of the hook with a bag and a 5.6 pound aluminum block. This caused the servo to stall out and we came to the conclusion that with the current design it could only hold up to about 3 pounds
