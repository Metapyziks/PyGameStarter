# Resources
## Version Control
You'll use this to download (pull) your code from GitHub, or send changes you make (push)
back to the cloud as a backup and so you can work on your project elsewhere. Pick one:

### SourceTree
More functionality, a bit more complex to set up. You'll need to make sure you select the
option to install git, or else you can install it from Tools -> Options -> Git.

* Download: https://www.sourcetreeapp.com/

### GitHub Desktop
Less functionality, easier to set up. Integrates nicely with GitHub.

* Download: https://desktop.github.com/

## Text Editor
Choose one of these, which will help out when editing code by colouring the text to help
with readability and providing some suggestions while you type.

### Sublime Text
* Download: https://www.sublimetext.com/3

### Visual Studio Code
* Download: https://code.visualstudio.com/Download

### Notepad++
* Download: https://notepad-plus-plus.org/download/v6.9.2.html

## Python / Pygame
### Python 2.7
Make sure you install it to C:\Python27 if you can, since some of the commands below will
assume it is installed there.

* Download: https://www.python.org/downloads/

### Pygame
Make sure you get a version for Python 2.7

* Download: http://www.pygame.org/download.shtml
* Documentation: http://www.pygame.org/docs/
* Cheatsheet: http://www.cogsci.rpi.edu/~destem/gamedev/pygame.pdf

### PyTmx
This Python package lets you import maps created in Tiled. To install, run this in the command prompt:

```
C:\Python27\python.exe -m pip install pytmx
```

Documentation: https://github.com/bitcraft/PyTMX#documentation

## Tiled Map Editor
Used to create tile-based levels for your game.

* Download: http://www.mapeditor.org/

# Examples
## Basic Game Outline
This example will open a 1280 by 720 window, clear the screen with a blue background every frame,
and run at a fixed update rate of 60 times a second.

```python
import os, sys
import pygame

from pygame.locals import *

class ExampleGame:
    def __init__(self, width=1280, height=720, frame_rate=60):
        pygame.init()
        pygame.display.set_caption("My Example Game!")

        self.width = width
        self.height = height

        self.frame_rate = frame_rate

        self.background_color = (100, 149, 237)

        self.clock = pygame.time.Clock()
        self.screen = pygame.display.set_mode((self.width, self.height))

    def Run(self):
        self.LoadSprites()
        self.MainLoop()

    def LoadSprites(self):
        # Load sprites and sounds
        return

    def UpdateFrame(self):        
        for event in pygame.event.get():
            if event.type == pygame.QUIT: 
                sys.exit()

        # Move things around and listen to input here

    def RenderFrame(self):
        self.screen.fill(self.background_color)

        # Draw sprites and text here

        pygame.display.flip()

    def MainLoop(self):
        while 1:
            self.UpdateFrame()
            self.RenderFrame()
            self.clock.tick(60)

if __name__ == "__main__":
    MainWindow = ExampleGame()
    MainWindow.Run()
```

## Loading and Drawing Sprites
This example adds functionality to the functions defined in the previous example, and will load
an image at "images/example.png" and convert it to a format that pygame knows has transparency.
Then each update it moves the sprite horizontally by 1 pixel, and draws it to the screen.

```python
    def LoadSprites(self):
        # Load sprites and sounds
        self.example_sprite = pygame.image.load('images/example.png').convert_alpha()
        self.example_sprite_rect = self.example_sprite.get_rect()

    def UpdateFrame(self):        
        for event in pygame.event.get():
            if event.type == pygame.QUIT: 
                sys.exit()

        # Move things around and listen to input here
        self.example_sprite_rect.move_ip(1, 0)

    def RenderFrame(self):
        self.screen.fill(self.background_color)

        # Draw sprites and text here
        self.screen.blit(self.example_sprite, self.example_sprite_rect)

        pygame.display.flip()
```

## Loading and Playing Sounds
This example builds from the previous example, loading in a sound effect that plays when the
example sprite hits the right hand side of the screen. The sprite will then also be moved back
to the left side of the screen again.

```python
    def LoadSprites(self):
        # ... at the end of the function ...
        self.example_sound = pygame.mixer.Sound("sounds/example.wav")

    def UpdateFrame(self):
        # ... at the end of the function
        if self.example_sprite.right >= self.width:
            self.example_sound.play()
            self.example_sprite.left = 0
```