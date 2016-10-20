---
layout: post
title:  "Exploring a Large Data Set"
date:   2016-10-19 20:19:28 +0100
categories: jekyll update
---


Earthquakes and Maths
--------------------------------


The US government maintains a set of live feeds of earthquake-related data from recent seismic events. You can choose to examine data from the last hour, through the last thirty days. You can choose to examine data from events that have a variety of magnitudes. For this project, we'll use a dataset that contains all seismic events over the last seven days, which have a magnitude of 1.0 or greater.

My ambition with this project is to import the data and then output (colour coded) points onto a globe giving the location and intensity of quakes! There are blogs on line which explore this already, but I am excited to add the complexity that rather than manually download the data I use Pandas to download from a url maintained by the US Goverment, so we are working with "live" data.

To follow this project go to the [USGS source](http://earthquake.usgs.gov/earthquakes/feed/v1.0/csv.php) for csv files of earthquake data and download the file "M1.0+ Earthquakes" under the "Past 7 Days" header. 

Alternatively, here is a [direct link](http://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/1.0_week.csv) to that file. This data is updated every 5 minutes!

Installation
-----------------

Before we begin we must import the Basemap package which will allow us to work on globes.

In the terminal window type
```conda install -c anaconda basemap=1.0.7```

Hit enter and then ```y``` to proceed.

Now reopen a Jupyter Notebook and we are ready to proceed. I will cummulative build up the code. Firstly, we import packages and ask that outputs are displayed inline. 


```python
%matplotlib inline
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
```

Next we draw a basic map centred on North America, complete with lines of latitude and longitude.


```python
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
 
# make sure the value of resolution is a lowercase L,
#  for 'low', not a numeral 1
my_map = Basemap(projection='ortho', lat_0=50, lon_0=-100,
              resolution='l', area_thresh=1000.0)
 
my_map.drawcoastlines()
my_map.drawcountries()
my_map.fillcontinents(color='coral')
my_map.drawmapboundary()
 
my_map.drawmeridians(np.arange(0, 360, 30))
my_map.drawparallels(np.arange(-90, 90, 30))
 
plt.show()
```


![png](/assets/output_4_0.png)


Now we fill in the oceans and lakes and change the focus to the UK.


```python
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
 
my_map = Basemap(projection='ortho', lat_0=50, lon_0=0,
              resolution='l', area_thresh=1000.0)
 
my_map.drawcoastlines()
my_map.drawcountries()
my_map.fillcontinents(color='coral',lake_color='aqua')
my_map.drawmapboundary(fill_color='aqua')
 
my_map.drawmeridians(np.arange(0, 360, 30))
my_map.drawparallels(np.arange(-90, 90, 30))
 
plt.show()
```


![png](/assets/output_6_0.png)


I now experiment with different projections, changing '''ortho''' to '''robin''', '''hammer''', and '''vandg'''.


```python
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
 
my_map = Basemap(projection='robin', lat_0=50, lon_0=0,
              resolution='l', area_thresh=1000.0)
 
my_map.drawcoastlines()
my_map.drawcountries()
my_map.fillcontinents(color='coral',lake_color='aqua')
my_map.drawmapboundary(fill_color='aqua')
 
my_map.drawmeridians(np.arange(0, 360, 30))
my_map.drawparallels(np.arange(-90, 90, 30))
 
plt.show()
```


![png](/assets/output_8_0.png)



```python
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
 
my_map = Basemap(projection='hammer', lat_0=50, lon_0=0,
              resolution='l', area_thresh=1000.0)
 
my_map.drawcoastlines()
my_map.drawcountries()
my_map.fillcontinents(color='coral',lake_color='aqua')
my_map.drawmapboundary(fill_color='aqua')
 
my_map.drawmeridians(np.arange(0, 360, 30))
my_map.drawparallels(np.arange(-90, 90, 30))
 
plt.show()
```


![png](/assets/output_9_0.png)



```python
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
 
my_map = Basemap(projection='vandg', lat_0=50, lon_0=0,
              resolution='l', area_thresh=1000.0)
 
my_map.drawcoastlines()
my_map.drawcountries()
my_map.fillcontinents(color='coral',lake_color='aqua')
my_map.drawmapboundary(fill_color='aqua')
 
my_map.drawmeridians(np.arange(0, 360, 30))
my_map.drawparallels(np.arange(-90, 90, 30))
 
plt.show()
```


![png](/assets/output_10_0.png)


Next I zoom on a specific area by giving the coordinates of the bottom left and top right point I'm interested in.


```python
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
 
my_map = Basemap(projection='merc', lat_0=50, lon_0=0,
              resolution='l', area_thresh=1000.0, 
                 llcrnrlon=-136.25, llcrnrlat=56,
    urcrnrlon=-134.25, urcrnrlat=57.75)
 
my_map.drawcoastlines()
my_map.drawcountries()
my_map.fillcontinents(color='coral',lake_color='aqua')
my_map.drawmapboundary(fill_color='aqua')
 
my_map.drawmeridians(np.arange(0, 360, 30))
my_map.drawparallels(np.arange(-90, 90, 30))
 
plt.show()
```


![png](/assets/output_12_0.png)


I now turn the resolution to high ('h'), and make small island appear by reducing the cut off area from 1000 to 0.1 km^2.


```python
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
 
my_map = Basemap(projection='merc', lat_0=50, lon_0=0,
              resolution='h', area_thresh=0.1, 
                 llcrnrlon=-136.25, llcrnrlat=56,
    urcrnrlon=-134.25, urcrnrlat=57.75)
 
my_map.drawcoastlines()
my_map.drawcountries()
my_map.fillcontinents(color='coral',lake_color='aqua')
my_map.drawmapboundary(fill_color='aqua')
 
my_map.drawmeridians(np.arange(0, 360, 30))
my_map.drawparallels(np.arange(-90, 90, 30))
 
plt.show()
```


![png](/assets/output_144_0.png)


I now illusatrate how to add a point on the map by manually giving coordinates.


```python
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
 
my_map = Basemap(projection='merc', lat_0=50, lon_0=0,
              resolution='h', area_thresh=0.1, 
                 llcrnrlon=-136.25, llcrnrlat=56,
    urcrnrlon=-134.25, urcrnrlat=57.75)
 
my_map.drawcoastlines()
my_map.drawcountries()
my_map.fillcontinents(color='coral',lake_color='aqua')
my_map.drawmapboundary(fill_color='aqua')
 
my_map.drawmeridians(np.arange(0, 360, 30))
my_map.drawparallels(np.arange(-90, 90, 30))

lon = -135.3318
lat = 57.0799
x,y = my_map(lon, lat)
my_map.plot(x, y, 'bo', markersize=12)

plt.show()
```


![png](/assets/output_16_0.png)


I can add more points and add labels.


```python
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
 
my_map = Basemap(projection='merc', lat_0=50, lon_0=0,
              resolution='h', area_thresh=0.1, 
                 llcrnrlon=-136.25, llcrnrlat=56,
    urcrnrlon=-134.25, urcrnrlat=57.75)
 
my_map.drawcoastlines()
my_map.drawcountries()
my_map.fillcontinents(color='coral',lake_color='aqua')
my_map.drawmapboundary(fill_color='aqua')
 
my_map.drawmeridians(np.arange(0, 360, 30))
my_map.drawparallels(np.arange(-90, 90, 30))

lons = [-135.3318, -134.8331, -134.6572]
lats = [57.0799, 57.0894, 56.2399]
x,y = my_map(lons, lats)
my_map.plot(x, y, 'bo', markersize=10)
 
labels = ['Sitka', 'Baranof Warm Springs', 'Port Alexander']
for label, xpt, ypt in zip(labels, x, y):
    plt.text(xpt, ypt, label)

plt.show()
```


![png](/assets/output_18_0.png)


The real power of this script is that using Pandas I can import from the URL and get "live" data and pick out the columns I need.


```python
import csv
from pandas import Series, DataFrame
import pandas as pd

data = pd.read_csv('http://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/1.0_week.csv')
reader = DataFrame(data,columns = ['latitude','longitude','mag'])
```

It is now easy to convert these DataFrames into lists.


```python
lats, lons, magnitudes = [], [], []

lats = reader["latitude"].tolist()
lons = reader["longitude"].tolist()
magnitudess = reader["mag"].tolist()
```


```python
# Display the first 5 lats, lons, and mags.
print 'lats', lats[0:5]
print 'lons', lons[0:5]
print 'magnitudes', magnitudes[0:5]
```

    lats [33.975999999999999, 63.4773, 62.212899999999998, 32.5833333, -9.0645000000000007]
    lons [-117.76100000000001, -154.9709, -145.61279999999999, -116.98883329999998, 123.9038]
    magnitudes []


Once I have the coordinates as lists it easy to plot the points where eartquakes took place (as above). 


```python
# --- Build Map ---
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
 
eq_map = Basemap(projection='robin', resolution = 'l', area_thresh = 1000.0,
              lat_0=0, lon_0=-130)
eq_map.drawcoastlines()
eq_map.drawcountries()
eq_map.fillcontinents(color = 'gray')
eq_map.drawmapboundary()
eq_map.drawmeridians(np.arange(0, 360, 30))
eq_map.drawparallels(np.arange(-90, 90, 30))
 
x,y = eq_map(lons, lats)
eq_map.plot(x, y, 'ro', markersize=6)
 
plt.show()
```


![png](/assets/output_25_0.png)


I now consolidate the code into a single cell, and look at scaling the diameter of the plot according to the magnitude of the quake.


```python
import csv
from pandas import Series, DataFrame
import pandas as pd

data = pd.read_csv('http://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/1.0_week.csv')
reader = DataFrame(data,columns = ['latitude','longitude','mag'])

lats, lons, mags = [], [], []

lats = reader["latitude"].tolist()
lons = reader["longitude"].tolist()
magnitudes = reader["mag"].tolist()
        
# --- Build Map ---
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np
 
eq_map = Basemap(projection='robin', resolution = 'l', area_thresh = 1000.0,
              lat_0=0, lon_0=-130)
eq_map.drawcoastlines()
eq_map.drawcountries()
eq_map.fillcontinents(color = 'gray')
eq_map.drawmapboundary()
eq_map.drawmeridians(np.arange(0, 360, 30))
eq_map.drawparallels(np.arange(-90, 90, 30))
 
min_marker_size = 2.5
for lon, lat, mag in zip(lons, lats, magnitudes):
    x,y = eq_map(lon, lat)
    msize = mag * min_marker_size
    eq_map.plot(x, y, 'ro', markersize=msize)
 
plt.show()
```


![png](/assets/output_27_0.png)


To aid data visualization further I colour code the quakes.


```python
import csv
from pandas import Series, DataFrame
import pandas as pd

data = pd.read_csv('http://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/1.0_week.csv')
reader = DataFrame(data,columns = ['latitude','longitude','mag'])

lats, lons, mags = [], [], []

lats = reader["latitude"].tolist()
lons = reader["longitude"].tolist()
magnitudes = reader["mag"].tolist()
        
# --- Build Map ---
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np

def get_marker_color(magnitude):
    # Returns green for small earthquakes, yellow for moderate
    #  earthquakes, and red for significant earthquakes.
    if magnitude < 3.0:
        return ('go')
    elif magnitude < 5.0:
        return ('yo')
    else:
        return ('ro')
 
eq_map = Basemap(projection='robin', resolution = 'l', area_thresh = 1000.0,
              lat_0=0, lon_0=-130)
eq_map.drawcoastlines()
eq_map.drawcountries()
eq_map.fillcontinents(color = 'gray')
eq_map.drawmapboundary()
eq_map.drawmeridians(np.arange(0, 360, 30))
eq_map.drawparallels(np.arange(-90, 90, 30))
 
min_marker_size = 2.5
for lon, lat, mag in zip(lons, lats, magnitudes):
    x,y = eq_map(lon, lat)
    msize = mag * min_marker_size
    marker_string = get_marker_color(mag)
    eq_map.plot(x, y, marker_string, markersize=msize)
 
plt.show()
```


![png](/assets/output_29_0.png)


Finally, I add a title and then use Nasa's data to colour the globe ('''eq_map.bluemarble()''').


```python
import csv
from pandas import Series, DataFrame
import pandas as pd

data = pd.read_csv('http://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/1.0_week.csv')
reader = DataFrame(data,columns = ['latitude','longitude','mag'])

lats, lons, mags = [], [], []

lats = reader["latitude"].tolist()
lons = reader["longitude"].tolist()
magnitudes = reader["mag"].tolist()
        
# --- Build Map ---
from mpl_toolkits.basemap import Basemap
import matplotlib.pyplot as plt
import numpy as np

def get_marker_color(magnitude):
    # Returns green for small earthquakes, yellow for moderate
    #  earthquakes, and red for significant earthquakes.
    if magnitude < 3.0:
        return ('go')
    elif magnitude < 5.0:
        return ('yo')
    else:
        return ('ro')
 
eq_map = Basemap(projection='robin', resolution = 'l', area_thresh = 1000.0,
              lat_0=0, lon_0=-130)
eq_map.drawcoastlines()
eq_map.drawcountries()
eq_map.bluemarble()
eq_map.drawmapboundary()
eq_map.drawmeridians(np.arange(0, 360, 30))
eq_map.drawparallels(np.arange(-90, 90, 30))
 
min_marker_size = 2.25
for lon, lat, mag in zip(lons, lats, magnitudes):
    x,y = eq_map(lon, lat)
    msize = mag * min_marker_size
    marker_string = get_marker_color(mag)
    eq_map.plot(x, y, marker_string, markersize=msize)
    
title_string = "Earthquakes of Magnitude 1.0 or Greater\n"
plt.title(title_string)
 
plt.show()
```


![png](/assets/output_31_0.png)


Lots of beautiful examples of different ways to present data on these maps are given [here](http://matplotlib.org/basemap/users/examples.html).
