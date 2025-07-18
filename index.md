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

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

In milestone 3, I got my milestone 2 goals done through a linear actuator and a relay module. The linear actuator is electromagnetic, so the rod that is launched will only stay on if the linear actuator has power. When powered, the rod's spring is compressed. The power is turned off and the rod launches out. The relay module helps control the power by closing and opening the circuit. One of my biggest challenges in this project was connecting to the raspberry pi. It was a necessary step in completing the robot. However, solving that problem was one of my biggest triumphs. I connected the raspberrypi to my TV and connected it to the wifi from there. I learned a lot about breadboards, wiring, raspberrypi, sonars, etc. I hope to continue to further progress my knowledge on these things and much more. 

# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/FQwBctQzHsA?si=1fnNRMI-f3Pny9SY&amp;start=44" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

The goals I set in milestone 1 are finally completed. In milestone 2, I got my raspberrypi camera working and got the robot to track and follow the ball. First, I started with my sonar cameras. I got their base screwed onto the baseplate, and I got them plugged into the raspberrypi. After that, I worked on its code and got it to track distance correctly. I downloaded the raspberrypi camera data and attached it to the raspberrypi itself. After that, all I needed to do was the code. This was the trickiest part of the project in my opinion. It was difficult to understand the code and implement the next steps. After I sat down and understood it, I got the movement of the robot working. Now, my robot is finished. In milestone 3, I plan to add my own twist to the project. I came up with the idea of getting something to shoot at the robot, and I ordered the parts.



# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/KWApl1w_IGM?si=avCXKORX-d3MFxxl" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


The ball tracking robot, a self-explanatory name, tracks a big red ball. In milestone 1, I plan to complete the hardware components of the robot, mainly in getting the raspberry pi ready and powering the motors through it. First, I started with setting up the raspberrypi. I flashed my sd card and inserted it into the pi. However, I had problems ssding it to my computer. I had to connect my raspberrypi to my TV, and it finally worked. For the robot, I started off with the base plate, which I attached the motor wheels and a support wheel to help with turning. Due to only having male to male wires, I wired the raspberrypi to the motors through the breadboard. I plan to get my raspberrypi camera set up and get the robot to track the ball through it. 

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser.

# Code

