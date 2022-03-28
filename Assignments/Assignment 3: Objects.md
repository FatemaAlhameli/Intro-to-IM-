
# Assignment 3: Objects

[Generated Art](https://editor.p5js.org/FatemaAlhameli/sketches/oEvgVJ1XM)


For my production, I was inspired by [Casey Reas's talk on chance operations](https://vimeo.com/45851523) and specifically randomness. The idea of letting a computer generate art really struck my attention and fascinated me. Below are pictures from his video where he presents his process in creating one of his art pieces. As you can see, the starting point is very different from the result, and this is what inspired me to, the randomness of the moving objects creating a wonderful piece. 

<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Inspiration%201.png" width = "500" height = "500"> 
<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Inspiration.png" width = "500" height = "500">  

I decided to create something similar using the new material taught this week. I picked my object, which was a circle, and made a class for it. In the class section, I specified adding the x and y coordinates and speed for creating movement in the object. I then created a function called ```drawCirle```, which is where I added an ellipse with its coordinates and size ```(this.x, this.y, 40, 50);```. I wanted the circles to be in random places on the canvas, so I made a for loop, and because I wanted about 150 circles, I created an array in the setup function. In the draw function, I used ```drawCircle``` and ```moveCircle``` to create and move the object from left to right horizontally. 

## Code:
```
let circle = [];
let noCircle = 150;
function setup() {
  createCanvas(400, 400);

  // Position of circles
  for (let i = 0; i < noCircle; i++) {
    let xPos = random(0, width);
    let yPos = random(0, height);
    circle[i] = new Circle(xPos, yPos);
  }
}

function draw() {
  background(247, 232, 223, 10);

  //Stroke color and thickness
  stroke(random(0, 255), random(120, 255), random(0, 255));
  strokeWeight(random(1, 3));

  //Creating the circles
  for (let i = 0; i < noCircle; i++) {
    circle[i].drawCircle();
    circle[i].moveCircle();
  }
}

// Class and Object
class Circle {
  constructor(xPos, yPos) {
    this.x = xPos;
    this.y = yPos;
    this.speed = 3;
  }

  //Shape and color of oject
  drawCircle() {
    fill(random(0, 255), random(200, 255), random(0, 255), 160);
    ellipse(this.x, this.y, 40, 50);
  }
  // Movemnet of circles
  moveCircle() {
    this.x = (this.x + this.speed) % width;
  }
}

```

To make this generated art look more appealing, I decided to use the variable random for the circles' color and added transparency to them by adding one more number with the RGB. I also did the same for the color of the stroke and also used random for the weight/thickness of the stroke, which gave a much more appealing look to the circles.  The concept behind this artwork is mainly randomness and its ability to add beauty to art. While coding, the only challenge I faced was trying to fully understand the functionality of objects and class, which made it difficult to create artwork. 

## Final Outcome:
![Artwork](https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Assignment%203.png)

## Next Steps: 
* Smoother random transitions, so that it is not disturbing to the eye
* Different speed for differnt ellipses
* Make the ellipses gilde sideways rather than having them move all in the same position to the same direction
