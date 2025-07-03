# Ball Tracking Robot
I made a Catmobile. Powered by Raspberry Pi and Python, it uses a camera, ultrasonic sensors, motor drivers, motors, and servos to autonomously navigate through obstacles with ease and get to the red ball, even in the dark - and when it's there, it holds onto it! Not only is this smart robot made to the highest efficiency, it's designed with silly features that make it so much more friendly!

```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Noah M | Gretchen Whitney High School | Electrical Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


After these three weeks, I am very satisfied with how the robot turned out. 

  Since the last milestone, I 3D modeled and printed the claw and shell of my robot, and attached it using tape. I used specific measurements to appropiately organize each part, and luckily, my first print allowed each part to fit seamlessly. Using SG90 servos, I embedded more code for the claw function, and together, the robot was able to grab the ball. For the final part, I inserted a flashlight; now it was able to work in the dark. 

  My biggest challenges mainly included the coding aspect of the project. It was a steep learning curve of working with the raspberry pi and electrical devices through code mostly by myself, as I had to experiment and research countless times. My biggest triumph was giving life to my robot; I was able to apply my own skills and create something that I am proud of.

  The main takeaways from the program were how many electrical devices - raspberry pi, breadboards, servos, motor drivers, ultrasonic sonars, and much more - and the code for running the robot work. I learned the importance of not giving up and learning from my mistakes to reiterate and improve.

  In the future, I hope to expand my knowledge on engineering, develop my skills, and seek electrical engineering in college.

Testing the servos:

```python

import pigpio
import time

RC = 16
LC = 12


pi = pigpio.pi()

while True:
    control = input()
    if "grab" in control:
        pi.set_servo_pulsewidth(LC, 1100)
        pi.set_servo_pulsewidth(RC, 2000)
    elif "rest" in control:
        pi.set_servo_pulsewidth(LC, 2000)
        pi.set_servo_pulsewidth(RC, 1100)
        pi.stop()
        break


```


# Second Milestone


<iframe width="560" height="315" src="https://www.youtube.com/embed/u6oXDnZl3_4?si=SSVksMeUt7HxIbfF" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

  Since the last milestone, I've worked tirelessly on completing the baseline project and preparing for a later modification of a claw. Some aspects that I have added include installation and code for ultrasonic sonars and a raspberry pi camera. The sonars calculates the distance of objects in front of it in thousanths of a second; the pi camera updates a livestream in real time displaying what it sees, as well as tracking the appropiate shades of red, grouping the largest areas of red, and calculating the offset of the ball from the center of the frame.

  The hardest part: combining the sonars, camera, and motors together in one piece of code. The main aspects that included this were writing code to bring the robot to line up a few centimeters behind the ball, spin when the ball is not in sight, stop at unusual obstructions, turn to the side from where the ball was last, and, utimately, ensure smooth turns. The robot had a hard time centering the ball; the motors often overresponded to voltage and would overshoot, and the robot would infinitely sway side to side. After many experiments and iterations, I was able to overcome. The most surprising part of this project so far is how I have been able to persevere despite these challenges.

  Before my final milestone, now that it's prepared for a later modification, I will work on my modification and putting in my best effort to give life to my robot.

Testing the sonars:

```python

import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)
Echo1 = 26
Trigger1 = 21
Echo2 = 2
Trigger2 = 3
Echo3 = 9
Trigger3 = 10

def sonar (GPIO_Trigger,GPIO_ECHO):
    start=0
    stop=0
    distance = 1000
    GPIO.setup(GPIO_Trigger, GPIO.OUT)

    GPIO.setup(GPIO_ECHO, GPIO.IN)

    GPIO.output(GPIO_Trigger, False)
    time.sleep(0.01)

    while distance > 5:
        GPIO.output(GPIO_Trigger, True)
        time.sleep(0.00001)
        GPIO.output(GPIO_Trigger, False)
        begin = time.time()
        while GPIO.input(GPIO_ECHO) == 0 and time.time()<begin+0.05:
            start = time.time()
        while GPIO.input(GPIO_ECHO) == 1 and time.time()<start+0.1:
            stop = time.time()
        elapsed = stop - start
        distance = elapsed * 34000/2
        return distance

