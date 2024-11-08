# Seaborn

Plotly has a lot of wow factor or whatever, but Seaborn produces the most impressive visual media I've basically ever seen in an inherently digital format.

We will use it today to produce a work of art that makes me feel roughly the way I felt the first time I saw imaging of the tiling work at the مسجد شاه. I have deliberately stolen the following image: it is "owned" by a company based in a country which sanctions the artists and artisans that maintain this tiling. I instead credit بهاء الدين محمد بن حسين العاملي, the mosque's designer.

The grasp of color by the artists and artisans that produced this work is stunning. To my mind the only things I've seen come close outside of the Islamic Golden Age are rigorous scientific endeavours into color theory by modern vision scientists. This is unsurprising - much of modern mathematics arises from scholars who would've contemporaries of these artists.

Using a variety of scientific and mathematical techniques, seaborn contains are four uniquely impressive "color maps", known as "perceptually uniform color maps". Seaborn additional provides a way to address five earlier efforts from matplotlib which I find impressive but less so. They are as follows:


```python
from PIL import Image as im
import numpy as np
import seaborn as sns
import random

CMPS = ["rocket", "mako", "flare", "crest", "viridis", "plasma", "inferno", "magma", "cividis"]
CMPS = [sns.color_palette(cmap, as_cmap=True) for cmap in CMPS] # I found this on the Seaborn website
CMPS[1]
```




<div style="vertical-align: middle;"><strong>mako</strong> </div><div class="cmap"><img alt="mako colormap" title="mako" style="border: 1px solid #555;" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAgAAAABACAYAAABsv8+/AAAAE3RFWHRUaXRsZQBtYWtvIGNvbG9ybWFwf+ab6gAAABl0RVh0RGVzY3JpcHRpb24AbWFrbyBjb2xvcm1hcPRUC3IAAAAwdEVYdEF1dGhvcgBNYXRwbG90bGliIHYzLjcuMSwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZyqv+E0AAAAydEVYdFNvZnR3YXJlAE1hdHBsb3RsaWIgdjMuNy4xLCBodHRwczovL21hdHBsb3RsaWIub3JnBAlnagAAAg1JREFUeJzt1juS2zAURcEHsBx5/+vVJJRcBAFDnPR2Jyx8SY0dnPb3+POqqmqtVVVVq/PZel3mP+vj/GK8vGcY7/Y9Xv/dubp91/xcLX//e30xv7h/nK9f3le3+97j+e/89zuu++7nh3urTedrcc9+/f/j12q9t2F9Pv7M93FfLe6rzb6az7f3/HVc13/G+/r2/vl7bs/+3b7l+7fnN+8fvv/r967uv90zP9++Pj/f1zbf0xb3rM618f4+Pzee38739t2+zbMP37Vcb69hfF1/+jwW46OG8fmi47ZvnG+P5vtt/vpcrY/z/fzDfdafzp/jfv4H7eN8u84fNZ9/es9yfwEAcQQAAAQSAAAQSAAAQCABAACBBAAABBIAABBIAABAIAEAAIEEAAAEEgAAEEgAAEAgAQAAgQQAAAQSAAAQSAAAQCABAACBBAAABBIAABBIAABAIAEAAIEEAAAEEgAAEEgAAEAgAQAAgQQAAAQSAAAQSAAAQCABAACBBAAABBIAABBIAABAIAEAAIEEAAAEEgAAEEgAAEAgAQAAgQQAAAQSAAAQSAAAQCABAACBBAAABBIAABBIAABAIAEAAIEEAAAEEgAAEEgAAEAgAQAAgQQAAAQSAAAQSAAAQCABAACBBAAABBIAABBIAABAIAEAAIEEAAAEEgAAEEgAAEAgAQAAgQQAAAQSAAAQ6AcTSxI150SdAwAAAABJRU5ErkJggg=="></div><div style="vertical-align: middle; max-width: 514px; display: flex; justify-content: space-between;"><div style="float: left;"><div title="#0b0405ff" style="display: inline-block; width: 1em; height: 1em; margin: 0; vertical-align: middle; border: 1px solid #555; background-color: #0b0405ff;"></div> under</div><div style="margin: 0 auto; display: inline-block;">bad <div title="#00000000" style="display: inline-block; width: 1em; height: 1em; margin: 0; vertical-align: middle; border: 1px solid #555; background-color: #00000000;"></div></div><div style="float: right;">over <div title="#def5e5ff" style="display: inline-block; width: 1em; height: 1em; margin: 0; vertical-align: middle; border: 1px solid #555; background-color: #def5e5ff;"></div></div>




