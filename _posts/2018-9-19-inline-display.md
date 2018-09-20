---
layout: post
title: Make a simple inline display for your outputs
---
# Import packages
```python 
import cairo
from IPython.display import SVG, display, Image
```

# Inline functions for displaying  
```python 
def show_img(file):
    display(Image(filename=file))
    
def show_svg(file):
    display(SVG(filename=file))
```

# Create pycairo example, write to PNG, display PNG inline 
```python
surface = cairo.ImageSurface(cairo.FORMAT_ARGB32, 200, 200)
context = cairo.Context(surface)

x, y, x1, y1 = 0.1, 0.5, 0.4, 0.9
x2, y2, x3, y3 = 0.6, 0.1, 0.9, 0.5
context.scale(200, 200)
context.set_line_width(0.04)
context.move_to(x, y)
context.curve_to(x1, y1, x2, y2, x3, y3)
context.set_source_rgb(0, 0, 0)
context.stroke()
context.set_source_rgba(1, 0.2, 0.2, 0.6)
context.set_line_width(0.02)
context.move_to(x, y)
context.line_to(x1, y1)
context.move_to(x2, y2)
context.line_to(x3, y3)
context.stroke()

surface.write_to_png("example.png")
show_img('example.png')
```
![](https://raw.githubusercontent.com/nickwan/how_to__simple_display/master/example.png)

# Create pycairo example, write to SVG, display SVG inline 
```python
with cairo.SVGSurface('example.svg', 200, 200) as surface:
    context = cairo.Context(surface)
    x, y, x1, y1 = 0.1, 0.5, 0.4, 0.9
    x2, y2, x3, y3 = 0.6, 0.1, 0.9, 0.5
    context.scale(200, 200)
    context.set_line_width(0.04)
    context.move_to(x, y)
    context.curve_to(x1, y1, x2, y2, x3, y3)
    context.set_source_rgb(1, 0.2, 0.2)
    context.stroke()
    context.set_source_rgba(0, 0, 0, 0.6)
    context.set_line_width(0.02)
    context.move_to(x, y)
    context.line_to(x1, y1)
    context.move_to(x2, y2)
    context.line_to(x3, y3)
    context.stroke()

show_svg('example.svg')
```
![](https://github.com/nickwan/how_to__simple_display/blob/master/example.svg)

# Link to notebook
[how_to_simple_display.ipynb](https://github.com/nickwan/how_to__simple_display/blob/master/how_to_simple_display.ipynb)
