## Drawing the maze

- To begin with you're going to need to display your maze on the LED matrix. It's best to use some squared paper to draw the design out first, so that you can easily identify the paths through the maze. The layout is up to you, but you could use the example below if you wanted. It is important that the maze is constructed from solid walls, and that there are no diagonal gaps.

	![maze1](images/maze1.jpg)

- Once you have drawn your maze, write down the initial of the colour used for each square.

	![maze2](images/maze2.jpg)

- Now you can implement this in code. First, you'll need to define the colours that you are using.

	```python
	r = (255,0,0)
	b = (0,0,0)
	```
	
- Then you can draw your maze. You're going to use a **list of lists** to do this. Each row of the matrix is represented by a single list, which are all grouped together in a larger list.

	```python
	maze = [[r,r,r,r,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,r,r,b,r,b,b,r],
			[r,b,r,b,r,r,r,r],
			[r,b,b,b,b,b,b,r],
			[r,b,r,r,r,r,b,r],
			[r,b,b,r,b,b,b,r],
			[r,r,r,r,r,r,r,r]]

	```

- To finish off this section, you can see how your maze looks on the LED matrix. To do this you're going to need to **flatten** the **list of lists** into a single list. This is easy to do in Python, as you can add all the individual lists together using the syntax - `sum(maze,[])`. To display this on the LED matrix, you can write:

	```python
	sense.set_pixels(sum(maze,[]))
	```

- Your code should now look like this:

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
			[r,b,b,r,b,b,b,r],
			[r,r,r,r,r,r,r,r]]

    sense.set_pixels(sum(maze,[]))
	```

	<iframe src="https://trinket.io/embed/python/3312ca9b94" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>
	
- Save it and run it to see the maze displayed on the LED matrix (`Ctrl` + `s`, `F5`).

