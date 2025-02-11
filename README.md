<img src="https://github.com/Ben-Drucker/psankey-modified/blob/master/pSankey.png" width="100">


# psankey - A module for plotting Sankey flow diagrams in Python

Inspired by **d3-sankey** package for d3js (https://github.com/d3/d3-sankey)

## Brief description

In data science, we often require to visualize flows in the form of a Sankey diagram. This module helps with that. Usage is very straightforward and customizable.

**Note:** Does not work for cyclical graphs.

## Getting started

### Installation

Directly from the source - clone this repo on local machine, open the shell, navigate to this directory and run:
```
python setup.py install
```
or through pip:
```
pip install psankey
```

### Documentation

#### Input Data Format

A dataframe of links with the following columns (first 3 required, rest optional):

**source:**  name of source node<br/>
**target:**  name of target node<br/>
**value:**   value (width or breadth) of the link<br/>
**color:**   _optional_. color of the link<br/>
**alpha:**   _optional_. alpha (opaqueness) of the link

Example:

Input:<br/>
```
data1.csv

source,target,value,color,alpha
B,E,20,,
C,E,20,,
C,D,20,,
B,A,20,,
E,D,20,,
E,A,20,,
D,A,40,orange,0.85
```
Output:<br/>
<img src="https://github.com/Ben-Drucker/psankey-modified/blob/master/output/sankey1.png" width="1000">

#### Usage

```python
from psankey.sankey import sankey
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv('data/data1.csv')
mod = {'D': dict(facecolor='green', edgecolor='black', alpha=1, label='D1', yPush=1)}
nodes, fig, ax = sankey(df, aspect_ratio=4/3, nodelabels=True, linklabels=True, labelsize=5, nodecmap='copper', nodecolorby='level', nodealpha=0.5, nodeedgecolor='white', nodemodifier=mod)
plt.show()
```

#### Parameters

**df:** _pandas dataframe_. DataFrame with the links. Required columns: source, target, value. Optional columns: color, alpha.

**aspect_ratio:** _float, default: 4/3_. Aspect ratio of the figure.

**nodelabels:** _boolean, default: True_. Whether node labels should be plotted.

**linklabels:** _boolean, default: True_. Whether link labels should be plotted.

**labelsize:** _int, default: 5_. Font size of the labels.

**nodecolorby:** _deafult:level_. Possible values:\['level'|'size'|'index'|dictionary mapping each node to a value|any color e.g. 'blue'\]

**nodecmap:** _default: None_. Colormap of the nodes, required if nodecolorby=\['level'|'size'|'index'\]. To learn more: https://matplotlib.org/3.2.1/tutorials/colors/colormaps.html

**nodealpha:** _float, default=0.5_. Alpha of the nodes, between 0 (100% transparent) and 1 (0% transparent).

**nodeedgecolor:** _default: 'white'_. color of the border of the nodes.

**nodemodifier:** _optional_. To be used if a few nodes need to be formatted selectively, overriding the nodecmap, nodecolorby, nodealpha & nodeedgecolor paramaters. Parameters can be passed as a dictionary as shown in example.

### Sample Output

<img src="https://github.com/Ben-Drucker/psankey-modified/blob/master/output/sankey1.png" width="1000">

<img src="https://github.com/Ben-Drucker/psankey-modified/blob/master/output/sankey2.png" width="1000">

## Citing **pSankey**

To cite the library if you use it in scientific publications (or anywhere else, if you wish), please use the link to the GitHub repository (https://github.com/Ben-Drucker/psankey-modified). Thank you!
