 # Ball Tracking Robot
Using components like the raspberry pi, sonars and motors, the robot uses them in tandem to track and follow a red ball. Additionally, I added a linear actuator and a relay module to shoot at the ball. 

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Jason M | Lowell Highschool | Electrical Engineering | Incoming Softmore

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE
In milestone 3, I got my milestone 2 goals done through a linear actuator and a relay module. The linear actuator is electromagnetic, so the rod that is launched will only stay on if the linear actuator has power. When powered, the rod's spring is compressed. The power is turned off and the rod launches out. The relay module helps control the power by closing and opening the circuit. One of my biggest challenges in this project was connecting to the raspberrypi. It was a nessesary step in completeing the robot. However, solving that problem was one of my biggest triumphs. I connected the raspberrypi to my TV and connected it to the wifi from there. I learned a lot about breadboards, wiring, raspberrypi, sonars, etc. I hope to continue to further progress my knowledge on these things and much more. 


# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/FQwBctQzHsA?si=1fnNRMI-f3Pny9SY&amp;start=44" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

The goals I set in milestone 1 are finally compeleted. In milestone 2, I got my raspberrypi camera working and got the robot to track and follow the ball. First, I started with my sonar cameras. I got their base screwed onto the baseplate, and I got them plugged into the raspberrypi. After that, I worked on its code and got it to track distance correctly. I downloaded the raspberrypi camera data and attached it to the raspberrypi itself. After that, all I needed to do was the code. This was the trickest part of the project in my opinion. It was difficult to understand the code and implement the next steps. After I sat down and understood it, I got the movement of the robot working. Now, my robot is finished. In milestone 3, I plan to add my own twist to the project. I came up with the idea of getting something to shoot at the robot, and I ordered the parts.



# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/KWApl1w_IGM?si=avCXKORX-d3MFxxl" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


The ball tracking robot, a self-explanitory name, tracks a big red ball. In milestone 1, I plan to complete the hardware components of the robot, mainly in getting the raspberry pi ready and powering the motors through it. First, I started with setting up the raspberrypi. I flashed my sd card and inserted it into the pi. However, I had problems ssding it to my computer. I had to connect my raspberrypi to my TV, and it finally worked. For the robot, I started off with the base plate, which I attached the motor wheels and a support wheel to help with turning. Due to only having male to male wires, I wired the raspberrypi to the motors through the breadboard. I plan to get my raspberrypi camera set up and getting the robot to track the ball through it. 

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

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