```python
CMPS[3]
```




<div style="vertical-align: middle;"><strong>crest</strong> </div><div class="cmap"><img alt="crest colormap" title="crest" style="border: 1px solid #555;" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAgAAAABACAYAAABsv8+/AAAAFHRFWHRUaXRsZQBjcmVzdCBjb2xvcm1hcDDWw8gAAAAadEVYdERlc2NyaXB0aW9uAGNyZXN0IGNvbG9ybWFwzolqLgAAADB0RVh0QXV0aG9yAE1hdHBsb3RsaWIgdjMuNy4xLCBodHRwczovL21hdHBsb3RsaWIub3JnKq/4TQAAADJ0RVh0U29mdHdhcmUATWF0cGxvdGxpYiB2My43LjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcECWdqAAAB3UlEQVR4nO3WMXLbMBRAQcj3L3KIHCdnMlPEyoxBIWBkjZu320igwU/IbN7t568fxxhjHOOP4+PLdv3x+X7ad/u/OdP6PO9V57qvj+85x2L9fjx33249vjp3cX3M+zb3jc2++1+e/T37+a+Zd77++QGvn//4/Pcv2/dy9fdvz7H4navzPXuO077j4r6r8xbr1XOm9fL6ad7jQfPz5/vn55xfxG7/dJDF/tvT+x+f57aZ8/f+0wv49/zVOXfn38+7dv3y85bvabp/+X9e7JuONV9fz12c5+L9bwMAyBEAABAkAAAgSAAAQJAAAIAgAQAAQQIAAIIEAAAECQAACBIAABAkAAAgSAAAQJAAAIAgAQAAQQIAAIIEAAAECQAACBIAABAkAAAgSAAAQJAAAIAgAQAAQQIAAIIEAAAECQAACBIAABAkAAAgSAAAQJAAAIAgAQAAQQIAAIIEAAAECQAACBIAABAkAAAgSAAAQJAAAIAgAQAAQQIAAIIEAAAECQAACBIAABAkAAAgSAAAQJAAAIAgAQAAQQIAAIIEAAAECQAACBIAABAkAAAgSAAAQJAAAIAgAQAAQQIAAIIEAAAECQAACBIAABAkAAAgSAAAQJAAAIAgAQAAQQIAAIJ+A9tsQVtfMWhrAAAAAElFTkSuQmCC"></div><div style="vertical-align: middle; max-width: 514px; display: flex; justify-content: space-between;"><div style="float: left;"><div title="#a5cd90ff" style="display: inline-block; width: 1em; height: 1em; margin: 0; vertical-align: middle; border: 1px solid #555; background-color: #a5cd90ff;"></div> under</div><div style="margin: 0 auto; display: inline-block;">bad <div title="#00000000" style="display: inline-block; width: 1em; height: 1em; margin: 0; vertical-align: middle; border: 1px solid #555; background-color: #00000000;"></div></div><div style="float: right;">over <div title="#2c3172ff" style="display: inline-block; width: 1em; height: 1em; margin: 0; vertical-align: middle; border: 1px solid #555; background-color: #2c3172ff;"></div></div>



Mako "makes me feel" similarly to the way the photography of the Isfahan tileset make me feel. But how can I create a tiling?

I believe the intent of بهاء الدين محمد بن حسين العاملي and other artisans is beyond my ability to grasp, so I will not place firm intent behind placing my tiles. Rather, I will place and color them randomly, then tune the process to evoke a similar feeling.

