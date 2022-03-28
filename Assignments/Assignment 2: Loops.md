
# Assignment 2: Loops

[Simple art using loops](https://editor.p5js.org/FatemaAlhameli/sketches/i_dG9Pp3W)

![Image](https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Assignment%202.png)

## Simple Art Work with Loops:
This work of simple art is an abstract piece. By using a for loop I was also to create shape and form in my art. This piece has a glitchy effect that was created by using ```random``` for the stroke thickness. The process of creation was based on trial and error. After random attempts I generated a loop of diagonal and random lines from two corners of the canvas. After achieving these lines, I remembered a logo that I came across that had an eye catching background. I found the design of the Vector Institute for Artificial Intelligence logo background extremely eye catching and was inspired to add ellipses in my simple art piece. 

<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/2017-09-26-vector-logo-resized.jpg" width = "250" height = "250">  

## Creation Process:
When I started this assignment I first kept creating for loops with ellipses and rectangles. However, I felt the drawing still looked boring. So I started over and began to explore creating lines with for loops. I kept playing around with the line loop until I got this combination of horizontal and vertical lines dragged, which looked pretty interesting. I kept switching and changing the place of the terms width and height until I achieved my desired design (this is shown in my code below). Once I was satisfied with what I created  on the bottom left corner, I tried doing the same to the top right corner. I then attempted and succeeded to do the same on the top right corner. Again, by only changing the place of the height and width I was able to create the same design on the opposite side of the canvas. To add more lines I created separated diagonal lines from the bottom left corner up to the middle. Then I did the same thing for the top right corner, which led them all to connect. Lastly, I added a diagonal row of ellipses from the top left corner to the bottom right corner. This process was firstly based on trial and error. Ultimately playing around and exploring the code allowed me to achieve this piece. 

## Challenges and Changes:
To play around more with the drawing I added a random stroke weight, which gave the lines a more appealing look. I also tried to create random sizes for the ellipses, however, it was disturbing to the eye so I kept them all at the same size. A challenge I faced while creating this drawing was that every time I tried to fill the lines with color it did not work. I didn’t understand why this happened because it was working the past week. Another challenge I faced was that when I wanted to create a diagonal set of ellipses I struggled to do so at first. I tried a couple of ways however, it was frustrating. I referred to an external resource which was a [YouTube video](https://www.youtube.com/watch?v=V56cH9R_X4k) to aid me in creating my idea.  Overall, I feel more confident with using for loops, as at the beginning of the week I struggled a bit with understanding them. For my next steps, I would like to incorporate animation with loops and create more things with them. 

## Next Steps:
* Explore loops in different shapes and incorporate them 
* Add animation to the ellipses, perhaps have them move up 
* Smooth random size changes 

## Code:

```
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(110, 110, 255);

  for (let i = 0; i < width; i = i + 50) {
    strokeWeight(random(1, 3));
    line(0, i, i, height);
  }
  for (let i = 0; i < width; i = i + 50) {
    line(0, height, i, i);
  }

  for (let i = 0; i < width; i = i + 50) {
    line(height, i, i, 0);
  }

  for (let i = 0; i < width; i = i + 50) {
    line(i, i, height, 0);
  }
  for (let i = 0; i < 20; i = i + 4) {
    fill(0);
    ellipse(i * 25, i * 25, 50);
  }
}


```
