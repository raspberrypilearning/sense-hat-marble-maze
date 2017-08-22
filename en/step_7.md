## Move the marble

The marble's movement will be controlled by moving the Sense HAT. The Sense HAT library can detect pitch, roll and yaw. You can see a picture illustrating this below.

![Sense HAT orientation](images/orientation.png)

+ Locate the code that sets the position of the marble and draws the maze on the display.

![Draw marble code](images/draw-marble-code.png)

+ Above this code, create a Boolean variable called `game_over` with a starting value of `False`.

+ Create a **while loop** which runs while the `game_over` variable is False. Put the two highlighted lines of code inside the loop.

[[[generic-python-while-boolean]]]

This will create a game loop allowing us to update the position of the marble when the Sense HAT is moved.


- You don't need the yaw orientation of the Sense HAT for this project, just the pitch and the roll. Add these two lines into the `while` loop, so that you get constant and up-to-date readings of the orientation, and it looks like this:

	```python
	while not game_over:
		pitch = sense.get_orientation()['pitch']
		roll = sense.get_orientation()['roll']
		maze[y][x] = w
		sense.set_pixels(sum(maze,[]))
	```

- Now it is time to move the marble. You're going to write a separate function to do this. **Above** the `while` loop, you can define the new function.

	```python
	def move_marble(pitch, roll, x, y):
	```

- The function has `pitch`, `roll`, `x`, and `y` as parameters. You're going to want to keep the `x` and `y` positions of the marble unchanged (you'll see why later), so the first thing to do is store these values as other variables.

	```python
	def move_marble(pitch, roll, x, y):
		new_x = x
		new_y = y
	```

- Now it's time to change the position of the marble, depending on the way that the Sense HAT is tilted. When the Sense HAT is lying flat, pitch and roll should be approximately 0. They will then either increase as the Sense HAT is tilted (0,1,2,3,4...), or they'll decrease (0,359,359,357,356...). You'll want to ignore very tiny movements (less than a degree) as the Sense HAT will very rarely be lying completely flat.

- If the pitch is between 1 and 179, then `new_x` needs to decrease. If it's between 359 and 181, then `new_x`should increase.

	```python
	def move_marble(pitch,roll,x,y):
		new_x = x
		new_y = y
		if 1 < pitch < 179:
			new_x -= 1
		elif 359 > pitch > 181:
			new_x += 1
		return new_x, new_y
	```

- To test this code out, you'll need to call the function within the `while` loop.

	```python
	while not game_over:
		pitch = sense.get_orientation()['pitch']
		roll = sense.get_orientation()['roll']
		x,y = move_marble(pitch,roll,x,y)
		maze[y][x] = w
		sense.set_pixels(sum(maze,[]))
	```

- Your entire script should now look like this:

	```python
	from sense_hat import SenseHat

	sense = SenseHat()
	sense.clear()

	r = (255,0,0)
	b = (0,0,0)
	w = (255,255,255)

	x = 1
	y = 1

	maze = [[r,r,r,r,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,r,r,b,r,b,b,r],
			[r,b,r,b,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,b,r,r,r,r,b,r],
			[r,b,b,r,b,b,b,r],
			[r,r,r,r,r,r,r,r]]

	def move_marble(pitch,roll,x,y):
		new_x = x
		new_y = y
		if 1 < pitch < 179:
			new_x -= 1
		elif 359 > pitch > 181:
			new_x += 1
		return new_x,new_y

	game_over = False

	while not game_over:
		pitch = sense.get_orientation()['pitch']
		roll = sense.get_orientation()['roll']
		x,y = move_marble(pitch,roll,x,y)
		maze[y][x] = w
		sense.set_pixels(sum(maze,[]))
	```

- Save and run your code. It **will** break, but don't worry: we will fix it in the next step.

<iframe src="https://trinket.io/embed/python/7197ab0e48" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
