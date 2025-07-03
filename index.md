# Ball Tracking Robot
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Noah M | Whtiney Gretchen High School | Electrical Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


After these three weeks, the robot turned out exactly how I planned it from the beginning. 

Since the last milestone, I 3D modeled and printed the claw and shell of my robot, and attached it using tape. I used specific measurements to appropiately organize each part, and luckily, my first print allowed each part to fit seamlessly. Using SG90 servos, I embedded more code for the claw function, and together, the robot was able to grab the ball. For the final part, I inserted a flashlight; now it was able to work in the dark. 

My biggest challenges mainly included the coding aspect of the project. It was a steep learning curve of working with the raspberry pi and electrical devices through code mostly by myself, as I had to experiment and research countless times. My biggest triumph was giving life to my robot; I was able to apply my own skills and create something that I am proud of.

The main takeaways from the program were how many electrical devices - raspberry pi, breadboards, servos, motor drivers, ultrasonic sonars, and much more - and the code for running the robot work. I learned the importance of not giving up and learning from my mistakes to reiterate and improve.

In the future, I hope to expand my knowledge on engineering, develop my skills, and seek electrical engineering in college.


# Second Milestone


<iframe width="560" height="315" src="https://www.youtube.com/embed/u6oXDnZl3_4?si=SSVksMeUt7HxIbfF" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Since the last milestone, I've worked tirelessly on completing the baseline project and preparing for a later modification of a claw. Some aspects that I have added include installation and code for ultrasonic sonars and a raspberry pi camera. The sonars calculates the distance of objects in front of it in thousanths of a second; the pi camera updates a livestream in real time displaying what it sees, as well as tracking the appropiate shades of red, grouping the largest areas of red, and calculating the offset of the ball from the center of the frame.

The hardest part: combining the sonars, camera, and motors together in one piece of code. The main aspects that included this were writing code to bring the robot to line up a few centimeters behind the ball, spin when the ball is not in sight, stop at unusual obstructions, turn to the side from where the ball was last, and, utimately, ensure smooth turns. The robot had a hard time centering the ball; the motors often overresponded to voltage and would overshoot, and the robot would infinitely sway side to side. After many experiments and iterations, I was able to overcome. The most surprising part of this project so far is how I have been able to persevere despite these challenges.

Before my final milestone, now that it's prepared for a later modification, I will work on my modification and putting in my best effort to give life to my robot.


# First Milestone


<iframe width="560" height="315" src="https://www.youtube.com/embed/D7zO6I78JUM?si=T224gci5G32yubB_" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


The ball-tracking robot utilizes two mechanics - a camera and ultrasonic sonars - to evaluate the distance and color of objects through sonar detection and image processing, while sending voltage to its two motors that give it a full range of motion; in total, these functions work through implementing code that sends commands to the Raspberry Pi. 

The current stage of my robot is that while its base/shell is constructed, I wired a Raspberry Pi to a motor driver module through female to male connectors via a breadboard in the middle, which, through code, allows me to control the movement of the robot's wheels. When running the code through VS Code, the robot remains at rest unless acted upon; therefore, I can write certain inputs into the terminal that give me full control of the robot's direction. Separately, I worked on flickering LED lights in order to test the functionality of my Raspberry Pi and deepen my knowledge on its process. 

I've faced harsh technical challenges that required several hours of debugging in order to work around them. For instance, I struggled with establishing a connection between my Raspberry Pi and computer as a result of my computer's inability to connect to a network wirelessly. Therefore, I connected it to an ethernet cable; however, I couldn't find out which network it belonged to. Because the Raspberry Pi requires a wireless connection (rather than a wired one, which would not be sustainable for when I complete the robot), I manually logged into different networks through its desktop mode to test whether it could establish a connection. 

My hope for this project is to expand beyond the blueprint and implement my own modifications to bring the robot to life. 

# Schematics 


![Screenshot 2025-07-03 133205](https://github.com/user-attachments/assets/f7333f64-8649-4047-a288-508dd6124013)
![Screenshot 2025-07-03 133142](https://github.com/user-attachments/assets/3839d2cd-ea21-49de-8103-2c415dcaa9a0)
![Screenshot 2025-07-03 133130](https://github.com/user-attachments/assets/e93e210a-6a49-411a-a349-890bc4a049d1)
![Screenshot 2025-07-03 133223](https://github.com/user-attachments/assets/7f494a91-536b-40ab-a532-1a2c3e6c1aed)

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
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
