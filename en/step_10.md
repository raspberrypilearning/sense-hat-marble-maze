## Make the walls solid

You have probably noticed that when the marble moves around the maze, it deletes the walls as it goes. To prevent this from happening, you're going to need some basic collision detection. To do this you can write a new function.

+ Above your `while` loop, add this line of code to begin a new function:

```python
def check_wall(x,y,new_x,new_y):
```

The function will check whether there is a wall at the `new_x` and `new_y` coordinates. If there is no wall, then it will return the `new_x` and `new_y`, otherwise it will return to old `x` and `y`. This is why we needed to copy the `x` and `y` variables earlier.

+ Add code inside the `check_wall` function to check for walls in all directions. Here is the pseudo code to help you.

```
**IF** the location at `new_y`, `new_x` is not red (i.e. no wall)
    return `new_x`, `new_y`
**ELIF** the location at `new_y` and `x` is not red (i.e. we can move up/down)
    return `x`, `new_y`
**ELIF** the location at `y`, `new_x`is not red (i.e. we can move left/right)
    return `new_x`, `y`
**ELSE**
    return `x`, `y` (i.e. there is nowhere to move to so stay where you are)
```

+ Call this function within the `move_marble` function.

 to decide what the `x` and `y` coordinates of the marble will be. The last line needs to be changed to return `x` and `y`, and the line before needs to be added, to call the `check_wall` function.

	```python
	def move_marble(pitch,roll,x,y):
		new_x = x
		new_y = y
		if 1 < pitch < 179 and x != 0:
			new_x -= 1
		elif 359 > pitch > 179 and x != 7 :
			new_x += 1
		if 1 < roll < 179 and y != 7:
			new_y += 1
		elif 359 > roll > 179 and y != 0 :
			new_y -= 1
		x,y = check_wall(x,y,new_x,new_y)
		return x,y
	```
