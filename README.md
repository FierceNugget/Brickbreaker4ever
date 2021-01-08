<!-- PROJECT LOGO -->
<p align="center">
  <h1 align="center">Brickbreaker 4Ever</h1>
  <h3 align="center">Introduction to Games Programming</h3>
  
  <p align="center">
    <h3">Harry Wilson</h3>
    ·
    <h3">S2041240</h3>
    ·
    <h3">Computer Games (Design)</h3>
  </p>
</p>




_I confirm that the code contained in this file (other than that provided or authorised) is all my own work and has not been submitted elsewhere in fulfilment of this or any other award._ 

_-Harry Wilson_


<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
  <ol>
      <li><a href="#about-the-project">About The Project</a></i>
      <li><a href="#description-of-the-code">Description of the Code</a></i>
      <ul>
        <li><a href="#main-menu">Main Menu</a></li>
        <li><a href="#game-manager">Game Manager</a></li>
        <li><a href="#ball-movement">Ball Movement</a></li>
        <li><a href="#bat-movement">Bat Movement</a></li>
      </ul>
    </li>
    <li><a href="#challenging-code">Challenging Code</a></li>
  </ol>
</details>


## About the Project

During my coursework for Introduction to Games Programming, we have been tasked to create and develop a 2D game similar to that of Breakout. This game would have to be hand-coded and include things such as movement, textures and collision detection. It is to test our ability and knowledge of coding and help us refine our skills. The game is to be made using Unity in C# and the deadline for this is the 11/01/2021.

## Description of the Code

### Main Menu

The main menu script handles anything that is shown on the main menu. In my game, the main menu is saved as a separate scene so I had to write code that would allow me to navigate between these scenes using buttons. This script also includes a function to save recent high scores and display them on the front page.

### Game Manager

The game manager deals with most of the mechanics for the game and is used heavily to link everything together. It contains functions for completing a level, getting a game over screen and changing stage. It also deals with the infinitely increasing score and speed multiplier that gets put on at the start of each new stage. I did this by constantly counting how many bricks are left in the stage and if their number is 0, it would then run the level complete function that would increase the multiplier.

```sh
if (brickCount <= 0)
  {
    LevelComplete();
  }
```

It also uses PlayerPrefs to hold onto a value during scene changes, this allows us to keep a high score that you can come back to beat and will be displayed at the end of each level. A special message is also displayed when the player beats their previous high score.
  
```sh
int highScore = PlayerPrefs.GetInt("HIGHSCORE");

if (score > highScore)
  {
    highScore = score;
    PlayerPrefs.SetInt("HIGHSCORE", highScore);
    highScoreText.text = ("NEW HIGHSCORE!");
  } else
  {
    highScoreText.text = ("HIGHSCORE: " + highScore);
  }
```  
### Ball Movement

### Bat Movement

## Challenging Code

One piece of code that I found challenging and difficult to implement is the removal of bricks after a game over screen has occurred on level 2 or later. This was difficult because of how I stored my levels. I wanted to store the levels as prefabs in an array so that I could call back to them and store multiple levels easily. I then ran into a problem, after completing the first level, it would respawn the prefab as a clone outside the determined game object. This means that when my game over script ran and there were still blocks on the screen, they weren't being removed because they were no longer stored inside the game object.

Luckily, I was using prefabs that all shared one common property, they all had the "Brick" tag. This meant that I could do a search for any game object with the "Brick" tag and destroy it. The way I did this was by using FindGameObjectsWithTag to store all bricks in its own array, I then used a simple for loop that would count the number of bricks in the array and delete them all until the value is 0. I then placed this bit of code inside its own function so that I could call it in my game over the script.

  ```sh
    void DestroyBricks()
    {
        GameObject[] bricks = GameObject.FindGameObjectsWithTag("Brick");
        
        for (int i = 0; i < bricks.Length; i++)
        {
            Destroy(bricks[i]);
        }
    }
  ```
