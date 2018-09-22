---
layout: post
title: Rotate a context layer  
---
Here are a few functions we whipped up during the stream to create something like the following image
![](https://raw.githubusercontent.com/nickwan/random_lines/master/lines/executive_authority.png)

## Line function 
```python 
def draw_line(context, loc_x,loc_y, angle, max_width):
    """
    draw rand line like in that one stream nw did!
    
    inputs:
        context: pycairo context
        loc_x: x location (pixels)
        loc_y: y location (pixels)  
        angle: angle (degrees)
        max_width: max line width possible
        
    output:
        a line on the canvas  
    
    Note: The line can start or end off the canvas  
        
    """
    
    line_length = random.randint(1,566)
    angle = random.randint(0,360)
    hue = angle/(angle+random.randint(0,360)) 
    context.set_source_rgb(angle/(angle+random.randint(0,360)), angle/(angle+random.randint(0,360)), angle/(angle+random.randint(0,360)))
    
    if not random.randint(0,20):
        context.set_source_rgb(0, 0, 0)
    
    context.set_line_width(random.randint(1,max_width))
    context.save()

    context.translate(xc,yc)
    context.rotate(angle*(math.pi/180)) # needs radians 
    context.translate(-xc,-yc)

    context.move_to(loc_x,loc_y-(line_length/2))
    context.line_to(loc_x,(loc_y-(line_length/2))+line_length)
    context.stroke()
```

## Circle function  
```python 
def draw_circle(context,loc_x,loc_y, min_radius, max_lo_radius, 
                max_hi_radius, canvas_width, canvas_height, alpha):
    """
    draw rand circle like in that one stream nw did!
    
    inputs:
        context: pycairo context
        loc_x: x location (pixels)
        loc_y: y location (pixels)  
        min_radius: smallest circle radius possible  
        max_lo_radius: smallest "max" possible 
        max_hi_radius: largest "max" possible 
        canvas_width: canvas width max 
        canvas_height: canvas height max 
        
    output:
        a circle within the canvas bounds 
    
    Note: Circle does not expand beyond the given bounds
        
    """
    
    alpha_black = alpha + random.randrange(1,10)/100
    context.set_source_rgba(0,0,0,alpha_black)

    context.arc(loc_x, loc_y, radius+random.randint(1,20), 0, 2*math.pi)
    context.fill()

    context.set_source_rgb(1,1,1)
    context.arc(loc_x, loc_y, radius, 0, 2*math.pi)
    context.fill()

    context.set_source_rgba(angle/(angle+random.randint(0,360)), 
                            angle/(angle+random.randint(0,360)), 
                            angle/(angle+random.randint(0,360)), 
                            alpha)
    context.arc(loc_x, loc_y, radius, 0, 2*math.pi)
    context.fill()
    
```

## Usage example   
```python
filename = "img/lines/example.png"

WIDTH = 400
HEIGHT = 400 
xc = WIDTH/2
yc = HEIGHT/2

surface = cairo.ImageSurface(cairo.FORMAT_ARGB32, WIDTH, HEIGHT)
context = cairo.Context(surface)
context.set_source_rgb(1, 1, 1)
context.paint()

circles_appear = [random.randint(0,19), 
                  random.randint(0,19), 
                  random.randint(0,19)]

for ix in range(20):
    if ix in circles_appear:
        loc_x = random.randint(0+(2*max_radius),400-(2*max_radius))
        loc_y = random.randint(0+(2*max_radius),400-(2*max_radius))
        
        draw_circle(context,loc_x,loc_y, min_radius=3, max_lo_radius=15, 
                    max_hi_radius=60, canvas_width=WIDTH, 
                    canvas_height=HEIGHT, alpha=random.randrange(40,100)/100)
   
    loc_x = random.randint(0,400)
    loc_y = random.randint(0,400)
    draw_line(context, loc_x, loc_y, random.randint(0,360), 5)

surface.write_to_png(filename)
```

## Sample gallery from the live stream 
![](https://raw.githubusercontent.com/nickwan/random_lines/master/lines/mean_crystal.png)
![](https://raw.githubusercontent.com/nickwan/random_lines/master/lines/example8.png)
![](https://raw.githubusercontent.com/nickwan/random_lines/master/lines/fuck_i_spilled_my_crayons.png)
![](https://raw.githubusercontent.com/nickwan/random_lines/master/lines/WEIRD_RANDOM_LINES_1.png)
![](https://raw.githubusercontent.com/nickwan/random_lines/master/lines/refactor_ftw.png)
![](https://raw.githubusercontent.com/nickwan/random_lines/master/lines/where_is_the_third_circle.png)

## Link to notebook
[random_lines.ipynb](https://github.com/nickwan/random_lines/blob/master/random_lines.ipynb)
