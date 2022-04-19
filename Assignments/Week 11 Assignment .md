## Exercise 1 & 2: 

In exercise one, I was able to take code from Ardunio to P5 by using serial control. I used two sensors on Arduino, which were a potentiometer and a photoresistor, to control an ellipse on p5. By controlling the ellipse, I made it move horizontally and vertically. Ultimately, I was able to draw lines of ellipses throughout the p5 editor canvas. In the Arduino code, I first declared the analog sensor's input pins. The potentiometer was A0, and the photoresistor was A1. In setup, I added ```Serial.begin(9600);``` so that I can print the values of the sensors and make sure they are working on Ardunio. Therefore, in loop I declared two variables, ```potValue``` and ```prValue``` that are equal to ```analogRead(POT/PR)```.This means that when I want to print the values of the sensors, the code reads them and then prints. Following that, I printed the values by using ```Serial.print``` and ```Serial.println```. To test this, I opened the serial monitor to make sure the values of the sensors were printing correctly. I then closed the serial monitor and opened p5 serial control, and connected it to the correct port to make sure the values are also printing correctly. Next, I copied and pasted the code in the p5 serial control in the p5 web editor. I made sure to make the necessary additions to the Html file. In the function ```gotData``` I split the values of the sensors that were stored in ``` currentString``` and initialized them in a variable called values. In the draw function, I created an ellipse without specifying the x and y coordinates. For the x, I mapped the values of the potentiometer to go from 0 to the width of the canvas. Similarly, for the y, I mapped the values of the photoresistor from 0 to the height of the canvas. Ultiemently, this will allow the potentiometer to draw the ellipses horizontally and the photoresistor vertically. To play around I changed the color of the ellipse and made it random RGB values ```fill(random(0, 120), random(0, 70), random(0, 150));```.  

For exercise two, I made additions to the code I had already for the previous exercise. I first began by adding an LED to my circuit board and connecting it to the Ardunio. Unlike exercise 1, I had to send code from p5 to Ardunio. Therefore, in Ardunio, I initialized the LED pin number and in setup, made it an output by using ```pinMode```. In loop, I added ```intByte = Serial.read``` and an if statement that indicates if ```intByte``` is equal to 0, then the LED should be off. The code for that would be ```digitalWrite(LED, LOW);```. Else the LED should be on. I then went through the same process of converting to p5 serial control. In the p5 editor, I added an if statement with a ```mouseIsPressed``` function stating that if the moused is pressed ```serial.write(1)```, else it should be ```serial.write(0)```.  1 means that the state of the LED is on and 0 is off. Thus when you press on the canvas, the LED will light up, and if you release it will turn off. 

## Arduino Code:
```
const int POT = A0;
const int PR = A1;
const int LED = 3;

void setup() {
  Serial.begin(9600);
  pinMode(LED, OUTPUT);
  
  Serial.begin(9600);
  while (Serial.available() <= 0) {
    Serial.println("hello"); // send a starting message
    delay(300);              // wait 1/3 second
  }

}

void loop() {

  // read information from p5
  int intByte = Serial.read();
  switch(intByte) {
    case 1:
      digitalWrite(LED, HIGH);
      break;
    default:
      digitalWrite(LED, LOW);
      break;
  }

  // send information to p5
  int potValue = analogRead(POT);
  int prValue = analogRead(PR);
  Serial.print(potValue);
  Serial.print(",");
  Serial.println(prValue);


  
}
```
## P5 Code:
```
let serial;
let latestData = 0;
let values = [0, 0];

function setup() {
  createCanvas(600, 600);

  serial = new p5.SerialPort();

  serial.list();
  serial.open("/dev/tty.usbmodem1101");

  serial.on("connected", serverConnected);

  serial.on("list", gotList);

  //gotData function is called when we rx data through the serial port
  serial.on("data", gotData);

  serial.on("error", gotError);

  serial.on("open", gotOpen);

  serial.on("close", gotClose);
}

function serverConnected() {
  print("Connected to Server!!!!");
}

function gotList(thelist) {
  print("List of Serial Ports:");

  for (let i = 0; i < thelist.length; i++) {
    print(i + " " + thelist[i]);
  }
}

function gotOpen() {
  print("Serial Port is Open");
}

function gotClose() {
  print("Serial Port is Closed");
  latestData = "Serial Port is Closed";
}

function gotError(theerror) {
  print(theerror);
}

function gotData() {
  let currentString = serial.readLine();
  // console.log(currentString);

  trim(currentString);
  if (currentString.length > 0) {
    // console.log(currentString);

    values = split(currentString, ",");
    // console.log(values);
  } else {
    return;
  }

 
}

function draw() {
  // let bg = map(latestData, 0,1023,0,255);
  // background(bg);

  let x = map(values[0], 0, 1023, 0, width);
  let y = map(values[1], 350, 750, 0, height);
  fill(random(0, 120), random(0, 70), random(0, 150));
  ellipse(x, y, 30, 30);

  if (mouseIsPressed) {
    serial.write(1);
  } else {
    serial.write(0);
  }
}

```


