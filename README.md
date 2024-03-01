# Welcome to Viden Vale!

## What is this?

I wanted something more interesting, and more real, than the typical To Do app for
learning new technologies. Build a fun adventure game using the technologies of your 
choice! This repository will provide all of the requirements, assets, and data 
needed to build an adventure game.

## Requirements

### Character Creation
* A user can create an account with their email address
* A user can create a character selecting the following
  * Name
  * Class (Barbarian, Rogue)
  * Portrait, upload their own or select from provided options
* A user may have as many characters as they like

### Game Loop
* User can select a character to begin an adventure
* An adventure is a sequence of encounters
* Each encounter contains a monster for the character to fight
  * Monster is determined randomly from the list of monsters
* An encounter is made of many turns
  * On each turn the character can take one of the following actions:
    * Attack
    * Heal
    * Flee
  * On each turn the monster can take one of the following actions:
    * Attack
* A turn is over when both the character and the monster have taken an action or
  when the encounter ends
  * After each action the results should be displayed in the game log
* The encounter ends when one of the following occurs
  * The monster is defeated
  * The character is defeated
  * The character successfully runs away
* After the encounter the following occurs
  * If the character defeated a monster
    * The character receives temporary experience
    * The character receives temporary gold
    * The character is given the choice to continue or return to town
  * If the character fled
    * The character loses temporary experience
  * If the character was defeated by a monster
    * The character is marked as dead and can no longer be played
    * The character is still displayed for the user with its stats
    * The user is returned to the character selection/creation screen 

### Encounter Actions
#### Attacking
When a player or a monster attacks they roll a d20 (random number from 1-20) and add 
their attack bonus to the roll. If the resulting number is higher than the armor value 
for the target then it is considered a hit.

If the attack hits then damage is calculated by picking a random number between the 
minimum and maximum values for the character or monster and then adding the damage 
bonus. Damage is subtracted from the current health on the character or monster. If 
the current health is reduced to less than one than the target is defeated.

If the attack misses then control passes from the attacker to the other entity in the 
encounter.

#### Heal
When a player chooses to heal then the heal value is determined by selecting a random
number between the minimum and maximum values for the characters heal values. That value
is added to the characters current health, not to exceed their maximum health value.

This ends the characters turn.

#### Flee
When a character chooses to flee the monster makes an attack on the character. If the
attack succeeds the character is blocked and it becomes the monsters turn. If the attack
fails then the encounter ends and the character loses the same amount of experience that
they would have received from defeating the monster.

### Returning to town
Upon returning to town the character receives the rewards in gold and has the opportunity
to level up.

#### Leveling Up
If the user does not have enough experience to get to the next level when returning to town,
all temporary experience is lost! If they do have enough experience to increase their 
level than the characters level increases and their temporary experience is set to 0.

Characters start at level 0. The cost to progress to the next level is the target level * 100.
For example, if a character is 4th level, then they need 500 experience to progress to 5th level.

The following happens upon gaining a level:
* The characters maximum health is increased by a random amount between the maximum and minimum
values for health progression.
* The characters armor goes up by 1 * the class armor modifier
* The characters damage bonus goes up by 1 * the class damage modifier
* The characters current health is set to the maximum health
* The characters temporary experience is set to 0

## The Interface

### Welcome screen
A screen that allows users to sign up or sign in

### Town Screen
This screen shows all of the characters and allows the user to create a new character

Characters are displayed as cards that include
* Name
* Level
* Health
* Gold
* Portrait
* Status (playable or deceased)
* Button to begin an adventure (unless they are deceased)
* Armor

### Adventure Screen
This is the main screen for the game. It displays the following:

A panel for the character showing:
* Name
* Portrait
* Current and max health
* Temporary XP accrued
* XP needed for next level
* Temporary gold
* Armor

A panel for the monster showing:
* Name
* Portrait
* Current and max health
* Armor

A panel showing the actions and outcomes during the encounter. For example:

```
Ogg attacks the skeleton (18) and hits doing 12 damage
Ogg defeats the skeleton!
Ogg attacks the skeleton (6) and misses
The skeleton attacks Ogg (21) and hits doing 7 damage
Ogg has been slain!
The skeleton attacks Ogg (4) and misses
Ogg attempts to flee but is blocked!
Ogg attempts to flee and escapes, losing 28 experience
Ogg takes a moment to heal and regains 7 health
```

A panel showing the actions that can be taken:
* Between encounters: Continue, Return to Town
* During encounters: Attack, Flee, Heal

## Winning
There is no end to the game in the traditional sense, rather the goal is to accumulate the
most gold. The character (alive or dead) with the most gold should be highlighted in some 
way as the current "winner".
