---
layout: post
title: PyCairo in Google Colab
---
Google Colaboratory (or "colab" for short) is a cloud-based Python notebook with all the Jupyter Notebook tools, Terminal tools, and GPU processing available. 

## Install PyCairo via colab
```
# This advice comes from https://github.com/pygobject/pycairo/issues/39#issuecomment-391830334
!apt-get install libcairo2-dev libjpeg-dev libgif-dev
!pip install pycairo
```
## Setup a PyCairo notebook  
```python
import cairo
from google.colab import files
from IPython.display import SVG, display, Image
```

## Inline functions for displaying  
```python 
def show_svg(file):
    display(SVG(filename=file))
```

## Create PyCairo example 
```python
with cairo.SVGSurface("example.svg", 200, 200) as surface:
    context = cairo.Context(surface)
    x, y, x1, y1 = 0.1, 0.5, 0.4, 0.9
    x2, y2, x3, y3 = 0.6, 0.1, 0.9, 0.5
    context.scale(200, 200)
    context.set_line_width(0.04)
    context.move_to(x, y)
    context.curve_to(x1, y1, x2, y2, x3, y3)
    context.stroke()
    context.set_source_rgba(1, 0.2, 0.2, 0.6)
    context.set_line_width(0.02)
    context.move_to(x, y)
    context.line_to(x1, y1)
    context.move_to(x2, y2)
    context.line_to(x3, y3)
    context.stroke()
    
show_svg("example.svg")
```
![](https://raw.githubusercontent.com/nickwan/how_to__simple_display/master/example.png)  

*Note: SVG doesn't play nice via github, image above is PNG*  

## Link to notebook
[[colab] pycairo_in_colab.ipynb](https://colab.research.google.com/drive/18IA7e_DJ0kYQCdw0UQI7vg8W2Jo9FE-b)  
[[GitHub] pycairo_in_colab.ipynb](https://github.com/nickwan/pycairo_in_colab/blob/master/pycairo_in_colab.ipynb)  
