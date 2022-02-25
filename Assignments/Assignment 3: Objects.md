
## Assignment 3: Objects

[Generated Art](https://editor.p5js.org/FatemaAlhameli/sketches/oEvgVJ1XM)


For my production, I was inspired by Casey Reas's talk on chance operations and specifically randomness. The idea of letting a computer generate art really struck my attention and fascinated me. Below are pictures from his video where he presents his process in creating one of his art pieces. As you can see, the starting point is very different from the result, and this is what inspired me to, the randomness of the moving objects creating a wonderful piece. 

![inspo](https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Inspiration%201.png)
![inspo](https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Inspiration.png)


I decided to create something similar using the new material taught this week. I picked my object, which was a circle, and made a class for it. In the class section, I specified adding the x and y coordinates and speed for creating movement in the object. I then created a function called drawCirle, which is where I added an ellipse with its coordinates and size (this.x, this.y, 40, 50);. I wanted the circles to be in random places on the canvas, so I made a for loop, and because I wanted about 150 circles, I created an array in the setup function. In the draw function, I used drawCircle and moveCircle to create and move the object from left to right horizontally. 

![code](https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Assignment%203%20code.png)

To make this generated art look more appealing, I decided to use the variable random for the circles' color and added transparency to them by adding one more number with the RGB. I also did the same for the color of the stroke and also used random for the weight/thickness of the stroke, which gave a much more appealing look to the circles.  The concept behind this artwork is mainly randomness and its ability to add beauty to art. While coding, the only challenge I faced was trying to fully understand the functionality of objects and class, which made it difficult to create artwork. 

![Artwork](https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Assignment%203.png)
