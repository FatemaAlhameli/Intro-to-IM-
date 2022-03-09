
# Boat Maze Game 


#### Fatema Alhameli
#### Introduction to Interactive Media 
#### Midterm Project
#### 10 March 2022




[Link to play the game](https://editor.p5js.org/FatemaAlhameli/full/RcoDaoymz)

## Game Description 

This maze game project is a fun experience for individuals. It aims to keep a player intrigued by having a maze to solve with limited time. At the top of the game canvas is a short list of instructions that specifies to the player the story of the game and how to play it. The player in the game is a boat, and he/she is supposed to get to the island because a storm is coming in. To do so the player needs to solve the maze and get to the endpoint which is the island while being aware of the time limit. The time limit is displayed as a decreasing red line. The player can move the boat by using the arrow keys and can refresh the game by pressing the key “R”. The game begins with a start screen that tells the player to double click to start after they do so, the game and timer both start. If they fail to get to the island on time, they lose the game, and if they succeed, they win. 

## Game Idea 

Growing up, I have always loved solving puzzles and mazes. I used to solve the mazes that were on the back of cereal boxes. So when I heard that our midterm project is a game, the first thing that came to my mind was creating a maze game. Although I didn't have a story for the game, I was sure I wanted it to be a maze. The week we were meant to start thinking of game ideas, my family and I went to my grandparent's beach house for the weekend. During the weekend we couldn't go out on the boat due to the bad weather. Moreover, when I went back to class the following week, I thought of my game story of having the main object in the game be a boat. As well as have a time limit that represents the time left for a storm to come in.

## Maze 

Initially, for the maze, I was using an algorithm from the [Coding Train videos](https://www.youtube.com/watch?v=HyK_Q5rrcr4) to create a maze. However, this algorithm is a maze generator that creates a new random maze every time the code runs. After I created it, I realized that it would not be suitable for my game because it does not fit the context/idea of my game. Since I wanted a specific endpoint to be in the game, that was not possible with the generator since it created a different maze every time the program ran. The documentation of the maze generator can be found [here](https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Midterm%20Project/Documentation%201.md). 

Before I started my maze I drew a digital sketch of my maze. To create a maze of my own with specific walls and pathways, I used the [professor's code example](https://editor.p5js.org/itp42/sketches/dBeLZC8mm) of using a grid for generating games. The code example consists of a grid class that indicates the size, number of rows, and columns in the grid. In the class is a draw function, which includes the code to draw the rectangles/squares of the rows and columns of the grid. In addition, it indicates the value of the grid. In other words, if the rectangle value is 0, it would be colored in blue, and if its value is 1, it would be colored brown. Therefore, to find the grid value, it is necessary to loop through the rows and columns and find the grid value at that position in the array. Another important function in the code is the ```getCurrValue``` that will allow us to know the x and y values of a certain position in the grid. Moreover, adding a return function to this in order to call this function and store the answer in a variable. Ultimately, in the constructor of the grid class, I am able to create an actual grid with the same number of rows and columns I need by using numbers 0 and 1 to color the grid and create the maze. In setup, I can create a new grid object and initialize the size, the number of rows, and columns to best my game. Lastly, to make sure it actually looks like a maze, I removed the stroke. 

<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Maze%20Sketch.jpg" width = "350" height = "200">   

<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/example.png" width = "250" height = "200">  <img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/New%20maze%201.png" width = "250" height = "200">  <img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/New%20Maze.png" width = "250" height = "200">

## Boat 

In my game, the boat is the main object that the player will be interacting with. To create the boat, I made a class for it with an x and y position with ```this.x``` and ```this.y```. Then I created a ```drawBoat``` function to create the shape of the boat. In order to do so, I used two right-angled triangles to draw the top of the boat and a trapezoid for the body of the boat. To create a trapezoid, I used the ```beginShape``` and ```endShape``` function with specifying the vertices of the shape.  In order to make sure the boat can be drawn anywhere on the canvas without having to identify all the coordinates of the shapes, I added the original coordinates numbers to the ```this.x``` and ```this.y``` variables in the syntax of the shapes. 

After drawing the boat, I needed to make it move. At first, I was unsure what to use between ```mouseX``` and ```mouseY``` or ```keyIsPressed``` to move the boat. After giving it a bit of thought, using ```keyIsPressed``` to move the boat with the key arrows would be a much more fun option for a player in my point of view. Therefore, I decided to use it. To do so, in the boat class, I created a function called ```moveBoat```.  In this function, I used an if statement to specify that if the ```keyCode``` the left arrow should be moved to the left. This is possible because after I specified the key, I wrote ```this.x - 1``` which means that the x value should decrease by one when the left key is pressed. Thus, allowing it to move to the left side. On the line after it, I added an else if statement to do the same thing for the other right, up, and down keys. Then I went to the draw function and added an if statement indicating that if the key is pressed the boat should move. With this, the boat was successfully able to move. However, I faced an obstacle which was that boat is able to move across the whole maze even the brown walls of the maze. What I needed was for the boat to move only in the blue pathways, and to do so, I needed to add restrictions. I used the print function to find out the value of the blue pathways and the brown walls. It showed that the blue pathways are 1. So in the if statement in the draw function that states if ```keyIsPressed``` the boat should move, I added if ```keyIsPressed && currGrid == 1```. Ultimately this means that the boat should only move on the areas where the grid value is 1. This worked, but once the boat touched a brown wall, it would stop moving.  Thus, I needed to attempt other ways. I needed to make sure that the boat checked its position value before moving. To do so, I needed to save the position of the boat’s x and y and later match the position of the boat with the position of the grid. If the grid value returns to 1, then this means it’s value is on the brown walls, so the boat should not move there, and if it returns to 0, then this means it's the blue path, so the boat should move now. Hence the boat only moves if the boat`s x and y are moving according to "0".


## Endpoint 

The endpoint of my maze is the island. Therefore, I decided to use an image as my endpoint. To do this, I first uploaded my image in p5.js and made sure it had a transparent background. I then used the ```preload()``` function that included the ```“name of the image” =  loadImage(“ URL”)``` to add the image. To make the image visible in setup I used the syntax ```image(img, x, y, [width], [height])```. In the syntax, I specified the coordinates of the maze’s endpoint to make it appear in the right location. 

## Timer 

The timer is one of the important elements in my game. The purpose of the timer is to let the player know how much they have left to get the boat to the island. At first, I was thinking of having a normal countdown timer. I began researching and came across a [countdown code example] (https://editor.p5js.org/marynotari/sketches/S1T2ZTMp-). However, for my game, I did not want a normal. I had an idea of making the timer a red line on top of the canvas that decreases and indicates the time left to the player. Using the countdown timer example code which is if the frame count is divisible by 60 it means that a second has gone by and when it reaches zero the timer will stop. The red line is basically a rectangle that was created with the ```rect()``` code in p5js. It`s been created that as you run the code the line would decrease, thus indicating the time. It is created from the canvas width, and it decreases itself according to the timer. As the timer decreases, the rectangle also decreases as its value is in relation to the timer. The written code for this is ```b1=width of canvas/timer;```.  Which in my case was b1 = 426 / 35. 

<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Timer%20for%20maze.png" width = "250" height = "200"> 

After the countdown timer, I added an if statement that specifies if the time is equal to zero and the player hasn't reached the island (endpoint), then they lose, so the “Game Over” screen would appear. The “Game Over” screen should appear only when the player hasn't reached the endpoint point, and they ran out of time. Visversa, I wrote an if statement that if the boat position is equal to the island position before the timer ends then the player wins. Thus, the “You Win”  screen appears.

<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/Game%20over.png" width = "250" height = "200">  <img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/you%20win%20screen.png" width = "250" height = "200">

## Restart buttons 

For the game, the player can restart the game once they have lost or won by pressing the key “R”. This is possible because I generated an if statement that states if the keys “r” or “R” are pressed the game, will restart the timer and new position of the boat which is the starting position. To this small chunk of code, I added the ```noLoop();``` function at the beginning and the ```loop();``` function to the end. This will allow the code to run continuously again. 

## Sound

For sound, I had the idea of adding sound effects to when the player wins or loses. Therefore, I downloaded two mp3 sound effect files in my assets folder and named them accordingly to win or lose sound effects. I then loaded the sound in my preload function and added them to the “You Win” and “Game Over” screens. However, when I played the game and restarted, the lost sound effect would still keep on playing.  To solve this problem, I needed to add and initialize a new variable called ``` let isSoundPlaying = false;```. Using this variable, I created an if statement in the code of the “You Win” and “Game Over” screens stating that sound should not play since it is equal to false, but if the player wins or loses the variable ```isSoundPlaying```  should equal true. 

## How to start the game?

My start screen was one of the last elements to add to my game code. By using the [Professor’s explanation](https://editor.p5js.org/itp42/sketches/hCa_xCoY5) I was able to incorporate it into my game. It works by clicking the screen twice. This is possible because I used a function called ```doubleClicked()```. By initializing a new variable called ```startScreen = 0```  I then created an if statement in the draw function that states that if the start screen value is 1 then the text "double click to start" should appear. I continued with an else if statement indicating that if the start screen value is 1 then the game mechanics would start, hence the actual game starts. Going back to the double-clicked function, I created an if statement specifying that if the mouse is double-clicked and the start screen value is 0 it should increase to 1. Thus, the game starts. 
 
<img src= "https://github.com/FatemaAlhameli/Intro-to-IM-/blob/main/start%20screen.png" width = "250" height = "200">

## Next steps

* Add new levels with difficulty of game increasing 
* Add obstacles to intensify the difficulty of the game 
* Add a component that allows the player to gain points when they win
* Try to find shortcuts for some of the code in my game to make it simpler to add complexity to the game. 


## Code Snippets


### Grid Class:

```
// Grid class, which is the outline of the maze.
class Grid {
  constructor(size, rows, cols) {
    //Create an actual grid/maze with 0s and 1s
    this.grid = `
      11111111111111111
      00000000010000001
      00111110010111011
      10001000110001001
      10001110010001001
      10000001110111101
      10011100010001001
      11010100010001001
      10010101111101011
      10000100000001001
      10010110010001001
      11010111111001001
      10010010001001101
      10011100001001001
      10110010011111001
      10000001010000001
      11111111110011111`;
    this.grid = this.grid.replace(/\s/g, ""); // IMP : This removes all the whitespaces in the grid.
    this.size = size;
    this.rows = rows;
    this.cols = cols;
    this.currVal = 0;
  }

  draw() {
    //loop through the rows and columns and find the grid value at that position in the array

    for (let i = 0; i < this.rows; i++) {
      for (let j = 0; j < this.cols; j++) {
        //get the grid value - is it 0 or 1
        let gridVal = this.grid[j * this.rows + i];

        // Creates the elements of the gids and depending on the value of the grid a color can be chosen. Blue and Brown
        if (gridVal == 0) {
          fill(127, 205, 255);
          rect(i * this.size, j * this.size, this.size, this.size);
        } else if (gridVal == 1) {
          fill(164, 116, 73);
          rect(i * this.size, j * this.size, this.size, this.size);
        }
      }
    }
  }

  // Given an x and a y it gives the grid value at that position.
  getCurrValue(x, y) {
    console.log(boat.x + 15);
    console.log(boat.y + 70);
    let gridX = floor((x + 15) / this.size);
    let gridY = floor((y + 70) / this.size);
    //  print(gridY * this.cols + gridX);
    return this.grid[gridY * this.cols + gridX]; // using the return function will give this value when the function is called. So you can call this function and store the answer in a variable.
  }
}


```

### Boat Class:

```
// Boat class with a constructor containing x and y position of the boat
class Boat {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  // The creation of the boat structure using triangles, begin and end shape for the body of the boat. As well as fill color white and brown.
  drawBoat() {
    fill(255, 255, 255);
    triangle(
      this.x + 27,
      this.y + 70,
      this.x + 38,
      this.y + 70,
      this.x + 27,
      this.y + 53
    );
    triangle(
      this.x + 15,
      this.y + 70,
      this.x + 25,
      this.y + 70,
      this.x + 25,
      this.y + 50
    );
    // The trapezoid shape for the body of the boat
    fill(71, 50, 49);
    beginShape();
    vertex(this.x + 15, this.y + 70);
    vertex(this.x + 43, this.y + 70);
    vertex(this.x + 38, this.y + 80);
    vertex(this.x + 17, this.y + 80);
    vertex(this.x + 10, this.y + 70);
    endShape();
  }
  // A function that moves the boat using the arrow keys if they are pressed.
  moveBoat() {
    if (keyCode == LEFT_ARROW) {
      this.x = this.x - 1;
    } else if (keyCode == RIGHT_ARROW) {
      this.x = this.x + 1;
    } else if (keyCode == UP_ARROW) {
      this.y = this.y - 1;
    } else if (keyCode == DOWN_ARROW) {
      this.y = this.y + 1;
    }
  }
}

```

### Sketch Code: 

```

//initializing all variables used in code
let gameGrid;
let islandImg;
let boat;
let font;
let isSoundPlaying = false;
let winSound;
let lostSound;
let startScreen = 0;
let x1, y1;
let timer = 35;
let xL;
let yL;

// preload is used to already load the stuff like sound , images or videos
function preload() {
  islandImg = loadImage("assets/image_processing20211012-26001-a82vax.png");
  font = loadFont("assets/SnesItalic-1G9Be.ttf");
  winSound = loadSound("assets/win-game.mp3");
  lostSound = loadSound("assets/lose-game.mp3");
}

//setting up the canvas and assignigng values to variables
function setup() {
  createCanvas(426, 426);
  noStroke();
  boat = new Boat(-15, -45);
  gameGrid = new Grid(25, 17, 17); //create a new Grid object
  textSize(50);
  textFont(font);
  xL = 421;
  yL = 10;
}

// draw is a loop function that calls itself repeatedly while the program runs
function draw() {
  background(127, 205, 255);

  // red line timer: the width of line divided by the time limit
  let b1 = 426 / 35;

  //start screen in order to start the game
  if (startScreen == 0) {
    rect(255, 0, 0);
    fill(0);
    text("double click to start", 70, 220);
  } else if (startScreen == 1) {
    // game mechanics
    gameGrid.draw(); //draw the grid
    boat.drawBoat(); // draw the boat
    image(islandImg, 255, 385, 40, 40); // endpoint image

    // the appearance of the redline timer with the countdown timer
    strokeWeight(1);
    stroke(255, 0, 0);
    fill(255, 0, 0);
    rect(0, 0, xL, yL);
    noStroke();
    // print("`timer:",timer);
    if (frameCount % 60 == 0) {
      timer--;
      xL -= b1;
    }
  }

  currGrid = gameGrid.getCurrValue(boat.x, boat.y);

  //if time is equal to zero and the player has reached the island, they win.
  if (boat.x + 10 >= 255 && boat.y + 70 >= 400) {
    background(127, 205, 255);
    textSize(50);
    fill(0);
    text("You Win ! ", 150, 220);
    if (isSoundPlaying == false) {
      winSound.play();
      isSoundPlaying = true;
    }

    //if time is equal to zero this means that the player has not reached  the island, so the game over.
  } else if (timer <= 0) {
    background(164, 116, 73);
    textSize(50);
    fill(255);
    text("Game Over You Lose ", 80, 220);
    if (isSoundPlaying == false) {
      lostSound.play();
      isSoundPlaying = true;
    }
  }

  //An if statement: if you press r key and time is 0 which means game has ended so restart game
  if (keyIsPressed) {
    if (keyCode == 32 && timer <= 0) {
      xL = 0;
      timer = 35;
      window.location.reload();
    }

    // this allows the boat to move in the blue pathways only
    if (keyCode == LEFT_ARROW) {
      if (gameGrid.getCurrValue(boat.x - 1, boat.y) == 0) {
        boat.moveBoat();
      }
    } else if (keyCode == RIGHT_ARROW) {
      if (gameGrid.getCurrValue(boat.x + 23, boat.y) == 0) {
        boat.moveBoat();
      }
    } else if (keyCode == UP_ARROW) {
      if (gameGrid.getCurrValue(boat.x, boat.y - 1) == 0) {
        boat.moveBoat();
      }
    } else if (keyCode == DOWN_ARROW) {
      if (gameGrid.getCurrValue(boat.x, boat.y + 7) == 0) {
        boat.moveBoat();
      }
    }

    //checking if user presses r or R key then restart the game. Thus, loop allows the game to play again.
    if (key == "r" || key == "R") {
      noLoop();
      noStroke();
      boat = new Boat(-15, -45);
      gameGrid = new Grid(25, 17, 17);
      isSoundPlaying = false;
      timer = 35;
      xL = 421;
      loop();
    }
  }
}

// if the screen is double clicked at the screen value 0, it moves to the other screen.
function doubleClicked() {
  if (startScreen == 0) {
    startScreen++;
  }
}

```





## References

* [p5.js Reference](https://p5js.org/reference/)
* [Grid Example for Games](https://editor.p5js.org/itp42/sketches/dBeLZC8mm)
* [Timer](https://editor.p5js.org/marynotari/sketches/S1T2ZTMp-)
* [Center Canvas](https://editor.p5js.org/itp42/sketches/4yYMl2c3P)
* [Start Screen](https://editor.p5js.org/itp42/sketches/hCa_xCoY5)