for i in range(1,200):
    distance = sonar(Trigger1, Echo1)
    print("right: ", distance)
    distance = sonar(Trigger3, Echo3)
    print("front: ", distance)
    distance = sonar(Trigger2, Echo2)
    print("left: ", distance)
    print("\n")
    time.sleep(0.5)

```

Testing the camera:

```python

#!/usr/bin/python3
import time

from picamera2 import Picamera2
from picamera2.encoders import H264Encoder
from picamera2.outputs import FfmpegOutput

picam2 = Picamera2()
video_config = picam2.create_video_configuration()
picam2.configure(video_config)

encoder = H264Encoder(10000000)
output = FfmpegOutput('test.mp4', audio=True)

picam2.start_recording(encoder, output)
time.sleep(10)
picam2.stop_recording()

```

# First Milestone


<iframe width="560" height="315" src="https://www.youtube.com/embed/D7zO6I78JUM?si=T224gci5G32yubB_" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


  The ball-tracking robot utilizes two mechanics - a camera and ultrasonic sonars - to evaluate the distance and color of objects through sonar detection and image processing, while sending voltage to its two motors that give it a full range of motion; in total, these functions work through implementing code that sends commands to the Raspberry Pi. 

  The current stage of my robot is that while its base/shell is constructed, I wired a Raspberry Pi to a motor driver module through female to male connectors via a breadboard in the middle, which, through code, allows me to control the movement of the robot's wheels. When running the code through VS Code, the robot remains at rest unless acted upon; therefore, I can write certain inputs into the terminal that give me full control of the robot's direction. Separately, I worked on flickering LED lights in order to test the functionality of my Raspberry Pi and deepen my knowledge on its process. 

Testing the LEDs:

```python

  import RPi.GPIO as GPIO
  import time
  
  leds_number = 18
  GPIO.setmode(GPIO.BCM)
  
  def flicker(leds_number):
      GPIO.setup(leds_number, GPIO.OUT)
      print("LED On")
      GPIO.output(leds_number,GPIO.HIGH)
      time.sleep(0.5)
      print ("Led Off")
      GPIO.output(leds_number, GPIO.LOW)
      time.sleep(0.5)
  
  for i in range (10):
      flicker(leds_number)
      leds_number = 21
      flicker(leds_number)
      leds_number = 26
      flicker(leds_number)
      leds_number = 18

```

Testing the motors:

```python

import RPi.GPIO as GPIO
import time

# Define GPIO pins for motor
# LMC - Left Motor clockwise, RMCC - Right Motor Counter-cloclwise
LMCC = 15
LMC = 20
RMCC = 6
RMC = 19

#Turn motors off
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)
for pin in [LMCC, LMC, RMCC, RMC]:
    GPIO.setup(pin, GPIO.OUT)

# PWM at 100 Hz
PWM1A = GPIO.PWM(LMCC, 100)
PWM1B = GPIO.PWM(LMC, 100)
PWM2A = GPIO.PWM(RMCC, 100)
PWM2B = GPIO.PWM(RMC, 100)

PWM1A.start(0)
PWM1B.start(0)
PWM2A.start(0)
PWM2B.start(0)

def RMforward(speed=100):
    PWM1A.ChangeDutyCycle(0)
    PWM1B.ChangeDutyCycle(speed)

def RMbackward(speed=100):
    PWM1A.ChangeDutyCycle(speed)
    PWM1B.ChangeDutyCycle(0)

def LMforward(speed=100):
    PWM2A.ChangeDutyCycle(0)
    PWM2B.ChangeDutyCycle(speed)

def LMbackward(speed=100):
    PWM2A.ChangeDutyCycle(speed)
    PWM2B.ChangeDutyCycle(0)

def stop():
    for pwm in [PWM1A, PWM1B, PWM2A, PWM2B]:
        pwm.ChangeDutyCycle(0)

