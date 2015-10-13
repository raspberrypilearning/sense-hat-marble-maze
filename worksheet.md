# Sense Hat Marble Maze

A Marble Maze is a game of skill, in which one or more marbles are placed inside of a maze, and the player needs to guide the marbles to a specific point by tiliting the maze in various directions, causing the marbles to roll around.

![Marble Maze](https://upload.wikimedia.org/wikipedia/commons/thumb/6/61/Round_maze.jpg/775px-Round_maze.jpg)

Given that the Sense HAT is capable of reporting it's exact orientation and has an in-built 8x8 pixel LED display, it makes the perfect device to create an electronic marble maze game.

## Setting up the Sense HAT

1. To begin with you'll need to start IDLE (`Menu>Programming>Python 3 (IDLE)`).

1. Now create a new text file to write your code in (`File>New File`)

1. You're going to need to import some modules from the `sense_hat` package to get going, so write the following three lines into your text file that will enable access to the Sense HAT and clear the LED matrix.

	```python
	from sense_hat import SenseHat
	sense = SenseHat()
	sense.clear()
	```

## Drawing the maze

1. To begin with you're going to need to display your maze on the LED matrix. It's best to use some squared paper to draw out your maze first, so that you can easily identify the paths through the maze. The maze you draw is up to you, but you could use the example below if you wanted. It is important that the maze is constructed from solid walls, and that there are no diagonal gaps.

1. Once you have drawn your maze, write the initial of the colour used for each square.

1. Now you can implement this in code. First you'll need to define the colours that you are using.

	```python
	r = (255,0,0)
	b = (0,0,0)
	```
	
1. And then you can draw your maze. You're going to use a *list of lists* to do this. Each row of the matrix is represented by a single list, which are all grouped together in a larger list.

	```python
	maze = [[r,r,r,r,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,r,r,b,r,b,b,r],
			[r,b,r,b,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,b,r,r,r,r,b,r],
			[r,b,b,r,g,b,b,r],
			[r,r,r,r,r,r,r,r]]

	```

1. To finish off this section, you can see how your maze looks on the LED matrix. To do this you're going to need to **flatten** the *list of lists*, into a single list. This is easy to do in Python, as you can add all the individual lists together (`sum(maze,[]`). So to then display this on the LED matrix, you can write:

	```python
	sense.set_pixels(sum(maze,[]))
	```

1. Your code should now look like this:

	```python
	from sense_hat import SenseHat

	sense = SenseHat()
	sense.clear()

	r = (255,0,0)
	b = (0,0,0)

	maze = [[r,r,r,r,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,r,r,b,r,b,b,r],
			[r,b,r,b,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,b,r,r,r,r,b,r],
			[r,b,b,r,g,b,b,r],
			[r,r,r,r,r,r,r,r]]

    sense.set_pixels(sum(maze,[]))
	```
1. Save it and run it to see the maze displayed on the LED matrix (`Ctrl` + `s`, `F5`)

## Adding a marble

1. You're going to need a marble to go in your maze. This can be achieved by changing one of the LEDs in the maze list to be white. Start by createing a variable to store the colour white, up where you have set the other colours.

	```python
	w = (255,255,255)
	```

1. Then you can set the starting position of the marble. You can use the variable `x` to store the horizontal position and the variable `y` to store the vertical positon. (**If you're using y to store a vertical positon, it's important to ensure you don't ever store the colour yellow with a `y`)

	```python
	x = 1
	y = 1
	```

1. Before you draw the marble, as it's going to be continually on the move, it's best to set up a main game loop straight away. You'll need a variable called `game_over` declared somewhere near the top of your program

	```python
	game_over = False
	```

1. Next you can create a `while` loop and use it to add the marble to the maze list and then redraw the maze.

```python
while not game_over:
    maze[y][x] = w
    sense.set_pixels(sum(maze,[]))

```

1. Your code should now look like this:


	```python
	from sense_hat import SenseHat

	sense = SenseHat()
	sense.clear()

	r = (255,0,0)
	b = (0,0,0)
	w = (255,255,255)

	maze = [[r,r,r,r,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,r,r,b,r,b,b,r],
			[r,b,r,b,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,b,r,r,r,r,b,r],
			[r,b,b,r,g,b,b,r],
			[r,r,r,r,r,r,r,r]]

	game_over = False

	while not game_over:
		maze[y][x] = w
		sense.set_pixels(sum(maze,[]))
	```

1. Save it and run it to see the maze and marble on the LED matrix (`Ctrl` + `s`, `F5`)

## Moving the marble

1. The marble's movement will be controlled by the orientation of the Sense HAT. The Sense HAT library can detect the *pitch*, *roll* and *yaw* of the board. You can see an picture illustrating this below.

	![orientation](images/orientation.png)

1. You don't need the *yaw* orientation of the SenseHat for this project, just the *pitch* and *roll*. Add these two lines into the `while` loop, so that you get constant and up-to-date readings of the orientation, and it looks like this

```python
while not game_over:
    pitch = sense.get_orientation()['pitch']
    roll = sense.get_orientation()['roll']
    maze[y][x] = w
    sense.set_pixels(sum(maze,[]))
```

1. Now it is time to move the marble. You're going to write a seperate function to do this.**Above** the `while` loop, you can define the new function.

```python
def move_marble(pitch, yaw, x, y):
```

1. The function has `pitch`, `yaw`, `x`, and `y` as parameters. You're going to want to keep the `x` and `y` positions of the marble unchanged (you'll see why later), so the first thing to do is stroe these values as other variables.

```python
def move_marble(pitch, yaw, x, y):
new_x = x
new_y = y
```

1. Now it's time to change the position of the marble, depending on the way that the Sense HAT is tilted. When the Sense HAT is lying flat, *pitch* and *yaw* should be approximately 0. They'll then either increase as the Sense HAT is tilted (0,1,2,3,4...), or they'll decrease (0,359,359,357,356...). You'll want to ignore very tiny movements (less than a degree) as the Sense HAT will very rarely be lying competely flat.

1. If the *pitch* is between 1 and 179, then `new_x` needs to decrease. If it's between 359 and 181, then `new_x`should increase.

```python
def move_marble(pitch,roll,x,y):
    new_x = x
    new_y = y
    if 1 < pitch < 179:
        new_x -= 1
    elif 359 > pitch > 181:
    new_x += 1
```

1. To test this code out, you'll need to call the function within the `while` loop.

```python
while not game_over:
    pitch = sense.get_orientation()['pitch']
    roll = sense.get_orientation()['roll']
    x,y = move_marble(pitch,roll,x,y)
    maze[y][x] = w
    sense.set_pixels(sum(maze,[]))

```

1. Save and run your code.



## What Next?

1. Can you play around with the variable values to make the game easier or more difficult?

1. Can you keep a score so that each time a column is successfully negotiated, the score increases by one point?

1. Can you think of other ways of controlling the astronaut? Maybe you could use the joystick or the humidity sensor?
