# hooman
~ pygame for humans

```
pip install hooman
```
# demos


![](assets/color_change.gif)

color change

```python
from hooman import Hooman

import pygame

hapi = Hooman(500, 500)

def handle_events(event):
    if event.type == pygame.QUIT:
        hapi.is_running = False

hapi.handle_events = handle_events

while hapi.is_running:
    hapi.background((255, 255, 255))

    hapi.no_stroke()
    mx = (hapi.mouseX() / hapi.WIDTH) * 255

    hapi.fill((0, mx, 0))
    for i in range(50 , 200, 60):
        hapi.rect(i, 50, 30, 30)

    hapi.fill((255, 0, 0))
    hapi.ellipse(hapi.mouseX(), hapi.mouseY(), 10, 10)

    hapi.stroke_size(1)
    hapi.stroke((255, 10, 10))
    hapi.line(0, hapi.mouseY(), hapi.mouseX()-10, hapi.mouseY())

    hapi.flip_display()
    hapi.event_loop()

pygame.quit()

```

lines

![](assets/lines.gif)

```python
from hooman import Hooman

import pygame

hapi = Hooman(500, 500)

def handle_events(event):
    if event.type == pygame.QUIT:
        hapi.is_running = False

hapi.handle_events = handle_events

while hapi.is_running:
    hapi.background((255, 255, 255))

    hapi.stroke_size(5)
    hapi.stroke((0, 255, 0))

    for i in range(0, hapi.WIDTH, 20):
        hapi.line(i, 0, hapi.mouseX(), hapi.mouseY())

    hapi.flip_display()
    hapi.event_loop()

pygame.quit()

```

squares

![](assets/squares.jpg)

```python
from hooman import Hooman

import pygame

hapi = Hooman(500, 500)

def handle_events(event):
    if event.type == pygame.QUIT:
        hapi.is_running = False

hapi.handle_events = handle_events

size = 50
while hapi.is_running:
    hapi.background((255, 255, 255))

    hapi.no_stroke()
    hapi.fill((0, 255, 0))
    hapi.rect(10, 10, size, size)
    hapi.fill((255, 255, 0))
    hapi.rect(100, 100, size, size)
    hapi.fill((255, 0, 0))
    hapi.rect(100, 10, size, size)
    hapi.fill((0, 0, 255))
    hapi.rect(10, 100, size, size)

    hapi.flip_display()
    hapi.event_loop()

pygame.quit()

```

buttons


![](assets/demo_buttons.png)

```python

from hooman import Hooman

import pygame

window_width, window_height = 500, 500
hapi = Hooman(window_width, window_height)

bg_col = (255, 255, 255)

#the function that gets called when the button is clicked on
def button_clicked(this): 
    if this.y == 250:
        this.y = 300
    else:
        this.y = 250
        
    print(this.y)



grey_style = {
    'background_color':(200, 200, 200),
    'curve':0.1,
    'padding_x':5,
    'padding_y':5,
    'font_size':15
    }

button1 = hapi.button(150, 150, "Click Me",
    grey_style
)

def button_hover(this):
    hapi.background(hapi.color['green'])
stylex = grey_style.copy()
stylex['on_hover'] = button_hover

buttonx = hapi.button(150, 10, "Hover Me",
    stylex
)

button2 = hapi.button(150, 250, "No Click Me",
    {
    'background_color':(200, 200, 200),
    'outline':hapi.outline({
            'color':(200, 200, 200), 
            'amount':5
            }),
    'curve':0.3,
    'on_click':button_clicked,
    'padding_x':40,
    'padding_y':10,
    'font_size':15
    })

def handle_events(event):
    if event.type == pygame.QUIT:
        hapi.is_running = False
    if event.type == pygame.KEYDOWN:
        if event.key == pygame.K_ESCAPE:
            hapi.is_running = False


hapi.handle_events = handle_events

clock = pygame.time.Clock()

while hapi.is_running:
    hapi.background(bg_col)

    if button1.update(): #if the button was clicked
        bg_col = (255, 0, 0) if bg_col == (255, 255, 255) else (255, 255, 255)
    
    # for i in range(5):
    #     x = hapi.button(10+i*80, hapi.mouseY(), "Click Me",
    #         grey_style
    #     )
    # don't use it for ui elements in loop lile the above
    # each element can also be individually
    # updated
    hapi.update_ui() 
    hapi.event_loop()

    hapi.flip_display()

    clock.tick(60)

pygame.quit()

```

