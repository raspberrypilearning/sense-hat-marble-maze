## Adding a marble

- You're going to need a marble to go in your maze. This can be achieved by changing one of the LEDs in the maze list to be white. Start by creating a variable to store the colour white, in the place where you have set the other colours.

	```python
	w = (255,255,255)
	```

- Then you can set the starting position of the marble. You can use the variable `x` to store the horizontal position and the variable `y` to store the vertical position. (Note that, if you're using `y` to store a vertical position, it's important to ensure you don't ever store the colour yellow with a `y`).

	```python
	x = 1
	y = 1
	```

- As the marble is going to be continually on the move, it's best to set up a main game loop straight away, before drawing the marble itself. You'll need a variable called `game_over` declared somewhere near the top of your program

	```python
	game_over = False
	```

- Next you can create a `while` loop, and use it to add the marble to the maze list and then redraw the maze.

	```python
	while not game_over:
		maze[y][x] = w
		sense.set_pixels(sum(maze,[]))

	```

- Your code should now look like this:


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

	game_over = False

	while not game_over:
		maze[y][x] = w
		sense.set_pixels(sum(maze,[]))
	```

- Save it and run it to see the maze and marble on the LED matrix (`Ctrl` + `s`, `F5`)

<iframe src="https://trinket.io/embed/python/fbd97f0e7e" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

