# Assignment 4: Generative Text

[Generative Text Code](https://editor.p5js.org/FatemaAlhameli/sketches/Op07FF22Z)

For this assignment, I wanted to create a text that moved in a circular motion and has a 3D effect to it rather than moving in 2D. I started off by generating a text using the text function and then added a font. I used the functions preload and textFont(font); to add the font. In order to adjust the font I just textSize(); and textAlign();. Additionally, I used CENTER in the textAlign() function in order to have the text in the center of the canvas which made it easier place the text where I wanted it. 

![code](https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Code%203.png)

I managed to add movement in the text by using frameCount however it wasn't visually appealing as I wanted it to be. I referred to the p5 reference to get some ideas of what I can do more with text and came across a text reference of movement by using WEBGL mode. I used millis(); as time, millis is to keep track of the number of milliseconds since the play button has been pressed. Therefore, the time would always keep on playing. Moreover, I added the variables rotateX and rotateZ to specify the directions of movement. RotateZ moves the text clockwise and rotateX moves the text around the X axis. 

With the aid of this mode and rotation, I managed to have the text move in the way I wanted it. To make it more interesting I moved the background to setup for the text to leave a trace during it movement which ultimately gave a nice 3D-like effect. I used fill(); to change the color of the text as well. An obstacle I faced while creating this generated text was I couldn't load the font I wanted. I then figured out that I needed to add the function textFont(font); not only the preload function. 


## Final Result

![picture](https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Text%202.png) ![picture2](https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Text%20Art.png)