```
from picamera2 import Picamera2
import RPi.GPIO as GPIO
import time
import cv2
import numpy as np
from flask import Flask, Response, render_template_string
app = Flask(__name__)
relay = 18

def shoot():
    GPIO.setup(relay, GPIO.OUT)
    GPIO.output(relay, GPIO.HIGH)
    time.sleep(3)
    GPIO.output(relay, GPIO.LOW)
picam2 = Picamera2()
picam2.configure(picam2.create_preview_configuration(main={"format": "BGR888", "size": (640, 480)}))
picam2.start()
FRAME_WIDTH = 640
CENTER_X = FRAME_WIDTH // 2

GPIO.setmode(GPIO.BCM)

GPIO_TRIGGER1 = 13     
GPIO_ECHO1 = 6

GPIO_TRIGGER2 = 5    
GPIO_ECHO2 = 1

GPIO_TRIGGER3 =26     
GPIO_ECHO3 = 19

MOTOR1B=2  
MOTOR1E=3

MOTOR2B=17  
MOTOR2E=27

LED_PIN=4  

GPIO.setup(GPIO_TRIGGER1,GPIO.OUT) 
GPIO.setup(GPIO_ECHO1,GPIO.IN)     
GPIO.setup(GPIO_TRIGGER2,GPIO.OUT)
GPIO.setup(GPIO_ECHO2,GPIO.IN)
GPIO.setup(GPIO_TRIGGER3,GPIO.OUT) 
GPIO.setup(GPIO_ECHO3,GPIO.IN)
GPIO.setup(LED_PIN,GPIO.OUT)

GPIO.output(GPIO_TRIGGER1, False)
GPIO.output(GPIO_TRIGGER2, False)
GPIO.output(GPIO_TRIGGER3, False)

def sonar(GPIO_TRIGGER,GPIO_ECHO):
    start=0
    stop=0
    GPIO.setup(GPIO_TRIGGER,GPIO.OUT) 
    GPIO.setup(GPIO_ECHO,GPIO.IN)     
     
    GPIO.output(GPIO_TRIGGER, False)
    time.sleep(0.01)
    GPIO.output(GPIO_TRIGGER, True)
    time.sleep(0.00001)
    GPIO.output(GPIO_TRIGGER, False)
    begin = time.time()
    while GPIO.input(GPIO_ECHO)==0 and time.time()<begin+0.05:
        start = time.time()
     
    while GPIO.input(GPIO_ECHO)==1 and time.time()<begin+0.1:
         stop = time.time()
     
    elapsed = stop-start

    distance = elapsed * 34000

    distance = distance / 2
    return distance

GPIO.setup(MOTOR1B, GPIO.OUT)
GPIO.setup(MOTOR1E, GPIO.OUT)

GPIO.setup(MOTOR2B, GPIO.OUT)
GPIO.setup(MOTOR2E, GPIO.OUT)

def stop():
    GPIO.output(MOTOR1B, GPIO.LOW)
    GPIO.output(MOTOR1E, GPIO.LOW)
    GPIO.output(MOTOR2B, GPIO.LOW)
    GPIO.output(MOTOR2E, GPIO.LOW)

def leftturn():
    GPIO.output(MOTOR1B, GPIO.LOW)
    GPIO.output(MOTOR1E, GPIO.HIGH)
    GPIO.output(MOTOR2B, GPIO.LOW)
    GPIO.output(MOTOR2E, GPIO.HIGH)
def forward():
    GPIO.output(MOTOR1B, GPIO.LOW)
    GPIO.output(MOTOR1E, GPIO.HIGH)
    GPIO.output(MOTOR2B, GPIO.HIGH)
    GPIO.output(MOTOR2E, GPIO.LOW)
def back():
    GPIO.output(MOTOR1B, GPIO.HIGH)
    GPIO.output(MOTOR1E, GPIO.LOW)
    GPIO.output(MOTOR2B, GPIO.LOW)
    GPIO.output(MOTOR2E, GPIO.HIGH)
def rightturn():
    GPIO.output(MOTOR1B, GPIO.HIGH)
    GPIO.output(MOTOR1E, GPIO.LOW)
    GPIO.output(MOTOR2B, GPIO.HIGH)
    GPIO.output(MOTOR2E, GPIO.LOW)

def track_red_ball(frame):
    hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)
    lower_red1 = np.array([0, 100, 100])
    upper_red1 = np.array([10, 255, 255])
    lower_red2 = np.array([160, 100, 100])
    upper_red2 = np.array([179, 255, 255])
    mask1 = cv2.inRange(hsv, lower_red1, upper_red1)
    mask2 = cv2.inRange(hsv, lower_red2, upper_red2)
    mask = cv2.bitwise_or(mask1, mask2)
    mask = cv2.erode(mask, None, iterations=2)
    mask = cv2.dilate(mask, None, iterations=2)
    contours, _ = cv2.findContours(mask, cv2.RETR_EXTERNAL,
    cv2.CHAIN_APPROX_SIMPLE)
    offsetPos = 0
    if contours:
        largest = max(contours, key=cv2.contourArea)
        M = cv2.moments(largest)
        if M["m00"] > 0:
            cx = int(M["m10"] / M["m00"])
            cy = int(M["m01"] / M["m00"])
            offset = cx - CENTER_X
            offsetPos = offset 
            if abs(offset) < 30:
                position = "Centered"
            elif offset < 0:
                position = "Left"
            else:
                position = "Right"
            cv2.drawContours(frame, [largest], -1, (0, 255, 0), 2)
            cv2.circle(frame, (cx, cy), 5, (255, 0, 0), -1)
            cv2.putText(frame, f"Offset: {offset} ({position})",
            (10, 30),
            cv2.FONT_HERSHEY_SIMPLEX, 0.7, (255, 255,
            255), 2)
   
    return frame, offsetPos

def drive(offset):
    distanceR = sonar(GPIO_TRIGGER3,GPIO_ECHO3)
    distanceL = sonar(GPIO_TRIGGER1,GPIO_ECHO1)
    found =0
    flag=0
    GPIO.output(LED_PIN,GPIO.LOW)   
    if(offset!=0):
        found=1       
    if(found==0):
        if (flag==0):
                rightturn()
                time.sleep(0.1)
        else:
                leftturn()
                time.sleep(0.1)
        stop()

    elif(found==1):
        GPIO.output(LED_PIN,GPIO.HIGH)
        if(offset<=-35 or offset>=35):
            if(offset<0):
                flag=0
                rightturn()
                print("turning right")
                time.sleep(0.08)
                stop()
                time.sleep(0)
            elif(offset>0):
                flag=1
                leftturn()
                print("turning left")
                time.sleep(0.08)
                stop()
                time.sleep(0.00625)
        else:
            print("hi")
            stop()
            time.sleep(1)
            print(distanceR)
            while distanceR>7:
                forward()
                time.sleep(0.05)
                stop()
                distanceR = sonar(GPIO_TRIGGER3,GPIO_ECHO3)
            shoot()
    return
def generate_frames():
    while True:
        frame = picam2.capture_array()
        frame = cv2.cvtColor(frame, cv2.COLOR_RGB2BGR)
        frame, offset = track_red_ball(frame)
        print(offset)
        drive(offset)
        ret, buffer = cv2.imencode('.jpg', frame)
        jpg_frame = buffer.tobytes()
        yield (b'--frame\r\n'
                b'Content-Type: image/jpeg\r\n'
                b'Content-Length: ' + f"{len(jpg_frame)}".encode()
                + b'\r\n\r\n' +
                jpg_frame + b'\r\n')
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
@app.route('/video_feed')


def video_feed():
    return Response(generate_frames(),mimetype='multipart/x-mixed-replace;boundary=frame')
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)


```

# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Raspberry Pi Kit | It helps control and power the robot | $95.19 | <a href="https://www.amazon.com/RasTech-Raspberry-Starter-Heatsink-Screwdriver/dp/B0C8LV6VNZ/ref=sr_1_4?crid=3506HY00MCGVM&dib=eyJ2IjoiMSJ9._zkM62vSQ8p7tNr88715LdMv_qHh72Je-tkF9PXEa3chDE53QT4aZu4AGAb4ihE61QY4ZD55nKF6Fp2Kfs8t7AbafM_JrlJFfHo9OB4eAVGqa0EB-7aoBQHPmhKHZ2MW8ny-Kd44bMVlVxPlTWVk5YHIN5P3uKVqrE5Dcal0rKkHny-O6Xyb5ux2AOU6OwVbkag_bqBX66RQNRrgBuz-0pS43mcx93IZTQA9R8NaJJypYU2HAycp-XicTFmyU60a01Nfm9iuyo6B9yA8ppN3OQQyJ-NQ9xyNPxfTLwkqtng.yAYpU6outhQcZmOZhN9Wb6yTw7A85CNUbXZguGInZNg&dib_tag=se&keywords=raspberry%2Bpi%2Bkit&qid=1718848547&s=electronics&sprefix=rasbperry%2Bpi%2Bkit%2Celectronics%2C83&sr=1-4&th=1"> Link </a> |
| Robot Chassis | It is the base of the robot that allows it to be mobile | $18.99 | <a href="https://www.amazon.com/Smart-Chassis-Motors-Encoder-Battery/dp/B01LXY7CM3/ref=sr_1_5?crid=373Y5YK6JWMD&keywords=robot+chassis&qid=1687740144&sprefix=robot+chassi%2Caps%2C93&sr=8-5"> Link </a> |
| Screwdriver Kit | It is used when attaching items to the chassis | $5.94 | <a href="https://www.amazon.com/Small-Screwdriver-Set-Mini-Magnetic/dp/B08RYXKJW9/"> Link </a> |
| Ultrasonic Sensor | Measure distance from things | $9.99 | <a href="https://www.amazon.com/WWZMDiB-HC-SR04-Ultrasonic-Distance-Measuring/dp/B0CQCCGXCP/ref=sr_1_1_sspa?crid=3J2JR973WKPHO&dib=eyJ2IjoiMSJ9.E2SIkElJhtFWCJCHL5Q6Y73Ys_HCMPRVFCIrG_zKv4Og7BdZNtr69Mkju140lhlfzFGQuY542jpsp8FMrtV9d2hCBI7D8lYTH9bcgDXZhs4941uj-d1D69ZYdKmAI1Jig3VmYXOl3axVQ8Jq5L3nGRymNMtNbxkaFqGNyzkq4p37hhxU6jheuoaMo3Onz2FE9ILThkjUbdxRNW3rrZgZ7bYj9mf-yav85hBAmNduYyo.EneY3GmHDfDjDwhdUdDQ4Ktk6fECH62Adb42cEkehRc&dib_tag=se&keywords=ultrasonic%2Bsensor&qid=1715961326&sprefix=ultrasonic%2Bsensor%2Caps%2C72&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1"> Link </a> |
| H Bridges | Allow the motors to operate | $8.99 | <a href="https://www.amazon.com/ACEIRMC-Stepper-Controller-2-5-12V-H-Bridge/dp/B0923VMKSZ/"> Link </a> |
| Pi Cam | Allows the robot to see | $12.86 | <a href="https://www.amazon.com/gp/product/B07RWCGX5K/ref=ox_sc_act_title_1?smid=A2IAB2RW3LLT8D&psc=1"> Link </a> |
| Electronics Kit | Allows parts of the robot to be powered | $11.98 | <a href="https://www.amazon.com/EL-CK-002-Electronic-Breadboard-Capacitor-Potentiometer/dp/B01ERP6WL4/ref=sr_1_4?crid=30T5LTYVQLQ7Z&dib=eyJ2IjoiMSJ9.XZtpck6Llt4UIuYeKM4X3BoXzDuzolZMTCtFDj-oTh1vuIi0HYJZJEdpS-MCdGCK1AWUbUmgoEswoRPxGUSKeGRTzsciRE_l2Vrp8FGX1SxK-HmibPNyHBEtkFJKo_OYmMhkhdCJ4OIH38ALRfFvrXZ7OU5faZVvkTBqod8p7UZYwNwdLCcimwFWGWKaDa-gbbx_TGk7lYQmEbrzeL4UXM-gW3RDtuOV0dCykxwyvYJKCCcOhrK3f18N4NZjiqL_Y5noE1rQTmwyFcG67DzgpNaUPanwIQaYfCe5mgD-njY.v6mU1wYX4M5ShCiyrZMey0hbOwvqLszD8axpHbKlA6I&dib_tag=se&keywords=mini+breadboard+kit&qid=1716419767&s=electronics&sprefix=mini+breadboard+kit%2Celectronics%2C106&sr=1-4"> Link </a> |
| Motors | Allows the robot to move | $11.98 | <a href="https://www.amazon.com/AEDIKO-Motor-Gearbox-200RPM-Ratio/dp/B09N6NXP4H/ref=sr_1_4?crid=1JP29NIWBLH2M&dib=eyJ2IjoiMSJ9.Wq3jKgOLbqtEP772vMD4pV5f-w3PLBdEpKqguykXOb0JFO14f4Dq0m_VDVUMUFtR8WFINUEticI3GXcoGqwXPqK9yIh04PhCktgccMz9zAUiKXMJPwmOTUp_6av3XuFD0lXo9WngN9iKI6YgZrhEEs9qnqbcB1GnvgntCdKz8Q1dFuNu61NgSE6Z8vBk3FRpaNcr1lCI7FApTiNi0Qce8gbfmMn6oUggZQHpIOKKZ6s.M7WsZ_ZZtm3rm93kKgw0NOxt1McVBYX6m55oGxu1xxI&dib_tag=se&keywords=dc+motor+with+gearbox&qid=1715911706&sprefix=dc+motor+with+gearbox%2Caps%2C126&sr=8-4"> Link </a> |
| DMM | Measures voltage, etc | $11 | <a href="https://www.amazon.com/AstroAI-Digital-Multimeter-Voltage-Tester/dp/B01ISAMUA6/ref=sxin_17_pa_sp_search_thematic_sspa?content-id=amzn1.sym.e8da13fc-7baf-46c3-926a-e7e8f63a520b%3Aamzn1.sym.e8da13fc-7baf-46c3-926a-e7e8f63a520b&cv_ct_cx=digital+multimeter&dib=eyJ2IjoiMSJ9.5LQumrfBR8l0mKnJCJlRg73dxpou0gqYD_ffU3srgs0Utegwth8GcQCSVXVzeZeLSJx5J3itz5TLdmJHsrVITQ.-00jRPoT-bBy26YC4LzQ-S4cYdztgmSMGb83_WEm6HY&dib_tag=se&keywords=digital+multimeter&pd_rd_i=B01ISAMUA6&pd_rd_r=e1ff2570-7e4a-4906-bc55-6f819d48d1bc&pd_rd_w=h7HgL&pd_rd_wg=0ZcFH&pf_rd_p=e8da13fc-7baf-46c3-926a-e7e8f63a520b&pf_rd_r=R6YKX3NXTDQ1PQP4H8RM&qid=1715911879&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&sr=1-1-7efdef4d-9875-47e1-927f-8c2c1c47ed49-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9zZWFyY2hfdGhlbWF0aWM&psc=1"> Link </a> |
| Red Ball | For the robot to track | $16.73 | <a href="https://www.amazon.com/Champion-Sports-Inch-Coated-Density/dp/B000KYTTYO/ref=sr_1_2_sspa?dib=eyJ2IjoiMSJ9.TLCeZ2jjYwnvK3RiJf14C4RstYOZXhRWTRbHkmLGiNfm5Vd8mVjvtsbUnBFk0S4d6cW9cPT7XDdhwMcPC30nsNwer7Uim0JVF49R8Od82u3RH4TY4mO1uP5LtqdvIEcW7CaOm7AzQ6xOvWQ4say1Ci9eGOxETDRWJP5rewLnqARbrvbe4kh-b2d5NHCLEsarPl16pM1UVlmQCXfMRksXigf_GpckmWPjeUM1AC8iiU0.lGUWr3-ZcZJNl0nJ2JaU6JEUOF9oR26lf0kUvETdmtM&dib_tag=se&keywords=7+inch+red+ball&qid=1748284272&sr=8-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1"> Link </a> |
| AA batteries | Powers the linear solenoid | $18.74 | <a href="https://www.amazon.com/Duracell-Coppertop-AA-Ingredients-Long-lasting/dp/B0035LCFNQ/ref=sr_1_2_sspa?crid=2YR65MVXWA50C&dib=eyJ2IjoiMSJ9.Y7LKJBX-6tZ05fw4EcW76nu14zklVu0uDSTwj-0-cV44GfYvoaYnLKVwcPIB1rWt_qVnpkZnwoqkvrQmMFQ1qiTWN_rokxCgCagwBWaAIiv9PAbMqrwOrkGuvfWfklSZi5Y9W6AaUUspAaSMBZuUyS4cUoJB-s35FE-4seDyYIxfOaNAZggr154hcf3CR015QRyanTdKe1P3g2-fihntxqYoU2ek7H01s8toH4MNd-E.Mnyne8z1KkhvfDMnfFLgjUB9WgjdkdMcYRL591Pngbk&dib_tag=se&keywords=aa+batteries&qid=1748284893&refinements=p_85%3A2470955011&refresh=1&rnid=2470954011&rps=1&sprefix=aa+batterie%2Caps%2C122&sr=8-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1"> Link </a> |
| USB power bank | Powers the raspberry pi | $16.19 | <a href="https://www.amazon.com/SIXTHGU-Portable-Charger-Charging-Flashlight/dp/B0C7PHKKNK/ref=sr_1_2_sspa?crid=2ZZM4AAZMMWHQ&dib=eyJ2IjoiMSJ9.W2Zx5_I3mKOn6UpwAzOw6PD0PNh1iaMRBiedequdv9weeWL0HPyPcxJBR9h6-LiFW-sHKnHSApN0sUxx0Q9xIRs80R57IlvvCsmEzXcktogo-4nP-NxrEZOy5dJTcXY8N-PBwfGt4fl_9LP8npenzDUV9TPA8KN6DMu175g6JegC_gZhAJrbqX94EfpQhLwP9vIJH45w2N-AFrfZZOy9jqk55gzVyk4Qst8uZvqn768.KBrc5_SqZ4e8zCpoFc-1C7rk02t3o2ykgDPB65W5JJU&dib_tag=se&keywords=always%2Bon%2Bpower%2Bbank&qid=1715957917&sprefix=always%2Bon%2Bpower%2Bbank%2Caps%2C107&sr=8-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1"> Link </a> |
| Relay | Turns on and off power for the linear solenoid | $6.99 | <a href="https://www.amazon.com/AEDIKO-Channel-Optocoupler-Isolation-Support/dp/B095YD3732?crid=1ZRHXRKW3TTWU&dib=eyJ2IjoiMSJ9.Ap3Z-NOR6vRNRVHVIJGgGQN4S8-VoiEZWfvBqwBW2MN_D9y9nlGHPUNT1iPiH-iBemnwoieDQofpNhUFJNzGtVusSy61XW-thn3hBKKAaJMBs1h5m6XkFugTeLSLftz4HAsEzJCIaWIIwhuFqDeuI3W6p83LZf1ppsiVrj_vU1QZDsxnQp2mvN49uZdzpRHGLraMnlizvQxvDPfQ8tiEp1JVs30ihcwJKy7Rd53kzANkpxnJDz_vtFo8kABhZaQJk-ueLebqkh3yYjscgKwj80zZGtRUvvjgEKYcoAdhEa8.HfQdWrfzSeClzFpRCNaEM-Qr6AfUDwJPMwGCnCP2yPI&dib_tag=se&keywords=arduino%2Brelay&qid=1750950739&s=industrial&sprefix=arduino%2Brela%2Cindustrial%2C457&sr=1-1&th=1"> Link </a> |
| Linear Solenoid | Shoots at the robot | $15.99 | <a href="https://www.amazon.com/Solenoid-Electromagnet-Actuator-Electric-DS-0420S/dp/B0BMVDPWS3/132-5188632-1212317?pd_rd_w=8PUvL&content-id=amzn1.sym.6640a844-ab24-4352-ac9b-78899e683a5e&pf_rd_p=6640a844-ab24-4352-ac9b-78899e683a5e&pf_rd_r=RXYGNRW41001KTNCRTP0&pd_rd_wg=FrFO0&pd_rd_r=af5cb0dd-453c-460a-9cf9-aa12a21f40ae&pd_rd_i=B0BMVDPWS3&psc=1"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