transparent circles

```python
import pygame
from hooman import Hooman
pygame.init()

hapi = Hooman(800, 600)


while hapi.is_running:
    hapi.background(hapi.color['white'])


    hapi.set_alpha(100)
    hapi.fill(hapi.color['red'])
    hapi.alpha_ellipse(100, 100, hapi.mouseX()//2, hapi.mouseX()//2)
    hapi.fill(hapi.color['yellow'])
    hapi.alpha_ellipse(100, 100, 100, 100)
    hapi.fill(hapi.color['green'])
    hapi.alpha_ellipse(150, 100, 100, 100)
    pygame.display.flip()

    hapi.event_loop()

pygame.quit()
```

# Docs

## Attributes

## .WIDTH

- `hapi.WIDTH` is gives the width of the screen

## .HEIGHT

- `hapi.HEIGHT` is gives the height of the screen

## .is_running

- if loop is running

## .screen

still exposes a screen to draw with any pygame shape

`pygame.draw.arc(hapi.screen, (255, 0, 0), [80,10,200,200], hapi.PI, hapi.PI/2, 2)`

## Constants

## .PI

The value of pi as provided by the maths module

`pygame.draw.arc(hapi.screen, (255, 0, 0), [80,10,200,200], hapi.PI, hapi.PI/2, 2)`


## Colors, strokes & Fill

## .fill

- used for colouring next shapes
- `hapi.fill((100, 100, 100))` for r g b
- `hapi.fill(100)`  same as `hapi.fill((100, 100, 100))`

## .stroke

- used to set color of next shapes' outlines
- `hapi.stroke((100, 100, 100))` for r g b
- `hapi.stroke(100)`  same as `hapi.stroke((100, 100, 100))`

## .background

- used to set background color of screen
- `hapi.background((100, 100, 100))` for r g b
- `hapi.background(100)`  same as `hapi.background((100, 100, 100))`

## .color

same as

```
{
    'red': (255, 0, 0),
    'green': (0, 255, 0),
    'blue': (0, 0, 255),
    'black': (0, 0, 0),
    'white': (255, 0, 0),
    'yellow': (255, 255, 0),
    'grey': (100, 100, 100)
}
```

also `.colors`, `.colours`, `.colour` same

## Size

## .stroke_size

- used to control thickness of lines and outlines
- `hapi.stroke_size(size)` where size is an int

## .no_stroke

- set lines and outlines thickness to 0
- `hapi.no_stroke()`
- same as `hapi.stroke_size(0)`

## .font_size

- sets font size of text
- `hapi.font_size(12)`

## Basic elements

## .rect

`hapi.rect(x, y, width, height)`
- x - x coordinate
- y - y coordinate

## .ellipse

`hapi.ellipse(x, y, width, height)`
- x - x coordinate
- y - y coordinate

## .line

`hapi.line(x1, y1, x2, y2)`

- x1 - x coordinate of first point
- y1 - y coordinate of first point
- x2 - x coordinate of second point
- y2 - y coordinate of second point

## .text

`.text(letters, x, y)`

- letters - string of chars eg. 'abcd'
- x - x coordinate
- y - y coordinate
- will convert any type passed to string
- `hapi.text(5, 10, 10)` is valid
- `hapi.text(hapi.mouseX(), 10, 10)` is valid out of the box

## .polygon

`.polygon(coords, fill=True)`

- coords is a 2d array [(0,0), (10, 10), (10, 100)]
- if fill is `False`, only the outline will be drawn
- adjust outline with `.stroke_size`

## .begin_shape

`hapi.begin_shape()` starts drawing a polygon

## .vertex

`.vertex((100, 200))`

## .end_shape

`hapi.end_shape(fill=True)` draws polygon on closing

Minimal demo of `.begin_shape`, `.vertex` and `.end_shape`

