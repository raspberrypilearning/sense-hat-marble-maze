## For the win

- Lastly, you'll want a way for the player to win. You can pick any black LED in the maze and set it as the target for the player to reach. The simplest way to do this is to create a new variable for the colour and then add it into your maze. Add the line and then update the maze.

	```python
	g = (0,255,0)

	maze = [[r,r,r,r,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,r,r,b,r,b,b,r],
			[r,b,r,b,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,b,r,r,r,r,b,r],
			[r,b,b,r,g,b,b,r],
			[r,r,r,r,r,r,r,r]]
	```

- Next you need a function to check whether the player has hit the target.

	```python
	def check_win(x,y):
	```

- This function needs to be able to alter the state of `game_over`, so add it in as a global variable first.

	```python
	def check_win(x,y):
		global game_over
	```

- Then the function needs to see whether the player has landed on the green LED. If it has, the game ends.

	```python
	def check_win(x,y):
		global game_over
		if maze[y][x] == g:
			game_over = True
			sense.show_message('You Win')
	```

- Then this function needs to be called inside the main game loop.

	```python
	while not game_over:
		pitch = sense.get_orientation()['pitch']
		roll = sense.get_orientation()['roll']
		x,y = move_marble(pitch,roll,x,y)
		check_win(x,y)
		maze[y][x] = w
		sense.set_pixels(sum(maze,[]))
		sleep(0.05)
		maze[y][x] = b
	```

- Your full code should now look like this:

	```python
	from sense_hat import SenseHat
	from time import sleep

	sense = SenseHat()
	sense.clear()

	r = (255,0,0)
	g = (0,255,0)
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
			[r,b,b,r,g,b,b,r],
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

	def check_win(x,y):
		global game_over
		if maze[y][x] == g:
			game_over = True
			sense.show_message('You Win')

	while not game_over:
		pitch = sense.get_orientation()['pitch']
		roll = sense.get_orientation()['roll']
		x,y = move_marble(pitch,roll,x,y)
		check_win(x,y)
		maze[y][x] = w
		sense.set_pixels(sum(maze,[]))
		sleep(0.05)
		maze[y][x] = b
	```

<iframe src="https://trinket.io/embed/python/84e8478d96" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

- Run your code. Well done: you have completed your Sense HAT game!

