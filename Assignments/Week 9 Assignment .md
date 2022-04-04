
# Digital and Analog Sensors

[Digital Sensor Video](https://vimeo.com/695490494)

[Analog sensor Video](https://vimeo.com/695835271)

For this assignment, I have created two sensors digital and analog with the aid of this week's class examples. For digital, I used the push button. The push-button function is that when it is pushed, a morse code would appear. The morse code spells out my name. When the push button is released, the LED remains on. For analog, I generated a photoresistor that turns on when it's dark (covered) and off when exposed to light. Ultimately, this acts as an emergency light and was my inspiration when creating this analog sensor. 


<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/LED%20Digital%202.jpg" width = "350" height = "400">  <img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Analog%201.jpg" width = "350" height = "400">     

## Process

#### Digital:

[Fading attempt on Tinkercad](https://www.tinkercad.com/things/kEO6aWOvEHI-epic-crift-snaget/editel?sharecode=1cB7sP_C_gWXQi-U-84rENBAoPBTB3w-3VbSQZvyU9w)

[Failed Fading Attempt Video](https://vimeo.com/695489761)

By using the examples from class, I created a circuit for a digital sensor, the push button. For this sensor, I initially wanted to make the LED fade in brightness when the button is pressed and remain on when it's not pressed. However, this idea didn’t seem to be successful. I first made a simulation on Tinkercad and added my code. To create the circuit I followed the class example of when we created the push button. I first added a push button with a red wire underneath it that connected to 5 volts with another red wire as well. I also connected a yellow wire from the push button to number 3, with a 10 kΩ resistor below the push button and yellow wire. Near the button, I added a red LED. Below the negative side of the LED, I added a 330 Ω resistor and connected it to GND by using two black wires. To write my code, I began with what we learned in class this week. Firstly, I initialized the LED pin number which was 7, and the button pin number which was 3 as well as the ```buttonState``` which is 0. In setup, I added the LED pin as an output since I wanted to turn it on and the button pin as input since it would be pressed in order to turn on the LED. I did this by using ```pinMode```. I also used digitalRead for the button state where I wrote the code ```buttonState = digitalRead(buttonPin);```. This means that based on the state of the push button, the LED will turn on. In the loop, I used an if statement that says if the button state is high (voltage is 5, thus LED is on), the LED should fade in brightness. I used the Arduino reference for the fading code, which included ```fadeValue``` and ```analogWrite```. Following it I had an else statement, indicating if the fading stops the LED light would remain on. 

This worked and was successful on Tinkercad, but when I created the same thing on my Arduino and circuit board, it didn’t work. The LED only blinks when the button is pressed. So I decided to go with another idea, which is that when the button is pushed the LED would spell my name in morse code. To begin, I had the same circuit connected to my Arduino. All I did was modify and make additions to my code. I used a [youtube video](https://www.youtube.com/watch?v=6mLytyKEU5Q) to help me with creating the morse code to spell my name. Following the video instructions, I added a new function called ```switchLED```. What this function does is that with ```digitalWrite``` the LED pin is high, then there is a delay, then the LED pin is low (0 voltage, thus LED is off), and then another delay. I initialized two variables called ```shortTime = 300``` and ```longTime = 900```. I then replaced the fading code in the if statement with the new function ```switchLED``` and next to it brackets indicating if long or short time. The purpose of these two types of timing is for the morse code. I looked at a chart that hard the alphabet of the morse code and spelled my name by using ```switchLED``` and ```delay```. Lastly, I connected my Ardunio to my laptop, and it worked. The LED blinked by name in more code. 


#### Result: 
[Digital Sensor Video](https://vimeo.com/695490494)

 <img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/LED%20Digital.jpg" width = "350" height = "400">   

## Code: 
```
const int buttonPin = 3;
const int ledPin = 7;

int shortTime = 300;
int longTime = 900;
int buttonState = 0;

void setup() {
  // put your setup code here, to run once:
  pinMode(ledPin, OUTPUT);
  pinMode(buttonPin, INPUT);

  buttonState = digitalRead(buttonPin);
}

void loop() {
  // put your main code here, to run repeatedly:

  buttonState = digitalRead(buttonPin);
  if (buttonState == HIGH) {
    // turn LED on:
  

  switchLED(shortTime);
  switchLED(shortTime);
  switchLED(longTime);
  switchLED(shortTime);
  delay(longTime);

  switchLED(shortTime);
  switchLED(longTime);
  delay(longTime);

  switchLED(longTime);
  delay(longTime);

  switchLED(shortTime);
  delay(longTime);

  switchLED(longTime);
  switchLED(longTime);
  delay(longTime);

  switchLED(shortTime);
  switchLED(longTime);
  delay(longTime);

  } else {
	digitalWrite(ledPin, HIGH);
  }
}

void switchLED( int timing){
  digitalWrite(ledPin, HIGH);
  delay(timing);
  digitalWrite(ledPin, LOW);
  delay(shortTime);
}
```
#### Analog (Emergency Light):

[Tinkercad simulation](https://www.tinkercad.com/things/6ag6zDRdWbg-tremendous-luulia/editel?tenant=circuits)

For this sensor I was inspired by the emergency lights that are located in parking lots. These emergency lights turn on when all the other main lights turn off. I used a photoresistor to turn on/off the LED light for my analog sensor. When the photoresisitor senses the dark it turns on the LED and when exposed to light it turns off.  By using the [Ardunio reference](https://create.arduino.cc/projecthub/siddh-1/turn-on-off-of-led-with-photoresistor-27a206) for code and circuit guidance, I was able to make the photoresistor work. On the breadboard, I added my photoresistor and connected it to a ten kΩ resistor that connected to GND as well as two wires that connect to 5V and A0. I included a red LED that has a  330Ω resistor that is connected to GND and number 13 on the Arduino.  For the code, I first initialized the LED I am using, the analog input, and the value that is equal to zero. In setup, I use ```pinMode``` to make the LED output and the photoresistor as an input. Throughout the code, Serial print is used to track the value of the photoresistor. In loop an if statement is included that says if the value of the photoresistor less than 50 then the LED should turn on, else it should be off.  This code works due to ```analogRead``` and the ```Serial.println``` throughout the whole algorithm. 

#### Result: 
[Analog sensor Video](https://vimeo.com/695835271)

<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Analog%202.jpg" width = "350" height = "400">   

## Code: 

```
const int ldrsen = A0;

int Led = 13;
int value = 0;


void setup() {
  // put your setup code here, to run once:
  delay(2000);
  Serial.begin(9600);
  pinMode(Led, OUTPUT); 
  pinMode(ldrsen, INPUT);

  Serial.println("======Starting the Test======");
  Serial.println("You should see the Led blinking every 2 sec");
  digitalWrite(Led, HIGH);
  delay(200);
  digitalWrite(Led, LOW);
  delay(200);

  Serial.println("Test 1 is completed");
  Serial.println("Now testing the Photoresistor, Make sure it is connected to the Pin A0");
  delay(2000);
  Serial.println("Starting the test now!");   

   rerun:
  value = analogRead(ldrsen) /4;

    if(value >1){
    Serial.print("The Photoresistor is connected and here are some value: ");
    delay(200);
    Serial.println(value); 
    }
    else{
      value = analogRead(ldrsen)/4 ;
        if(value<0)
          Serial.println("Hmm the Photoresistor is not connected");
          Serial.println("Retrying in 5s");
          delay(5000);
          goto rerun;
        }
          Serial.println("======END======");    
}

void loop() {
  // put your main code here, to run repeatedly:
  value = analogRead(ldrsen)/4;
  Serial.println(value);
  delay(10);
    if(value < 50){
    digitalWrite(Led, HIGH);
  }else{
    digitalWrite(Led, LOW);
  }




}


```

## Challenges

This homework assignment was one of the homework I faced many difficulties with. I believe this assignment was a challenge within itself that was a bit frustrating however I learned a lot from it and made me more familiar with Ardunio. The first challenge I faced was that my Arduino didn't work when I was generating the push button. It turns out that I accidentally connected the 5V and GND lines. It took me a while to figure this out and with the help of the professor, I was able to fix the problem. Another challenge I faced was when creating the photoresistor was that when I uploaded the code the LED would only turn on and off once when I covered the photoresistor and then the LED would stop working.

## Next Steps
* Add a potentiometer with the push button to control the brightness of the LED and make it play a role with more code.

* Perhaps have the LED fading quickly instead of blinking the morse code.

* For the photoresistor, try and make it also blink in morse code. 

## References: 
[Ardunio Fading Reference](https://www.arduino.cc/en/Tutorial/BuiltInExamples/Fading)

[Ardunio Photoresistor Reference](https://create.arduino.cc/projecthub/siddh-1/turn-on-off-of-led-with-photoresistor-27a206)

[Morse Code](https://www.youtube.com/watch?v=6mLytyKEU5Q)

[Class Examples](https://github.com/MathuraMG/IntroductionToInteractiveMedia/tree/master/Week9)


