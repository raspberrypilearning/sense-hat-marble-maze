## Handling collision with the walls.

- You have probably noticed that when the marble moves around the maze, it deletes the walls as it goes. To prevent this from happening, you're going to need some basic collision detection. To do this you can write a new function.

	```python
	def check_wall(x,y,new_x,new_y):
	```

- This function will check whether there is a wall at the `new_x` and `new_y` coordinates. If there is no wall, then it will return the `new_x` and `new_y`, otherwise it will return to old `x` and `y`. This is why we needed to copy the `x` and `y` variables earlier.

	```python
	def check_wall(x,y,new_x,new_y):
		if maze[new_y][new_x] != r:
			return new_x, new_y
		elif maze[new_y][x] != r:
			return x, new_y
		elif maze[y][new_x] != r:
			return new_x, y
		return x,y
	```

- This function can now be called within the `move_marble` function, to decide what the `x` and `y` coordinates of the marble will be. The last line needs to be changed to return `x` and `y`, and the line before needs to be added, to call the `check_wall` function.

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

- The full code should now look like this:

	```python
	from sense_hat import SenseHat
	from time import sleep

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

	def check_wall(x,y,new_x,new_y):
		if maze[new_y][new_x] != r:
			return new_x, new_y
		elif maze[new_y][x] != r:
			return x, new_y
		elif maze[y][new_x] != r:
			return new_x, y
		return x,y

	game_over = False

	while not game_over:
		pitch = sense.get_orientation()['pitch']
		roll = sense.get_orientation()['roll']
		x,y = move_marble(pitch,roll,x,y)
		maze[y][x] = w
		sense.set_pixels(sum(maze,[]))
		sleep(0.05)
		maze[y][x] = b
	```

<iframe src="https://trinket.io/embed/python/4ffb8826a8" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