## Exercise 3:

For exercise 3, we had to use the [gravity wind example](https://editor.p5js.org/aaronsherwood/sketches/I7iQrNCul) of a bouncing ball to control the wind direction of the ball and make an LED light-up every time the ball bounces. For the Arduino code, I used the same code as the previous exercises and only excluded the code for the photoresistor. I converted it to p5 serial control and used the code given in the p5 serial control. I merged it with the code from the example and made sure it worked. I looked for the code that bounced the ball, which was an if statement. In that if-statement I added ```serial.write(1)``` which means the LED should turn on else ```serial.write(0)```. At first, this did not work out because it turned out that I had mistakenly put LOW for both ```digitalWrite```. Also another obstacle that I faced was that when I ran the code on p5, I had to go back on serial control and press okay for the code to work. This only occurred twice, and after that, it worked normally. 

Using the potentiometer the wind direction of the ball can be moved. The wind direction in the example is controlled by a key pressed function with a variable of wind.x that had two values to move -1 and 1. I first initialized a variable named ```windValue```. In the function ```gotData``` the values of the potentiometer are stored in a variable called ```latestData```. Therefore, in ```gotData``` I used ```windValue``` to map the values of the potentiometer and make the only go from -1 to 1.  Following this, I made wind.x equal to the variable wind value. Lastly, I deleted the key pressed function. The ball successfully moved direction, and an LED would turn on once it bounced. To explore, I played with the values in the map that ultimately changed the speed of the ball. 


Arduino Code:
```
const int POT = A0;
const int LED = 3;




void setup() {
  // put your setup code here, to run once:

  Serial.begin(9600);
  pinMode(LED, OUTPUT);

}

void loop() {
  // put your main code here, to run repeatedly:


  if(Serial.available()>0) {
    int intByte = Serial.read();
    if(intByte == 1){
      digitalWrite(LED, HIGH);
    } else {
      digitalWrite(LED, LOW);
    }
  }


 int potValue = analogRead(POT);
  Serial.println(potValue);
  // Serial.print(",");

}
```
P5 Code:
```
let serial;
let latestData = "waiting for data";
let windValue;
let velocity;
let gravity;
let position;
let acceleration;
let wind;
let drag = 0.99;
let mass = 50;

function setup() {
  createCanvas(windowWidth, windowHeight);

  noFill();
  position = createVector(width / 2, 0);
  velocity = createVector(0, 0);
  acceleration = createVector(0, 0);
  gravity = createVector(0, 0.5 * mass);
  wind = createVector(0, 0);

  serial = new p5.SerialPort();

  serial.list();
  serial.open("/dev/tty.usbmodem1101");

  serial.on("connected", serverConnected);

  serial.on("list", gotList);

  serial.on("data", gotData);

  serial.on("error", gotError);

  serial.on("open", gotOpen);

  serial.on("close", gotClose);
}

function serverConnected() {
  print("Connected to Server");
}

function gotList(thelist) {
  print("List of Serial Ports:");

  for (let i = 0; i < thelist.length; i++) {
    print(i + " " + thelist[i]);
  }
}

function gotOpen() {
  print("Serial Port is Open");
}

function gotClose() {
  print("Serial Port is Closed");
  latestData = "Serial Port is Closed";
}

function gotError(theerror) {
  print(theerror);
}

function gotData() {
  let currentString = serial.readLine();
  trim(currentString);
  if (!currentString) return;
  // console.log(currentString);
  latestData = currentString;

  windValue = map(latestData, 0, 1023, -1, 1);
  wind.x = windValue;
}

function draw() {
  background(255);
  applyForce(wind);
  applyForce(gravity);
  velocity.add(acceleration);
  velocity.mult(drag);
  position.add(velocity);
  acceleration.mult(0);

  ellipse(position.x, position.y, mass, mass);
  if (position.y > height - mass / 2) {
    velocity.y *= -0.9; // A little dampening when hitting the bottom
    position.y = height - mass / 2;
    // print("bounce");
    serial.write(1);
  } else {
    serial.write(0);
  }

  //serial.write(position.y);

  text(latestData, 10, 10);
  // Polling method
  /*
 if (serial.available() > 0) {
  let data = serial.read();
  ellipse(50,50,data,data);
 }
 */
}

function applyForce(force) {
  // Newton's 2nd law: F = M * A
  // or A = F / M
  let f = p5.Vector.div(force, mass);
  acceleration.add(f);
}


```