I will create an image of a fixed size, break it into tiles, color tiles with "mako" and perhaps other maps, and see how they make me feel.


```python
siz = 400
# A way to create a new array of size s
new = lambda s : [[0 for i in range(s)] for j in range(s)]
# A way to see an array as an image
see = lambda a : im.fromarray(np.array(a).astype(np.uint8))
see(new(siz))
```




    
![png](sns_files/sns_5_0.png)
    



It would be a simple matter to break this into rectangles, but there seems a much more complex geometry at play in Isfahan. I will instead:
* Select some number _n_ of random locations
* Computer which random location each pixel is closest too
* Color each tile randomly.
That is two randoms for those following along at home. Let's begin


```python
# A way to get a random point given some size s
rpt = lambda s : (random.randint(0, s - 1), random.randint(0, s - 1))
# A way to measure distance between two points. We want integers here.
dst = lambda a, b : int(((a[0] - b[0]) ** 2 + (a[1] - b[1]) ** 2) ** 0.5)
```

We need to test this code, so we'll pick a random point and color the entire grid based on proximity.

Test it a few times to make sure it changes.


```python
siz = 400
pnt = rpt(siz)
img = [[dst((i,j),pnt) for i in range(siz)] for j in range(siz)]
see(img)
```




    
![png](sns_files/sns_9_0.png)
    



It is non-obvious how to apply a color map. Here is one example. We create a grid that increases in one direction, and rather than plotting in grayscale, we plot the cmap as a function over the pixel location.


```python
mako = CMPS[1]
mako(100)
```




    (0.22698081, 0.35544612, 0.60642528, 1.0)



Here's an interesting thing - those numbers are not between 0 and 255. They are between 0 and 1. So we need to multiple by 255 to be able to see much of anything at all.


```python
mako = lambda x : [255 * i for i in CMPS[1](x)]
mako(100)
```




    [57.88010655, 90.6387606, 154.6384464, 255.0]



Well, really we should be able to do this for all cmaps, so, we make a double lambda - it takes a cmap function that return 0-1 scale colors, and returns a new function that returns 0-255 scale colors.


```python
scl = lambda c : lambda x : [255 * i for i in CMPS[c](x)]
mako = scl(1)
mako(100)
```




    [57.88010655, 90.6387606, 154.6384464, 255.0]




```python
siz = 400
img = [[i for i in range(siz)] for j in range(siz)]
see(img)
```




    
![png](sns_files/sns_16_0.png)
    




```python
siz = 400
img = [[mako(i) for i in range(siz)] for j in range(siz)]
see(img)
```




    
![png](sns_files/sns_17_0.png)
    



We can test distance.


```python
siz = 400
pnt = rpt(siz)
img = [[mako(dst((i,j),pnt)) for i in range(siz)] for j in range(siz)]
see(img)
```




    
![png](sns_files/sns_19_0.png)
    



Let's try adding a few points, and coloring randomly based on which is closer.

To do this, we introduce a new "thing" - a dictionary. Dictionaries relate "keys" to "values" - like words to definitions. Ours will relate random points to random colors. Not too bad, I hope.

The notation is:

```
d = { key_0 : val_0, key_1 : val_1 }
```

We can look up a value given a key:
```
print(d[key_0]) # prints 'val_0'
```
Keys can be pretty much anything except a list or another dictionary. Values can be anything at all.

We can look at *only* keys or *only* values via `d.keys()` and `d.values()`.


```python
siz = 400
rps = [rpt(siz) for i in range(5)]
rps = {i : mako(random.randint(0, 255)) for i in rps}
rps.keys(), rps.values()
```




    (dict_keys([(274, 143), (302, 35), (192, 162), (266, 305), (91, 275)]),
     dict_values([[17.863703700000002, 7.7807589, 13.4239803, 255.0], [18.89536485, 8.5637262, 14.87830905, 255.0], [20.942772599999998, 10.221241500000001, 17.7756981, 255.0], [212.35803555, 240.57559605, 220.45381635, 255.0], [72.07371255, 191.9895867, 173.16529545, 255.0]]))



