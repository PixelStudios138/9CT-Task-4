# 9CT Assessment Task 4

## Project Development - Part B

This markdown file will go over the development stages of my final project, from researching to the finished product.

## Identifying And Defining

### Identifying A Need

The first step was to identify a need for my game. I decided to use the Unity engine early on, but what game to make took a bit longer to come up with. I decided to come up with a game idea first and then find the need following that. My ideas were:

- An adventure game about collecting orbs
- A game about an AI vs human war
- A survival game

I decided to go for a survival game. 

**Need:** To simulate a situation in which a person needs to survive for 7 days with no food, water, or shelter at the start. All they will have is an axe. 

**Problem Statement:** Young people need to learn basic survival skills in case they are in a situation where they are in an unfamiliar area, with no food, water, or shelter. This game will teach them techniques such as purifying water, finding food, and building shelter.

**Skill Develepment:** I will utilise [this tutorial by Sebastian Lague](https://www.youtube.com/playlist?list=PLFt_AvWsXl0eBW2EiBtl_sxmDtSgZBxB3) on procedural generation (which I have used in the past, such as in my [Ludum Dare 58 project Isle Of The Orbs](https://dreamsphere-games.itch.io/isle-of-the-orbs)) and parts of [this tutorial by Mike's Code](https://www.youtube.com/playlist?list=PLtLToKUhgzwnk4U2eQYridNnObc2gqWo-) on survival game development, but probably only the parts on the building system.

### Requirements Outline

**Inputs:** User inputs will include: WASD or arrow keys for movement; spacebar for jumping; left click for attacking an enemy, breaking trees/rocks, and placing an item; E for collecting items, and I for opening the inventory

**Processing:** The game will keep track of all enemies killed, the score, and the player's health and hunger; any items that have been collected/placed; trees/rocks that have been destroyed

**Outputs:** The game will display the player's score, any objects that are collected (when they have been collected), the inventory (when opened), the player's health & hunger; and it will play a music track in the background.

**Transmission**: The game will include a multiplayer option, where it will transmit other player's position and currently equipped item

**Storage**: The game may save the player's progress, such as position, any items built, and potentially user settings

### Functional Requirements:

**User Interaction:** The user can use keyboard commands and mouse clicks to perform different actions. The WASD keys can be used for movement, the spacebar can be used to jump, the I key can be used to open the player's inventory, and E can be used to collect items. The mouse can be used for moving the camera, left click can be used for attacking an enemy, breaking trees/rocks, and placing an item when in game, or interacting with the menu when at the start screen.

**Core Gameplay Mechanics:** The movement mechanics will be fairly basic, with only walking, running, and jumping features. The game will include mechanics for building structures, destroying trees, and killing animals, which will be the core mechanics of the game. There may be a cooking system. There will be a hunger system in place which will slowly decrease, only replenishable by eating. Once the hunger bar is at 0, the health bar will start to slowly decrease. The health bar can also decrease if attacked by an enemy.

**Scoring System:** The game will award points for performing certain tasks and collecting certain achievements. 100 points will be awarded for crafting for the first time, 25 points will be awarded for every enemy killed, and 10 points for every 10 minutes spent in the game.

### Non-Functional Requirements

**Performance Requirements:** The game should load in no more than 5 seconds, and respond to user inputs instantly without noticeable lag.

**Usability Requirements:** The game will have an in game user interface showing the player's health, hunger, score, and inventory, and have space to show achievements when they are met. The controls should be easy and simple to understand. The game will have a cutscene prior to the actual gameplay explaining core mechanics.

**Compatibility Requirements:** The game must run on Windows and Mac laptops using keyboard and mouse, and may run on consoles with button and joystick controls.

### Consideration of Social & Ethical issues

Equity: the quality of being fair and just, especially in a way that takes account of and seeks to address existing inequalities.  
Accessibility: the quality of being able to be reached or entered

**Accessibility:** The game will be accessible to the majority of people. The game will utilise subtitles for deaf people when audio tracks are present, and the controls will be easy to understand.

**Privacy And Data Protection:** The game will not collect any data on players. This prevents any data being stolen.

**Fairness & Representation:** This game will avoid stereotypes & bias. The game is first person, and the player's will be random solid colours, e.g red, green, blue, etc

**Mental & Emotional Well-being:** The game won't be harmful to people's mental or emotional wellbeing. It will avoid distressing content, and the only violence will be attacking mobs, which will be very rare and light-hearted. The blood and all graphics will be cartoony with no distressing attack sounds, but there will be an option to turn off blood for those who are extremely disturbed by it.

**Cultural Sensitivities:** The game will not feature anything that will be culturally insensitive, and will not be able to be misinterpreted.

## Researching & Planning

### PMI Table

| Existing Idea          | Plus                                 | Minus                                         | Implications                                     |
|------------------------|--------------------------------------|-----------------------------------------------|--------------------------------------------------|
|[Muck](https://store.steampowered.com/app/1625450/Muck/)|The enemies are good, crafting system is well done, swimming is good|There is no pause button, and is rather difficult|I will use a similar swimming and crafting system, while avoiding making it too difficult and adding a pause button|
|[Minecraft](https://www.minecraft.net/)|Not too difficult|The game is made up of nothing but cubes|I will make the game with a similar difficulty, but have different shapes, not just cubes|
|[Rust](https://store.steampowered.com/app/252490/Rust/)|The gameplay and story is similar|Too graphic and violent|I will make the game with a similar storlyine, but with less graphic and more cartoony violence/graphics|

### Flowcharts and Pseudocode

To see how the game will be programmed, I have made flowcharts for all of the functional requirements. Underneath the flowcharts will be the respective pseudocode.

![Flowchart describing the process of the code used in the assessment task](/Images/UIChart.png "Flowchart of User Interaction")  

![Flowchart describing the process of the code used in the assessment task](/Images/DJScoreChart.png "Flowchart of Score & Health Systems")  

Below is the pseudocode for the User Interaction flowcharts:

```
BEGIN User Interaction
IF userInput == "W"
  movePlayerForward()
ELSEIF userInput == "S"
  movePlayerBackward()
ELSEIF userInput == "A"
  movePlayerLeft()
ELSEIF userInput == "D"
  movePlayerRight()
ELSEIF userInput == "Spacebar"
  IF isOnGround
    makePlayerJump()
  ENDIF
ELSEIF userInput == "I"
  IF inventoryIsOpen
    closePlayerInventory()
  ELSE
    openPlayerInventory()
  ENDIF
ELSEIF userInput == "E"
  collectItem()
ELSEIF userInput == "Left Click"
  IF isAttackingEnemy
    attackEnemy()
  ELSEIF isBreakingTree
    breakTree()
  ELSEIF isInGame
    placeItem()
  ELSE
    interactWithMenu()
  ENDIF
ENDIF
END User Interaction
```

And here is the pseudocode for the Systems flowchart

```
BEGIN Systems

DECLARE score : INT
DECLARE health : INT
DECLARE hunger : INT
score = 0
health = 100
hunger = 10
IF hasKilledEnemy
  score += 10
ELSEIF hasEaten
  hunger += 1
ELSEIF timeSinceLastEaten == 60
  hunger -= 1
  IF hunger == 0
    IF timeSinceNoHunger == 20:
      health -= 3
    ENDIF
  ENDIF
ELSEIF timeSinceNoHunger == 20:
  health -= 3
ENDIF

END Systems
```

### Storyboards

Here are the storyboards for the whole game, one for the in-game scene, and one for the title screen

![Storyboard describing the main process of the code used in the whole game](/Images/WholeGameStoryboard.png "Storyboard of Whole Game")  
![Storyboard describing the main process of the code used in the game scene](/Images/InGameStoryboard.png "Storyboard of In-Game Scene")  
![Storyboard describing the main process of the code used in the title screen](/Images/TitleScreenStoryboard.png "Storyboard of Title Screen")  

### Gantt Chart

Below is the gantt chart of the entirety of Part B of this assessment, along with the creation of the game starting next week:

![Gantt chart explaining the flow of creating the assessment and game](/Images/GanttChart.png "Gantt Chart Of Assessment Task Creation")  

## Conclusion

This markdown file has described everything required in this task, from functional and non functional requirements to pseudocode to the actual code and everything inbetween. I have poured my heart and soul into this (as always), and I hope it pays off. Thank you for your time.

