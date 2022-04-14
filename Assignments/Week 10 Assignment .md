
# Musical Instrument
[Final Result Video 1](https://vimeo.com/698949033)

[Final Result Video 2](https://vimeo.com/698949077)

In this assignment, My partner Meera and I created a musical instrument with lime. Through brainstorming our ideas, we have seen examples of people creating similar things with bananas. We looked for fruits that conduct electricity, and we came across citrus fruits. Therefore, we chose limes as they are small and easily portable. Using thick slices of lime, we attached alligator clips to the juice sac of each lime. The alligator clips on the limes are attached to separate resistors, then connected to the ardunio. The instrument functions by the user making contact with a black wire that is connected to GND. Once the user touches the metal tip on the wire and then proceeds to use their other hand to touch one of the limes from the inside, the buzzer speaker activates. 

 <img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Outcasing%20Week%2010.jpg" width = "520" height = "390">   

## Process: 

To create our musical instrument, we used two references [1](https://create.arduino.cc/projecthub/Heathen_Hacks-v2/playing-tones-using-bananas-c4c1ff) and [2](https://www.jameco.com/Jameco/workshop/JamecoBuilds/banana-piano.html). The first reference helped us with writing our code and the second with creating the circuit. To create the circuit we first used six resistors. Compared to class exercises, the resistors were attached differently on the circuit. All six resistors were placed vertically and into two groups of three; however, the top part of each resistor was aligned vertically on the same line, and the bottom part of the resistors was aligned horizontally on the same line. The image below shows the structure of the resistors:

<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Instrument%201.jpg" width = "350" height = "400"> 

At the bottom of each resistor, we used a wire to connect the resistors to separate analog inputs, starting from A0 - A5. We then added two wires red and black on the positive and negative lines that connected to 5V (red wire) and GND (black wire). To connect all resistors to 5V, we used a short purple wire to horizontally connect both resistors' connection points. On the top right side of the purple wire, we attached another red wire that connected to 5V. Next, we used alligator clips at the bottom part of the resistor that connected to the top section of the juice sac of the lime. To install the buzzer speaker, we used a similar circuit that we created in class where we attached the positive side of the buzzer to a pin, in our case 8, and the negative side to GND. Using another black wire, we attached it to GND to act as our digital switch. By touching the metal part of this wire and using your other hand to touch the top of the lime, the buzzer lets out a note. For the code, we started off with initializing our speaker pin and used ```toneMelody``` for the speaker sound. Then in setup, we added ```pinMode``` to declare the speaker as an output. In loop, we used six if statements. The if statement first includes ```analogRead``` with the analog input pin number less than 1000. One thousand represents the value of the ```analogRead```, which ultimately means that the buzzer will only be activated if the value of 1000 is reached. The if statement also includes the tone() code syntax. In the tone syntax, we added the speaker pin variable, note value, and the duration of the tone, in our case, 100 milliseconds. We proceed to add a delay of 10 milliseconds. We copied and pasted the same if statement five times for each analog input pin (limes) and adjusted the note value. After running this code our lime instrument successfully worked. However, we still needed to add an analog sensor. 

[Video of instrument without potentiometer](https://vimeo.com/698659112)

For our analog sensor, we decided to use a potentiometer. The initial idea we had was to use a potentiometer to adjust the volume of the buzzer. But due to a lot of complications, that didn't seem to work. Therefore, we used the potentiometer to adjust the frequency difference of the notes. To do this, we first attached the sensor to our circuit with a 5V wire, analog input wire(A5), and GND wire. To include the sensor we had to remove one of our limes to have space for the sensor. In our code, we used a variable called ```knobValue``` to read the tone values. Following it, we initialized the variable ```freq``` and next to it added the map code, which first included the ```knobValue``` , then the value of the potentiometer (0 - 1023), lastly, the frequency value (0 - 50). Then in each tone code that is in the if statement, we added ```+ freq```. Ultimately when the potentiometer is turned while the lime is playing the speaker, you can listen to the tone frequency change. 

[Video of instrument with potentiometer](https://vimeo.com/698949077)

<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Instrument%202.jpg" width = "420" height = "390">  <img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/fa20a78a-ad3a-4586-a646-15dfb92719d1.jpg" width = "420" height = "390">   
                   <img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Instrument%204.jpg" width = "300" height = "350">   

## Code:

```
int speakerPin = 8;
int potPin = A5;

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  pinMode (speakerPin,OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:

  int knobValue = analogRead(A5);
  int freq = map(knobValue, 0,1024,0,50);
  Serial.print(knobValue);
  
  if (analogRead(A0) < 1000)  {
    tone(speakerPin, 261 + freq , 100);
    delay(10);
  }

  if (analogRead(A1) < 1000)  {
    tone(speakerPin, 277 + freq, 100);
    delay(10);
  }

  if (analogRead(A2) < 1000)  {
    tone(speakerPin, 294 + freq, 100);
    delay(10);
  }

  if (analogRead(A3) < 1000)  {
    tone(speakerPin, 311 + freq, 100);
    delay(10);
  }

  if (analogRead(A4) < 1000)  {
    tone(speakerPin, 330 + freq, 100);
    delay(10);
  }


}

```

## Challenges:
The main challenge we faced during the process of creating our musical instrument was trying to incorporate the potentiometer. We initially wanted the potentiometer sensor to control the volume of the buzzer when the limes play the notes. However, this was a bit difficult to make. When we connected the wires and added the code for it, the buzzer would immediately turn on without stopping every time we ran the code. We tried looking at examples as well as other references and adjusting the code, but it still didn't seem to work. Therefore, we decided to let the potentiometer in control of something else, which was the frequency of the tone. As explained in our process, this was a nice and interesting addition to our instrument. 


## Outcomes and Next Steps: 
This particular assignment was very interesting and insightful for me. My understanding of Ardunio and coding increased significantly as a result of this assignment. As such, I am more confident about working with it and with the different sensors we have. The next step for this mini-project is to include additional sensors that could control elements such as value as well as incorporate a p5 code with it that would make it more interactive and fun.



## References: 

* [Instrument Code](https://create.arduino.cc/projecthub/Heathen_Hacks-v2/playing-tones-using-bananas-c4c1ff)
* [Instrument Cricut](https://www.jameco.com/Jameco/workshop/JamecoBuilds/banana-piano.html)