while(1):
    control = input()
    if "forward" in control:
        LMforward(50)
        RMforward(50)
        time.sleep(0.5)
        stop()
    elif "backward" in control:
        RMbackward(40)
        LMbackward(40)
        time.sleep(0.5)
        stop()

    elif "left" in control:
        LMbackward(40)
        RMforward(40)
        time.sleep(0.5)
        stop()

    elif "right" in control:
        RMbackward(40)
        LMforward(40)
        time.sleep(0.5)
        stop()
        
    elif "leave" in control:
        break


GPIO.cleanup()

```

  I've faced harsh technical challenges that required several hours of debugging in order to work around them. For instance, I struggled with establishing a connection between my Raspberry Pi and computer as a result of my computer's inability to connect to a network wirelessly. Therefore, I connected it to an ethernet cable; however, I couldn't find out which network it belonged to. Because the Raspberry Pi requires a wireless connection (rather than a wired one, which would not be sustainable for when I complete the robot), I manually logged into different networks through its desktop mode to test whether it could establish a connection. 

  My hope for this project is to expand beyond the blueprint and implement my own modifications to bring the robot to life. 

# Schematics 

![Screenshot 2025-07-03 133130](https://github.com/user-attachments/assets/e93e210a-6a49-411a-a349-890bc4a049d1)

```
Base Foundation

```


![Screenshot 2025-07-03 133205](https://github.com/user-attachments/assets/f7333f64-8649-4047-a288-508dd6124013)

```

Attachable Back End

```
 
![Screenshot 2025-07-03 133142](https://github.com/user-attachments/assets/3839d2cd-ea21-49de-8103-2c415dcaa9a0)

```

Lid

```

![Screenshot 2025-07-03 133223](https://github.com/user-attachments/assets/7f494a91-536b-40ab-a532-1a2c3e6c1aed)

```

Claw