We can loop over the dictionary keys the way we loop over anything else...


```python
_ = [print(i) for i in rps]
```

    (274, 143)
    (302, 35)
    (192, 162)
    (266, 305)
    (91, 275)


However, using indices is quite different. The points are indices, and the keys are the values at the index. It's quite odd to look at this, so I grab a valid key by looping over the keys and taking the first key, then plugging that into the dictionary.


```python
ky0 = [i for i in rps][0]
rps[ky0]
# Or in a single line...
rps[[i for i in rps][0]]
```




    [17.863703700000002, 7.7807589, 13.4239803, 255.0]



Okay - so now we have colors associated with areas. How do we associate a pixel with an area? Well, for each pixel, we need to know the closest point. We just loop over points and find the closest.

I do this by looping over the points in the dictionary, calculating distances, and taking the minimum. But I use one trick: Besides the distance, I also save the color associated with the point. So whatever the minimum is, that's the color I want, because it's the color associated with the closest point (and therefore my tile)!

This checks random points. See how each finds a different color!


```python
min([(dst(rpt(400),i), rps[i]) for i in rps])
```




    (63, [72.07371255, 191.9895867, 173.16529545, 255.0])



We'll now define a few new things - a lambda that returns a tiling given (a) a cmap, (b) a size and (c) a number of colors, and a lambda that returns a color given a tiling and a point.


```python
til = lambda c, s, n : {rpt(s) : scl(c)(random.randint(0,255)) for i in range(n)}
til(1, 400, 10)
```




    {(36, 36): [62.27980515, 52.73007045, 107.06251245, 255.0],
     (2, 379): [52.83855765, 157.51902585, 170.3217369, 255.0],
     (371, 50): [61.5310614, 79.77989925, 148.61046825, 255.0],
     (226, 30): [52.1962458, 36.5139498, 72.31764555, 255.0],
     (285, 201): [59.927346, 47.69637045, 96.42896400000001, 255.0],
     (206, 40): [12.5791959, 4.358694600000001, 6.46608345, 255.0],
     (378, 245): [206.25702285, 238.15859640000002, 215.4392541, 255.0],
     (89, 310): [52.388344950000004, 154.16378685, 169.71629295, 255.0],
     (54, 50): [142.02369075000001, 218.58274365, 178.88358885000002, 255.0],
     (264, 241): [48.689557199999996, 32.7176985, 63.947290949999996, 255.0]}




```python
col = lambda t, p : min([(dst(p,i), t[i]) for i in t])[1]
t = til(1, 400, 10)
col(t, (100,100)), col(t, (100,101)), col(t, (300,300))
```




    ([61.92825705, 78.5908419, 147.67877985, 255.0],
     [61.92825705, 78.5908419, 147.67877985, 255.0],
     [52.6175568, 125.1489051, 163.2424269, 255.0])



We put it all together to tile an image. We just need a tiling and a size. We could do without the size in fact, but it's a bit scuffed.


```python
siz = 400
art = lambda t, s : [[col(t, (i,j)) for i in range(s)] for j in range(s)]
t = til(1, siz, 10)
see(art(t, siz))
```




    
![png](sns_files/sns_32_0.png)
    



With 400x400 = 16000 pixels, I probably need more than 10 tiles. Let's try 160. It took me 33 seconds, which is slow but hey, art amirite.


```python
see(art(til(1, siz, 160), siz))
```




    
![png](sns_files/sns_34_0.png)
    



I don't know why I made this so hard to write:

```
see(art(til(1, siz, 160), siz))
```

Let's make an easier function to let you test faster.

By the way, how long it takes to see something is basically height time width times number of tiles, just so you know what will take a long time.

Try different 'c' for color changes, and change 's' and 'n' just in order to see something you like without waiting forever!


```python
csn = lambda c, s, n : see(art(til(c, s, n), s))
csn(0, 400, 160)
```




    
![png](sns_files/sns_36_0.png)
    


