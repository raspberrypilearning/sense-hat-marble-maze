## Setting up the Sense HAT

- To begin with you'll need to start IDLE (`Menu>Programming>Python 3 (IDLE)`) if you're using a real SenseHat, or open a new [Trinket](https://trinket.io/) if you're using the emulator.

- Now create a new text file in which to write your code (`File>New File`).

- You're going to need to import some modules from the **sense_hat** package to get going, so write the following three lines into your text file to enable access to the Sense HAT and to clear the LED matrix.

	```python
	from sense_hat import SenseHat
	sense = SenseHat()
	sense.clear()
	```
	<iframe src="https://trinket.io/embed/python/4728cbe745" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

