# Seaborn

Plotly has a lot of wow factor or whatever, but Seaborn produces the most impressive visual media I've basically ever seen in an inherently digital format.

We will use it today to produce a work of art that makes me feel roughly the way I felt the first time I saw imaging of the tiling work at the مسجد شاه. I have deliberately stolen the following image: it is "owned" by a company based in a country which sanctions the artists and artisans that maintain this tiling. I instead credit بهاء الدين محمد بن حسين العاملي, the mosque's designer.

<img src="tiling.png">

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