```python
from hooman import Hooman

import pygame

hapi = Hooman(500, 500)

def handle_events(event):
    if event.type == pygame.QUIT:
        hapi.is_running = False

hapi.handle_events = handle_events

while hapi.is_running:
    hapi.background(hapi.color['white'])

    hapi.fill(hapi.color['blue'])
    hapi.stroke_size(4)

    hapi.begin_shape()
    hapi.vertex((0, 0))
    hapi.vertex((100, 0))
    hapi.vertex((hapi.mouseX(), hapi.mouseY()))
    hapi.end_shape()

    # same as hapi.polygon([(0, 0), (100, 0), (hapi.mouseX(), hapi.mouseY())])

    hapi.flip_display()
    hapi.event_loop()

pygame.quit()

```

## Interactivity

## .mouseX

- `hapi.mouseX()` gives the current x coordinate of the mouse

## .mouseY

- `hapi.mouseY()` gives the current y coordinate of the mouse

## Pygame specifics

## .flip_display

- is just `pygame.display.flip()` behind the scene

## .event_loop

requires

```python
def handle_events(event):
    if event.type == pygame.QUIT:
        hapi.is_running = False

hapi.handle_events = handle_events
```

- is put inside `hapi.is_running` loop

## .set_caption

same as `pygame.display.set_caption`

# Ui

## .update_ui

- no need to update each element if you call this
- called inside `hapi.is_running` loop
- here is when **NOT** to use it:

```python
while hapi.is_running:
    for i in range(5):
            x = hapi.button(10+i*80, hapi.mouseY(), "Click Me",
                grey_style
            )
        hapi.update_ui() 
```

## .button

Create a button with `hapi.button(x, y, text, [optional paramters])`

- `x` - x location of the button
- `y` - y location of the button
- `text` - the text on the button
- `[optional parameters]` - a dictionary of any extra options you want for the button listed below

#### Optional Parameters

- surface - the surface you want the button on, by default it is the main window
- background - the color of the utton background
- hover_background_color - the color of the button background when the mouse is over the button
- font - the font of the text, by default it is Calibri
- font_size - the size of the text, by default it is 30
- font_colour - the colour of the text, by default it is black
- outline - this creates an outline for the button, must be a `hapi.outline()` object
- action - this is a function that gets called when the button is clicked
- action_arg - if the function given in action requires a parameter, you can use this to send to the function
- image - this should be a `pygame.Surface()` object that the button will show instead
- hover_image - this should be a `pygame.Surface()` object that the button will show when the mouse is over the button
- enlarge - this will resize the button when the mouse is over the button, this should be a bool
- enlarge_amount - this is the percentage that you want the button to resize to when the mouse is over the button (1 = no change)
- calculate_size - when set to True, this will calculate the width and height of the button from the size of the text
- padding_x - an integer that is added on to the width on both sides of the text when calculate_size is set to True
- padding_y - an integer that is added on to the height on both sides of the text when calulate_size is set to True
- dont_generate - when set to True, the button will not generate the images to put on screen, this can be handy if you want to use calculate_size without supplying text, you will need to call `button.update_text()` to generate the images before drawing
- curve - the amount of curve you want the button to have on the edges with 0 being no curve and 1 being full curve, by default it is 0
- on_hover_enter - when start hovering
- on_hover_exit - when end hovering
- on_click - when button clicked
```python

def on_hover_enter(this): # this refers to the button
    this.background_color = hapi.color['blue']

button = hapi.button(150, 250, "Click Me",
        {'on_hover_enter':on_hover_enter}
    )
```

#### Methods

- update() - this updates the button and draws it on screen, this should be called every frame
- Update_text(text) - this changes the text and recreates the button
- get_rect() - this returns a pygame.Rect of the button
- width() - this returns the width of the button
- height() - this returns the height of the button

### Outline
create a outline for ui elements with `hapi.outline([optional parameters])`

- `[optional parameters]` - options for the outline

#### Optional paramters

- type - the type of outline, there is 'full' and 'half', by default it is 'full'
- amount - the thickness of the outline, by default it is 2
- color - the colour of the outline, by default it is black
