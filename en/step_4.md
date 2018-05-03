## Set up the Sense HAT

+ Start by attaching the Sense HAT to your Raspberry Pi.

[[[rpi-sensehat-attach]]]

+ If you do not have a Sense HAT, you can create the project offline or in a web browser by using the Sense HAT emulator.

[[[rpi-sensehat-emulator]]]

+ Open the IDLE editor and create a new file, or if you are using the online emulator, open a new trinket.

[[[rpi-gui-idle-opening]]]

+ Save your IDLE file as **marble_maze.py**

+ In the new file, start by importing the Sense HAT module:

```python
from sense_hat import SenseHat
```

+ Next, create a connection to your Sense HAT and clear the screen by adding:

```python
sense = SenseHat()
sense.clear()
```
