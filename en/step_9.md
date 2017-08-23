## Fix the marble

There are two problems:
  - The marble illuminates a whole line of LEDs
  - The code breaks with a `IndexError: list assignment index out of range` error.

### Problem one: Lots of LEDs are illuminated

The first problem occurs because, once the marble moves onto the next LED, you have not changed the colour of the first LED back to black.

+ Use the sleep function to add a pause of 0.05 seconds into your while loop, on the line below the code to show the pixels on the Sense HAT display

[[[generic-python-sleep]]]

+ Then on the line below that, add some code to tell the LED at the current `x`, `y` position to reset itself to blank.

--- hints ---
--- hint ---
Here is the line of code you used to tell the LED at the current position to turn white:

```python
maze[y][x] = w
```

Can you alter this code to tell the LED to turn blank?
--- /hint ---

--- hint ---
Your code should look like this:

```python
while not game_over:
    pitch = sense.get_orientation()['pitch']
    roll = sense.get_orientation()['roll']
    x,y = move_marble(pitch,roll,x,y)
    maze[y][x] = w
    sense.set_pixels(sum(maze,[]))
    sleep(0.05)
    maze[y][x] = b
```
--- /hint ---
--- /hints ---

+ Save and run your code. Move the Sense HAT to check that the marble looks as if it is moving.

### Problem two: IndexError

This occurs because in the `move_marble` function, we simply add one or take away one from the `new_x` variable depending on which way the Sense HAT is tilted. Eventually this means that the `new_x` value will increase above `7` or decrease below `0`.

As this would be outside the boundaries of the LED matrix, the SenseHat library returns an error. This can be fixed by only changing `x` and `y` when they are **not** equal to 0 or 7.

+ Alter your `move_marble` function so that it looks like this:

	```python
	def move_marble(pitch,roll,x,y):
		new_x = x
		new_y = y
		if 1 < pitch < 179 and x != 0:
			new_x -= 1
		elif 359 > pitch > 179 and x != 7 :
			new_x += 1
		return new_x,new_y
	```

- Save and run your code to ensure the marble is moving horizontally across the screen.

- Now that you have the marble moving horizontally, you need to make it move vertically as well. Update the `move_marble` function so that it uses the `roll` to move the marble in the y direction.

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
		return new_x,new_y
	```

<iframe src="https://trinket.io/embed/python/5c2e24ced3" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
