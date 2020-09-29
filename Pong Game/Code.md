# Pong game code

//create the ball, playerPaddle and computerPaddle as sprite objects

~~~objects
var ball = createSprite(200,200,10,10);
var playerPaddle = createSprite(380,200,10,70);
var computerPaddle = createSprite(10,200,10,70);
~~~

//variable to store different state of game

~~~variables
var gameState = "serve";
var computerScore = 0;
var playerScore = 0;
~~~

## function draw 

function draw() {

  //clear the screen

~~~background
 background("white");
~~~

  //place info text in the center

~~~center line
if (gameState === "serve") {
    text("Press Space to Serve",150,180);
  }
~~~

~~~Score board
  text(computerScore,180,20);
  text(playerScore,220,20);
~~~

~~~playerPaddle controls
  if(keyDown("up")){
    playerPaddle.y = playerPaddle.y - 5; 
    }

  if(keyDown("down")){
    playerPaddle.y = playerPaddle.y + 5; 
    }
~~~

~~~computerPaddle controls
if(keyDown("w")){
    computerPaddle.y = computerPaddle.y - 5; 
    }



  if(keyDown("s")){
    computerPaddle.y = computerPaddle.y + 5; 
    }
~~~

  //make the player paddle move with the mouse's y position

  //playerPaddle.y = World.mouseY;

~~~optional
  //AI for the computer paddle
  //make it move with the ball's y position

  //computerPaddle.y = ball.y;
~~~

  //draw line at the centre

~~~draw center line
for (var i = 0; i < 400; i=i+20) {
    line(200,i,200,i+10);
  }
~~~


  //create edge boundaries

  //make the ball bounce with the top and the bottom edges

~~~createEdgeSprites
createEdgeSprites();

  ball.bounceOff(topEdge);
  ball.bounceOff(bottomEdge);
  ball.bounceOff(playerPaddle);
  ball.bounceOff(computerPaddle);

  playerPaddle.collide(topEdge);
  playerPaddle.collide(bottomEdge);

  computerPaddle.collide(topEdge);
  computerPaddle.collide(bottomEdge);


~~~

  //serve the ball when space is pressed

~~~start game when space pressed
if (keyDown("space") && gameState === "serve") {
    serve();
    gameState = "play";
  }
~~~

  //reset the ball to the centre if it crosses the screen

~~~computerScore
if(ball.x  >  400){
    computerScore = computerScore +1 ;
    }
    
~~~

    if(ball.x < 0){
      playerScore = playerScore + 1;
      }
      reset();
      gameState = "serve";
  }

~~~gameOver text
if(playerScore === 5 || computerScore === 5){
    gameState = "over";
    textSize(30);
    text("Game Over",110,150);
    text("Press R to Restart",110,180);
    }
    
~~~

    if(keyDown("r") && gameState === "over"){
      gameState = "serve"; 
      computerScore = 0 ;
      playerScore = 0 ;
    }
    
    drawSprites();
    }
~~~function serve
function serve() {
  ball.velocityX = 3;
  ball.velocityY = 4;
}
~~~

  ~~~function reset
function reset() {
  ball.x = 200;
  ball.y = 200;
  ball.velocityX = 0;
  ball.velocityY = 0;
}
  ~~~