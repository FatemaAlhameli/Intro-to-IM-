
# Graffiti Wall


#### Fatema Alhameli and Meera Al Khazraji 
#### Introduction to Interactive Media 
#### Final Project
#### 13 May 2022 

[P5 Web Editor Link](https://editor.p5js.org/FatemaAlhameli/full/XiviQ-tmH)

## Concept Description 

[Video Demo of Final Project](https://vimeo.com/709105224)



<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Final%20Project/Screen%20Shot%202022-05-12%20at%206.02.01%20PM.png" width = "370" height = "320">   <img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Final%20Project/enclosing%202.png" width = "370" height = "320"> 

## Ardunio Code Explanation
In our Arduino code, we first begin with initializing the pin numbers for our sensors. For instance, the six buttons for color changing are plugged into pins 2 - 7, and the x and y values of the joystick are plugged into A0 and A1 as it is an analog sensor. Also, the switch(SW) of the joystick, which is like a momentary button, is plugged into pin 8. Lastly, our last sensor, which is the force sensor, is plugged into the analog pin A2. We also declared variables that will store the values of these sensors. For example, ```xPosition``` and ```yPosition``` store the x and y values of the joystick sensor as it is used. For the buttons, we created a separate variable for each colored button like rvalue, bvalue, etc. 

In void setup, we used the ```pinMode``` command to set each of the sensors as either inputs or outputs. In our case, all of our sensors are inputs. In void loop, we began with letting the variables  ```xPosition``` and ```yPosition``` read the joystick values by using ```analogRead```. Likewise, for the force sensor, we let the variable ```FSvalue``` store/read the values of the force sensor.  Similarly, we did the same thing for each colored button. However, we used digitalRead as it is a digital sensor. The switch on the joystick had the same line of code as it is a digital input.  

The final step in the Ardunio code is to send it to P5. previously we did this step using P5 serial control. However, we were given an alternative for P5 serial control as it was a lengthy process. This new process is a web serial p5 Ardunio. Thus, we don't have to deal with anything out of these two programs. From the Ardunio side, all we have to do is print the values of each sensor. Therefore, in setup, we put the ```Serial.begin(9600);```. Then in loop we put ```Serial.print``` for all the value variables of the sensors and made sure to print commas in between in order for us to see the values in an organized manner. Ultimately, when we run the code in Ardunio and open the serial monitor, we can see the correct values of each sensor. 

```
int VRx = A0;
int VRy = A1;
int xPosition = 0;
int yPosition = 0;
int SW = 8;
int SWstate = 0;

int FS = A2;
int FSvalue = 0;

int RbuttonPin = 7;
int GbuttonPin = 5;
int BbuttonPin = 2;
int PUbuttonPin = 4;
int PbuttonPin = 6;
int BLbuttonPin = 3;

int rValue = 0;
int gValue = 0;
int bValue = 0;
int puValue = 0;
int pValue = 0;
int blValue = 0;

void setup() {

  Serial.begin(9600);

  // Joystick to draw
  pinMode(VRx, INPUT);
  pinMode(VRy, INPUT);
  pinMode(FS, INPUT);

  //Color buttons for spray paint
  pinMode(RbuttonPin, INPUT);
  pinMode(GbuttonPin, INPUT);
  pinMode(BbuttonPin, INPUT);
  pinMode(PbuttonPin, INPUT);
  pinMode(PUbuttonPin, INPUT);
  pinMode(BLbuttonPin, INPUT);
  pinMode(SW, INPUT_PULLUP);
}

void loop() {
  //Reading the values of the sensors and storing in variables 
  xPosition = analogRead(VRx);
  yPosition = analogRead(VRy);
  SWstate = digitalRead(SW);

  FSvalue = analogRead(FS);

  rValue = digitalRead(RbuttonPin);
  gValue = digitalRead(GbuttonPin);
  bValue = digitalRead(BbuttonPin);
  puValue = digitalRead(PUbuttonPin);
  pValue = digitalRead(PbuttonPin);
  blValue = digitalRead(BLbuttonPin);

  // Printing values to send to P5
  Serial.print(xPosition);
  Serial.print(",");
  Serial.print(yPosition);
  Serial.print(",");
  Serial.print(rValue);
  Serial.print(",");
  Serial.print(puValue);
  Serial.print(",");
  Serial.print(pValue);
  Serial.print(",");
  Serial.print(gValue);
  Serial.print(",");
  Serial.print(bValue);
  Serial.print(",");
  Serial.print(blValue);
  Serial.print(",");
  Serial.print(FSvalue);
  Serial.print(",");
  Serial.println(SWstate);



  delay(100);
}

```


## P5 Code Explanation

To send Ardunio values into p5, we used the [WEB SERIAL p5 ARDUINO](https://editor.p5js.org/itp42/sketches/KDPs5Rl-P) the Professor gave us to use.  This example was far simpler than using p5 serial control. This example included two important functions. The first is a simple ```keyPressed``` function that includes the line ``` setUpSerial();``` that allows us to make the serial connection by pressing the space bar key and then selecting the correct port. The second function is ```readSerial```, which in an array splits the data received from Ardunio, and then you specify the number of data (sensor values) coming from Ardunio.  To do this, we initialized the variables for all of our sensor's values and added them to this function. When we added these values, we added the condition ```fromArdunio[#]``` that specifies which number on the array has these values of the specific sensor stored. We ensured that the number organization of sensors in the array corresponds to the same list organization in Ardunio (serial printing section). Then the values that are stored in the variables can be used in the draw function. 

 

#### Joystick 
Once we became familiar with the process of how to send values from Ardunio to p5, it was simpler to do so for the rest of the sensors used in our project. The first sensor we worked with in p5 was the joystick. This sensor, in particular, was quite difficult to work with at first. Since the sensors had three types of values included in it. The first is the x value, which is when the sensor moves from left to right. The second one is the y value which is when it moves up and down. Lastly is the switch (SW), which is a digital sensor that changes value from HIGH to LOW or 1 to 2 when pressed. We first struggled with mapping the x and y values to draw strokes of lines. We started by using ```mapX``` and ```mapY``` where we mapped the original values 0 - 1023 and the values we wanted 0 - 550. The map values we chose were just random. We wanted to explore the sensor as it was our first time using it. However, the sensor drew straight strokes of lines rather than in a free manner. We then realized that the sensor draws quickly because its values change quickly when moved. Therefore, we had to limit that. We set the initial value of the sensor as a middle value, so we did ```let xPosition = 1023 / 2``` and the same for y. Then we changed ```mapX``` and ```mapY``` into other variables called ```tempX``` and ```tempY```. We did the same mapping of values but changed our values from -5 to 5. We then made ```mapX = mapX + tempX``` and the same for ```mapY```. Lastly, we decraled the stroke condition and placed the variables ```mapX``` and ```mapY``` in it. Ultimately, this allowed for smoother drawing using the joystick. 



#### Spray Effect
To make it seem as if the user is drawing with spray paint on the graffiti wall we tried looking for a way to create a spray effect on p5. We came across a [reference](https://www.dongphilyoo.com/archive/blog/itp/icm/icm-week6-p5-js-serial-port-communication-with-arduino/)  that helped us with understanding how to do so. This example method of creating a spray effect uses sin and cos. We created a new function called spray, with ```mapX``` and ```mapY``` as its coordinates. The function first includes two important things the stroke and setting a diameter. At the top of the sketch code, we made the diameter equal to 10.  In the function, we initialized a variable called ```radiusHigh``` which multiples the diameter by 0.5. The function includes an if statement that states if the diameter is larger than 0, then a for loop draws ellipses at random angles of ```TWO_PI``` and at a random radius between 0 and ```radiusHigh```. This spray effect is possible because when the ellipse code is written, the radius is multiplied by cos and sin and added to ```mapX``` and ```mapY```. The coordinates in the ellipse code are set at random values. The function also includes another if statement that specifies that if the values of ```mapX``` and ```mapY``` at the same point, the diameter of the spray would increase. The mechanics of this code is the same as the other if statement, whereas the only difference is in one of the values of the for loop. Lastly, to make sure that when the joystick draws in uses the spray effect, we replaced the stroke in the draw with spray and added ```mapX``` and ```mapY``` next to it in brackets. 

#### Switch in the joystick
We realized that the spray effect began immediately after we ran the code. So we wanted to change that by using the switch in the joystick. This was simple to add in the p5 code. The values of this switch are stored in the variable ```SWstate```. While printing the values of the switch in Ardunio, we saw that the value of the switch when pressed is 0 and 1 when it's not. Therefore, in draw, we added an if statement that indicates if the switch value is 0, then we put all the code for the joystick inside. Therefore, only when the switch is pressed can the user draw with it.  

[Drawing with Joystick Video](https://vimeo.com/709107962)

#### Buttons for color change 
Next, we added buttons to enable the change of the spray color. The initial color that is set for the drawing is grey. The buttons have values 0 or 1. zero means off, and one means on. For each colored button, we created a variable to store these two values. To take the red button value as an example, we added an if statement for it in draw that states if the button's value equals one, then the fill color should be red. We proceeded to do the same thing for all six colored buttons. The color that is selected is shown in the text that is on the canvas and everytime it is changes the text color changes. 

#### Force sensor for reset
The last sensor we added was a force sensor to allow the user to reset and erase the whole canvas. Since we are using an image for the background of the canvas, all we had to was make the force sensor add a new one when it's used. So we stored all the values of the force sensor in a variable called ```FSvalue``` which were from 0 to 1023. In draw, we wrote an if statement saying that if the force value is greater than 400, then a new image of the brick wall would be created on the canvas, ultimately removing all that has been drawn with the joystick. 

#### Assets
To upload our image, sound, and font, we used the preload function. To upload the image in setup, we used the image syntax where we added the image we uploaded and the XY coordinates and size. For the size, we set it as ```windowWidth``` and ```windowHeight``` as that is what we set our canvas size too. For the text, we used the text syntax where we added the text we wanted and its XY coordinates. We also used ```textFont(font)``` to ensure the font works. The sound we had minor obstacles with. When we uploaded it, the sound quality was horrible, but we realized why after the professor pointed out we had it in draw instead of loop. However, we couldn't move it to loop because the sound was meant to play when the joystick switch was pressed and drawn with. Therefore, the professor recommended we create a new variable called ```pSWstate``` and set it equal to one. In the ```readSerial``` function we added an if statement specifying that if ```pSWstate``` is less than ```SWstate``` then the sound should stop. Else if the ```pSWstate``` is larger than the ```SWstate```then the sound should play. In other words, if the switch is pressed and its value becomes 0, then the ```pSWstate``` becomes larger, so the sound plays. 

```
let xPosition = 1023 / 2;
let yPosition = 1023 / 2;
let mapX = 200;
let mapY = 200;
diameter = 10;
let pX = 0, pY = 0;
let rvalue = 0;
let gvalue = 0;
let bvalue = 0;
let puvalue = 0;
let pvalue = 0;
let blvalue = 0;
let FSvalue = 0;
let SWstate = 1;
let pSWstate = 1;
let brickWall;
let spraySound;
let font; 

// preload function to upload the brick wall image, spray sound effects, and font
function preload() {
  brickWall = loadImage("assets/white-brick-wall-bg.webp");
  spraySound = loadSound("assets/Spray Effect Sound.mp3");
  font = loadFont("assets/AttackGraffiti-ZVJPZ.otf")
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  // background(220);
  fill(99, 97, 99);
  image(brickWall, 0, 0, windowWidth, windowHeight);
  textFont(font);
}

function draw() {
 
  // the text on top of the canvas 
  textSize(60)
  textAlign(CENTER, TOP);
  text("Graffiti Wall", 710, 20);
 


  // if the joystick is pushed down you are able to draw with it
  if (SWstate == 0 && serialActive) {
    //Joystick
    pX = mapX;
    pY = mapY;
    tempX = map(xPosition, 0, 1023, -7, 7); //reads the values of the x values in the joystick
    tempY = map(yPosition, 0, 1023, -7, 7); //reads the values of the y values in the joystick
    mapX = mapX + tempX;
    mapY = mapY + tempY;
    // print(mapX, mapY);
    spray(mapX, mapY); // call the function spray to be using with the values of the joystick
  }

  //fill color of buttons
  if (rvalue == 1) {
    fill(212, 95, 93); //red
  }
  if (gvalue == 1) {
    fill(140, 230, 176); //green
  }
  if (bvalue == 1) {
    fill(151, 192, 252); //blue
  }
  if (puvalue == 1) {
    fill(139, 83, 163); //purple
  }
  if (pvalue == 1) {
    fill(217, 126, 206); //pink
  }
  if (blvalue == 1) {
    fill(0, 0, 0); //black
  }

  //reading force sensor values and resets canvas by adding a new image on top
  if (FSvalue > 400) {
    image(brickWall, 0, 0, windowWidth, windowHeight);
  }
}

// spray effect function
function spray(mapX, mapY) {
  
  stroke(0);
  radiusHigh = diameter * 0.5;
  
  // if the diameter is more than zero ellipse are drawn at a random angle, radius, and distance 
  if (diameter > 0) {
    for (let i = 0; i <= 1000; i++) {
      let angle = random(TWO_PI);
      let radius = random(0, radiusHigh);

      noStroke();
      ellipse(
        mapX + radius * cos(angle),
        mapY + radius * sin(angle),
        random(1.2),
        random(1.2)
      );
    }
  }
  
// diameter increases when mapX and mapY values are not changing 
  if (diameter > 0 && mapX == mapX) {
    for (let i = 0; i <= 1200; i++) {
      let angle = random(TWO_PI);
      radiusHigh = radiusHigh + 0.032;
      let radius = random(0, radiusHigh);
      ellipse(
        mapX + radius * cos(angle),
        mapY + radius * sin(angle),
        random(1.2),
        random(1.2)
      );
    }
  }
}

// use keypressed to connect to the correct port
function keyPressed() {
  if (key == " ") {
    // important to have in order to start the serial connection!!
    setUpSerial();
  }
}

function readSerial(data) {
  
  pSWstate = SWstate;
  // make sure there is actually a message
  // split the message
  let fromArduino = split(trim(data), ",");
  // if the right length, then proceed
  if (fromArduino.length == 10) {
    // only store values here
    // do everything with those values in the main draw loop
    xPosition = fromArduino[0];
    yPosition = fromArduino[1];
    rvalue = fromArduino[2];
    puvalue = fromArduino[3];
    pvalue = fromArduino[4];
    gvalue = fromArduino[5];
    bvalue = fromArduino[6];
    blvalue = fromArduino[7];
    FSvalue = fromArduino[8];
    SWstate = fromArduino[9];
  }

  //////////////////////////////////
  //SEND TO ARDUINO HERE (handshake)
  //////////////////////////////////
  writeSerial("x");
  
  //plays the spray effect sound only when the button in the joystick if pressed 
  if (pSWstate < SWstate) {
    spraySound.stop();
  } else if (pSWstate > SWstate) {
    spraySound.play();
  }

}

```

## Enclosure and Soldering

<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Final%20Project/wiring.png" width = "370" height = "320"> <img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Final%20Project/soldered%20breadboards.png" width = "370" height = "320"> 

<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Final%20Project/Enclosure%20planning.jpeg" width = "450" height = "360"> 
<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Final%20Project/Sparying%20box.png" width = "320" height = "400"> 

#### Final result
<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Final%20Project/Screen%20Shot%202022-05-12%20at%206.02.01%20PM.png" width = "370" height = "320">   <img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Final%20Project/enclosing%202.png" width = "370" height = "320"> 

## Challenges

## Next Steps

## User Experiences During Showcase

[Video 1]()
[Video 2]()
[Video 3]()
[Video 4]()

## My Contributions
For my contribution, I worked partially on the Arduino and the P5 code. I also worked on the soldering and encasing. My partner Meera and I did most of the work together and not separately. This way, we were able to complete most tasks of the project effectively and efficiently. Personally, I believe I really learned more about the process of sending from Arduino to P5. While practicing this in class I did learn a lot but while doing it constantly throughout the final project I became more confident with it.

## References: 

* [WEB SERIAL p5 ARDUINO](https://editor.p5js.org/itp42/sketches/KDPs5Rl-P)
* [Spray Effect](https://www.dongphilyoo.com/archive/blog/itp/icm/icm-week6-p5-js-serial-port-communication-with-arduino/)
* [About Joystick Sensor](https://create.arduino.cc/projecthub/MisterBotBreak/how-to-use-a-joystick-with-serial-monitor-1f04f0) 
* [P5 Reference](https://p5js.org/reference/)
* [Spray Sound Effect](https://www.soundsnap.com/tags/spray_paint)
* [Brick Wall Image](https://www.freepik.com/photos/white-brick-wall-texture)
* [Graffiti Text Font](https://www.dafont.com/theme.php?cat=606)