```

# Final Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```python

  from flask import Flask, Response, render_template_string
  from picamera2 import Picamera2
  from datetime import datetime
  import RPi.GPIO as GPIO
  import pigpio
  import time
  import cv2
  import numpy as np
  
  #Marks which side the ball was seen last
  marker = 0
  
  # Define GPIO pins for motor
  # LMC - Left Motor clockwise, RMCC - Right Motor Counter-cloclwise
  LMCC = 15
  LMC = 20
  RMCC = 6
  RMC = 19
  
  # Define GPIO pins for ultrasonic sensors
  Echo1 = 26
  Trigger1 = 21
  Echo2 = 2
  Trigger2 = 3
  Echo3 = 9
  Trigger3 = 10
  
  # Define GPIO pins for servos
  RC = 16
  LC = 12
  pi = pigpio.pi()
  
  #Set up Picamera settings
  app = Flask(__name__)
  picam = Picamera2()
  picam.configure(picam.create_preview_configuration(main={"format":"BGR888", "size": (640, 480)}))
  picam.start()
  FRAME_WIDTH = 640
  CENTER_X = FRAME_WIDTH // 2
  
  #Turn motors off
  GPIO.setmode(GPIO.BCM)
  GPIO.setwarnings(False)
  for pin in [LMCC, LMC, RMCC, RMC]:
      GPIO.setup(pin, GPIO.OUT)
  
  # PWM at 100 Hz
  PWM1A = GPIO.PWM(LMCC, 100)
  PWM1B = GPIO.PWM(LMC, 100)
  PWM2A = GPIO.PWM(RMCC, 100)
  PWM2B = GPIO.PWM(RMC, 100)
  
  PWM1A.start(0)
  PWM1B.start(0)
  PWM2A.start(0)
  PWM2B.start(0)
  
  
  def RMforward(speed=100):
      PWM1A.ChangeDutyCycle(0)
      PWM1B.ChangeDutyCycle(speed)
  
  def RMbackward(speed=100):
      PWM1A.ChangeDutyCycle(speed)
      PWM1B.ChangeDutyCycle(0)
  
  def LMforward(speed=100):
      PWM2A.ChangeDutyCycle(0)
      PWM2B.ChangeDutyCycle(speed)
  
  def LMbackward(speed=100):
      PWM2A.ChangeDutyCycle(speed)
      PWM2B.ChangeDutyCycle(0)
  
  def stop():
      for pwm in [PWM1A, PWM1B, PWM2A, PWM2B]:
          pwm.ChangeDutyCycle(0)
  
  #Function to read distance from ultrasonic sensors
  def sonar (GPIO_Trigger,GPIO_ECHO):
      #Define variables
      start=0
      stop=0
      distance = 1000
  
      #Set GPIO pins
      GPIO.setup(GPIO_Trigger, GPIO.OUT)
  
      GPIO.setup(GPIO_ECHO, GPIO.IN)
  
      #Turn off the trigger
      GPIO.output(GPIO_Trigger, False)
      time.sleep(0.01)
  
      while distance > 5:
          #Ultrasonic sensor sends a signal
          GPIO.output(GPIO_Trigger, True)
          time.sleep(0.00001)
          GPIO.output(GPIO_Trigger, False)
          #Variable for current time
          begin = time.time()
          #Measuring the start - when the signal is sent
          while GPIO.input(GPIO_ECHO) == 0 and time.time()<begin+0.05:
              start = time.time()
          #Measuring the stop - when the echo from the signal is received
          while GPIO.input(GPIO_ECHO) == 1 and time.time()<start+0.1:
              stop = time.time()
          #Calculate the distance
          elapsed = stop - start
          distance = elapsed * 34000/2
          return distance
  
  def claw():
      print("3. Grab")
      pi.set_servo_pulsewidth(LC, 1100)
      pi.set_servo_pulsewidth(RC, 2000)
      time.sleep(2)
      pi.set_servo_pulsewidth(LC, 2000)
      pi.set_servo_pulsewidth(RC, 1100)
  
  #Function to move the car every thousandth of a second
  def drive(offset, area):
      #distance from right ultrasonic sensor
      distanceR = sonar(Trigger1, Echo1)
      #distance from left ultrasonic sensor
      distanceL = sonar(Trigger2, Echo2)
      #distance from front ultrasonic sensor
      distanceF = sonar(Trigger3, Echo3)
  
      global marker
  
      if(area < 5000):
          print("0. Looking")
          if (marker <= 0):
              RMforward(30.8)
              LMbackward(30.8)
              time.sleep(0.0001)
              print("i turn left now")
          elif (marker > 0):
              RMbackward(30.8)
              LMforward(30.8)
              time.sleep(0.0001)
              print("i turn right now")
          return
      else:
          print("1. Object found")
          if distanceR > 20 and distanceL > 20 and distanceF > 20:
              #print("DRIVE MODE ENABLED")
              if(offset>50):
                  RMforward(40)
                  LMforward(40)
                  time.sleep(0.0001)
                  RMforward(30)
                  LMforward(40)
                  time.sleep(0.0001)
                  RMforward(30)
                  LMforward(45)
                  time.sleep(0.0001)
                  #print("RIGHT")
              elif(offset<-50):
                  RMforward(40)
                  LMforward(40)
                  time.sleep(0.0001)
                  RMforward(40)
                  LMforward(30)
                  time.sleep(0.0001)
                  RMforward(45)
                  LMforward(30)
                  time.sleep(0.0001)
                  #print("LEFT")
              elif(offset != 0):
                  LMforward(30)
                  RMforward(30)
                  time.sleep(0.0001)
                  #print("FORWARD")
              else:
                  stop()
                  #print("STOP")
          elif (distanceL <= 20 or distanceR <= 20):   
              if (area > 3000):
                  print("Extra: Backing up")
                  if (distanceL > 20):
                      RMbackward(20)
                      LMbackward(20)
                      time.sleep(0.0002)
                      RMbackward(40)
                      LMbackward(40)
                      time.sleep(0.0003)
                      RMbackward(50)
                      LMbackward(40)
                      time.sleep(0.0001)
                      RMbackward(60)
                      LMbackward(40)
                      time.sleep(0.0001)
                  
                  elif (distanceR > 20):
                      RMbackward(20)
                      LMbackward(20)
                      time.sleep(0.0002)
                      RMbackward(40)
                      LMbackward(40)
                      time.sleep(0.0003)
                      RMbackward(40)
                      LMbackward(50)
                      time.sleep(0.0001)
                      RMbackward(40)
                      LMbackward(60)
                      time.sleep(0.0001)
                  
              else:
                  print("Wait for procedure")
                  stop()
          elif(distanceL > 20 and  distanceF < 8 and distanceR > 20):
              print("2. In optimal position")
              print("right: ", distanceR)
              print("front: ", distanceF)
              print("left: ", distanceL)
              stop()
              claw()
          elif(8 < distanceF < 20):
              print("Extra: Just a little closer")
              LMforward(35)
              RMforward(35)
              time.sleep(0.0001)
  
          marker = offset
      return
  
  #Function to find red (and its area) in frame and set up website visuals
  def track_object(frame):
      hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)
      lower_red1 = np.array([0,100,30])
      upper_red1 = np.array([10,255,255])
      lower_red2 = np.array([160, 100, 30])
      upper_red2 = np.array([179, 255, 255])
  
      mask1 = cv2.inRange(hsv, lower_red1, upper_red1)
      mask2 = cv2.inRange(hsv, lower_red2, upper_red2)
      mask = cv2.bitwise_or(mask1, mask2)
  
      mask = cv2.erode(mask, None, iterations=2)
      mask = cv2.dilate(mask, None, iterations=2)
  
      contours, _ = cv2.findContours(mask, cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_SIMPLE)
      offsetPos = 0
      global area
      area = 0
  
      if contours:
          area = cv2.contourArea(max(contours, key=cv2.contourArea))
          largest = max(contours, key=cv2.contourArea)
          M = cv2.moments(largest)
          if M["m00"] > 0:
              centre_x = int(M["m10"] / M["m00"])
              centre_y = int(M["m01"] / M["m00"])
              offset = centre_x - CENTER_X
              offsetPos = offset
  
              if abs(offset) < 30:
                  position = "Centered"
              elif offset < 0:
                  position = "Left"
              else:
                  position = "Right"
  
              cv2.drawContours(frame, [largest], -1, (0, 255, 0), 2)
              cv2.circle(frame, (centre_x, centre_y), 5, (255, 0, 0), -1)
              cv2.putText(frame, f"Offset: {offset}({position})", (10, 30), 
              cv2.FONT_HERSHEY_SIMPLEX, 0.7, (255, 255, 255), 2)
      return frame, offsetPos, area
  
  #Function to generate frames for the video stream
  def generate_frames():
      while True:
          frame = picam.capture_array()
          frame = cv2.cvtColor(frame, cv2.COLOR_RGB2BGR)
          frame, offset, area = track_object(frame)
  
          drive(offset, area)
  
          ret, buffer = cv2.imencode('.jpg', frame)
          jpg_frame = buffer.tobytes()
          yield (b'--frame\r\n'
                  b'Content-Type: image/jpeg\r\n'
                  b'Content-Length: ' + f"{len(jpg_frame)}".encode() 
                  + b'\r\n\r\n' + 
                  jpg_frame + b'\r\n')
  
  #Setting up web browser via HTML
  @app.route('/')
  def index():
          return render_template_string('''
          <html>
              <head><title>Red Ball Tracking Stream</title></head>
              <body>
                  <h2>Live Tracking</h2>
                  <img src="/video_feed">
              </body>
          </html>
          ''')
  
  #Function to handle video feed AND robot functions
  @app.route('/video_feed')
  def video_feed():
      return Response(generate_frames(), mimetype='multipart/x-mixed-replace; boundary=frame')
  
  if __name__ == '__main__':
      app.run(host='0.0.0.0', port=5000)
  
  GPIO.cleanup()

```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
