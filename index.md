# Solar Tracker 
Using photoresistors, servo motors, and a solar panel, my project becomes a solar tracker that measures the best position for the solar panel based on the of the sun voltage of the sun tracked by the photoresistor values by moving the base part which has the solar panel to areas with more sun.


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Kritika C | Westmont High School| Enviormental Engineering | Incoming Senior

<!--
**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
 -->
# Complete and working project with modifcations
<!--
**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
-->
For my final milestone, I have fully completed the solar tracker and added modifications such as wheels and a motor control board that helps create power for the wheels to move and overall helps level up the base project. My biggest challenges throughout the Blue Stamp Engineering program was working on time management and thinking of and implementing modifications that I could add to my project. My biggest triumph throughout the project was getting my base project to work smoothly on my first try without having to disassemble big parts of it to fix it. Throughout the program, I learned how to successfully code, solder, and wire components that I added onto my original project. I hope to learn in the future more about mechanical engineering and electrical engineering as I learned to challenge myself with skills from both types of engineering throughout BlueStamp.

# Adding Wheels 
<!--
**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
-->
For my second milestone, I have added 2 motors and wheels to the bottom of my solar tracker, as well as wire up a motor control board to allow for the motors to run and the robot to move by itself. So far, throughout the project, I'm surprised by the many little things that, if not taken care of, could cause a big problem later on. For example, just changing a small wire could stop half of the arduino from working. I overcame the challenge of not knowing where to put the pins blocked by the arduino shield. I overcame this by finding pins which were covered, but not being used, and attached the wires underneath the board.
 

# Orginal Solar Tracker Build
<!--
**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
-->
For my first milestone, I used servos, batteries, an arduino, arduino shield, different screw types, and more to power and build the 2 main parts of my solar tracker. The batteries help power the solar panel allowing it to move to spots that have a greater amount of sunlight. A challenge I noticed for future milestones is how I will use the pins covered by the arduino shield for future modifications that will need the pins to connect to the arduino and solar tracker. My plan is to continue adding modifications, such as creating a connection to charge phones and allowing the robot to move on wheels.


<!--
# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser.
-->
# Code
```
 * Dual_Axis_Tracker_V3.ino
 * Brown Dog Gadgets <https://www.browndoggadgets.com/>
 */
*/ const int in1 = 4; // in1,2 for right wheel
const int in2 = 3;
int speed = 150;
// include Servo library
#include <Servo.h>

// horizontal servo
Servo horizontal;
int servoh = 90;

int servohLimitHigh = 180;
int servohLimitLow = 65;

Servo vertical;
int servov = 90;

int servovLimitHigh = 120;
int servovLimitLow = 15;


// LDR pin connections
int ldrTR = 0; // LDR top right
int ldrTL = 1; // LDR top left
int ldrBR = 2; // LDR bottom right
int ldrBL = 3; // LDR bottom left
int N= 4;
int S=5;
// put other varibales for south, east and west
int tol = 50;
void setup() {
  Serial.begin(9600);
  // servo connections
  horizontal.attach(5);
  vertical.attach(6);
  // move servos
  horizontal.write(90);
  vertical.write(45);
  delay(3000);
}


void loop() {

  int tr = analogRead(ldrTR); // top right
  int tl = analogRead(ldrTL); // top left
  int br = analogRead(ldrBR); // bottom right
  int bl = analogRead(ldrBL); // bottom left
  int north = analogRead (N);
  int south = analogRead (S);
  int dtime = 0; // change for debugging only
  int tol = 50;

  int avt = (tl + tr) / 2; // average value top
  int avd = (bl + br) / 2; // average value bottom
  int avl = (tl + bl) / 2; // average value left
  int avr = (tr + br) / 2; // average value right

  int dvert = avt - avd;  // check the difference of up and down
  int dhoriz = avl - avr; // check the difference of left and right


  // send data to the serial monitor if desired
  Serial.print(tl);
  Serial.print(" ");
  Serial.print(tr);
  Serial.print(" ");
  Serial.print(bl);
  Serial.print(" ");
  Serial.print(br);
  Serial.print("  ");
  Serial.print(avt);
  Serial.print(" ");
  Serial.print(avd);
  Serial.print(" ");
  Serial.print(avl);
  Serial.print(" ");
  Serial.print(avr);
  Serial.print("  ");
  Serial.print(dtime);
  Serial.print("   ");
  Serial.print(tol);
  Serial.print("  ");
  Serial.print(servov);
  Serial.print("   ");
  Serial.print(servoh);
  Serial.println(" ");


int NS = north - south;
// move forward
if (NS > tol ){digitalWrite(in1, 0);
  digitalWrite(in2, speed);
  }

// move backwards 
else if (NS < -1* tol){digitalWrite(in1, speed);
  digitalWrite(in2, 0);
}

 // stop moving 
 else {digitalWrite(in1, 0);
  digitalWrite(in2, 0);
 }
 
  // check if the difference is in the tolerance else change vertical angle
  if (-1 * tol > dvert || dvert > tol) {
    if (avt > avd) {
      servov = ++servov;
      if (servov > servovLimitHigh) {
        servov = servovLimitHigh;
      }
    }
    else if (avt < avd) {
      servov = --servov;
      if (servov < servovLimitLow) {
        servov = servovLimitLow;
      }
    }
    vertical.write(servov);
  }

  // check if the difference is in the tolerance else change horizontal angle
  if (-1 * tol > dhoriz || dhoriz > tol) {
    if (avl > avr) {
      servoh = --servoh;
      if (servoh < servohLimitLow) {
        servoh = servohLimitLow;
      }
    }
    else if (avl < avr) {
      servoh = ++servoh;
      if (servoh > servohLimitHigh) {
        servoh = servohLimitHigh;
      }
    }
    else if (avl = avr) {
      // nothing
    }
    horizontal.write(servoh);
  }
 
  delay(dtime);  
}

```
 # Bill of Materials

