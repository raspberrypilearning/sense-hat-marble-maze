## Goal!

Lastly, you'll want a way for the player to win. You can pick any blank LED in the maze and set it as the target for the player to reach.

+ Create a new variable to store your chosen colour for the winning marker. Put this code with the other colour variables you already created.

+ Add the winning marker to the `maze` by changing one of the *b*'s in the grid to the letter representing your winning marker colour.

+ Inside your `while` loop, once you have calculated the new `x`, `y` coordinates with the `move_marble` function, write an `if` statement to check whether the colour at this position is the winning colour.

![Check for win](images/check-for-win.png)

+ If the colour is the winning colour, display a message saying "Win!" and set the `game_over` variable to `True` to end the game.

[[[rpi-sensehat-show-message]]]

--- hints ---
--- hint ---
Here is some pseudo code to help you:

**IF** maze (x, y) **EQUALS** the winning colour variable
**DISPLAY** "Win!" on the screen
**SET** `game_over` variable to `True`
--- /hint ---

--- hint ---
Here is how your code should look:
![Code to check for win](images/win-code-finished.png)
--- /hint ---

--- /hints ---

- Save and run your code. Move the Sense HAT around and check that when you reach the winning marker your "Win!" message is displayed.
