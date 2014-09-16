---
layout: post
title: "Tutorial: Build a Game with Phaser"
author: "Thomas Palef"
categories:
- games
- tutorials
- phaser
---

<div class="intro">
This is a guest post written by <a href="http://www.lessmilk.com/">Thomas Palef</a>, the author of <a href="https://www.discoverphaser.com/">Discover Phaser</a> and the <a href="http://www.lessmilk.com/12games">12 Games in 12 Weeks</a> challenge.
</div>

### Introduction

In this tutorial I will show you how to use Phaser to build a really simple retro breakout clone. Phaser is a simple yet powerful JavaScript framework for making HTML5 games.

![Game screenshot](/images/posts/phaser/game.png)

You can play the finished game we are going to make [here](/files/phaser-tutorial/).

### Set Up

You should download [this empty template](/files/phaser-template.zip) that I made for this tutorial. In it you will find:

* phaser.min.js, the Phaser framework v2.0.5
* index.html, where the game will be displayed
* main.js, a file where we will write all our code
* assets/, a directory with 3 images (ball.png, paddle.png and brick.png)

You should also download the [code editor Brackets](http://brackets.io/), that will make it easier for starting a web server during development.

### Empty Game

Let's start by creating an empty Phaser project.  Add this code inside the main.js file:

{% highlight javascript %}
// Define our main state
var main = {
  preload: function() {
    // This function will be executed at the beginning     
        // That's where we load the game's assets  
  },

  create: function() { 
    // This function is called after the preload function     
        // Here we set up the game, display sprites, etc. 
  },

  update: function() {
    // This function is called 60 times per second    
        // It contains the game's logic     
  },
};

// Initialize Phaser, and start our 'main' state 
var game = new Phaser.Game(400, 300, Phaser.AUTO, 'gameDiv');
game.state.add('main', main);
game.state.start('main');
{% endhighlight %}

This will create a 400x300 black rectangle on the screen. All we have left to do is to fill the `preload`, `create`, and `update` functions to build our breakout clone.

#### Add the Paddle

Let's focus on creating the paddle first. We load it in the `preload` function, initialize it in the `create` function, and make it move in the `update` function:

{% highlight javascript %}
preload: function() {
  // Load the paddle image
  game.load.image('paddle', 'assets/paddle.png');
},

create: function() { 
  // Initialize the physics system of the game
  game.physics.startSystem(Phaser.Physics.ARCADE);

  // Create a variable to handle the arrow keys
  this.cursor = game.input.keyboard.createCursorKeys();

  // Create the paddle at the bottom of the screen
  this.paddle = game.add.sprite(200, 400, 'paddle');

  // Enable the physics system for the paddle
  game.physics.arcade.enable(this.paddle);
},

update: function() {
  // If the right arrow is pressed, move the paddle to the right
  if (this.cursor.right.isDown) 
    this.paddle.body.velocity.x = 350;

  // If the left arrow if pressed, move left
  else if (this.cursor.left.isDown) 
    this.paddle.body.velocity.x = -350;

  // If no arrow is pressed, stop moving
  else 
    this.paddle.body.velocity.x = 0;  
}
{% endhighlight %}

### Test the Game

Now it's time to test our game. Open the whole directory in the Brackets editor, select the index.html file, and click on the small bolt icon in the top right corner. It will launch a live preview of the game, where you should have a paddle that you can move with the arrow keys.

If you don't want to use Brackets, then you'll have to use a local web server to test the game.

### Add the Bricks

Now let's add a dozen bricks to the game.

Start by adding this to the `preload` function:

{% highlight javascript %}
// Load the brick sprite
game.load.image('brick', 'assets/brick.png');
{% endhighlight %}

Then add this to the `create` function:

{% highlight javascript %}
// Create a group that will contain all the bricks
this.bricks = game.add.group();
this.bricks.enableBody = true;

// Create the 16 bricks
for (var i = 0; i < 5; i++)
  for (var j = 0; j < 5; j++)
    game.add.sprite(55+i*60, 55+j*35, 'brick', 0, this.bricks);

// Make sure that the bricks won't move
this.bricks.setAll('body.immovable', true);
{% endhighlight %}


### Add the Ball

Now that we have a paddle and some bricks, it's time to add the ball.

Add this in the `preload` function:

{% highlight javascript %}
// Load the ball sprite
game.load.image('ball', 'assets/ball.png');
{% endhighlight %}

And add this in the `create` function to initialize the ball:

{% highlight javascript %}
// Create the ball with physics
this.ball = game.add.sprite(200, 300, 'ball');
game.physics.arcade.enable(this.ball);

// Add velocity to the ball
this.ball.body.velocity.x = 200; 
this.ball.body.velocity.y = 200;

// Make the ball bouncy 
this.ball.body.collideWorldBounds = true;
this.ball.body.bounce.x = 1; 
this.ball.body.bounce.y = 1;
{% endhighlight %}

### Handle Collisions

The only thing left to do is handle collisions. And it turns out this is super simple with Phaser -- just add these 2 lines of code to the `update` function:

{% highlight javascript %}
// Make the paddle and the ball collide
game.physics.arcade.collide(this.paddle, this.ball);

// Call the 'hit' function when the ball hit a brick
game.physics.arcade.collide(this.ball, this.bricks, this.hit, null, this);
{% endhighlight %}

Next, create the new `hit` function, just below the `update` function:

{% highlight javascript %}
hit: function(ball, brick) {
  // When the ball hits a brick, kill the brick
  brick.kill();
}
{% endhighlight %}

And we are done! you can now play a really simple breakout clone made in less than 50 lines of JavaScript.


### Conclusion

The game is working, but it's a little bit boring. With Phaser it's really simple to add sounds effects, animations, transitions, and so on to make a game better.

If you want to learn more about Phaser, I can recommend you to check out the first and only Phaser ebook currently available: [Discover Phaser](https://www.discoverphaser.com/).

![Phaser cover](/images/posts/phaser/phaser-cover.jpg)