| Dual axis solar tracker|Base solar tracker project  | $150 |https://www.amazon.com/Brown-Dog-Gadgets-Tracker-Educational/dp/B07X4LCHLY/ref=sr_1_10?crid=QQ2E2TQW2O2Y&keywords=dual+axis+solar+tracker&qid=1688071265&sprefix=dual+axis+%2Caps%2C167&sr=8-10 |
|:--:|:--:|:--:|:--:|
| DC Buck Converter| Convertor for volts to amps (which I used to charge a phone with the solar tracker) | $5.99| https://www.amazon.com/KOOBOOK-DC-DC-Charger-Module-      Converter/dp/B07SDB3CVX/ref=asc_df_B07SGWRQGX/ tag=&linkCode=df0&hvadid=385215532707&hvpos=&hvnetw=g&hvrand
=1340376542165361001&hvpone=&hvptwo =&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9027632 &hvtargid=pla-844459571215&ref=&adgrpid=73789134890&th=1|
|:--:|:--:|:--:|:--:|
| Photoresitors| Used to measure resistance and light values from a light source| $5.99 |https://www.amazon.com/eBoot-Photoresistor-Sensitive-Resistor-Dependent/dp/B01N7V536K/ref=sr_1_1?crid=166L5796OYRJB&dd=GDYMwvM5SarwxK7z_eOewQ%2C%2C&keywords=photoresistors&qid=1687446872&refinements=p_90%3A8308921011&rnid=8308919011&sprefix=photoresistors%2Caps%2C131&sr=8-1|
|:--:|:--:|:--:|:--:|
| Gearbox motor, controll board, wheel set| A set with motors, wheels wired and a motor controll board to implement motors into a project.| $12.99 |https://www.amazon.com/ShangHJ-Gearbox-Motor-200RPM-Wheel/dp/B09F9HNP7M/ref=sr_1_6crid=374OJXZNPQEGI&keywords=arduino+motor+kit+board+and+wheels+4+pieces&qid=1687449018&sprefix=ardiuno+motor+kit+board+and+wheels+4+pecies+%2Caps%2C126&sr=8-6|

<!--
# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
-->
