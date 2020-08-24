<a href="https://IsaacZacher.github.io/Portfolio/">Home</a>

# DataFrame Manipultations 
---

## Open Multiple Files and Load into One DataFrmae
--- 
```python
# Open 'spid...' folders, read in subjects' data.txt files into one list, concatenate list into one DataFrame; data
data = pd.concat([pd.read_csv(f, sep='\t') for f in sorted(glob('**/*data.txt'))], ignore_index=True)
```
>> *code develped with Arlene Jiang*
## Create DataFrame with Panadas DateTime Objects 
```python
import pandas as pd

data = pd.read_csv('uber-raw-data-apr14.csv',)
```


```python
data['Date/Time'] = data['Date/Time'].map(pd.to_datetime)
```


```python
def get_dom(dt):
    return dt.day

data['DOM'] = data['Date/Time'].map(get_dom)

def get_weekday(dt):
    return dt.weekday()

data['weekday'] = data['Date/Time'].map(get_weekday)

def get_hour(dt):
    return dt.hour

data['hour'] = data['Date/Time'].map(get_hour)

```


```python
data.tail()

```





<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date/Time</th>
      <th>Lat</th>
      <th>Lon</th>
      <th>Base</th>
      <th>DOM</th>
      <th>weekday</th>
      <th>hour</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>564511</th>
      <td>2014-04-30 23:22:00</td>
      <td>40.7640</td>
      <td>-73.9744</td>
      <td>B02764</td>
      <td>30</td>
      <td>2</td>
      <td>23</td>
    </tr>
    <tr>
      <th>564512</th>
      <td>2014-04-30 23:26:00</td>
      <td>40.7629</td>
      <td>-73.9672</td>
      <td>B02764</td>
      <td>30</td>
      <td>2</td>
      <td>23</td>
    </tr>
    <tr>
      <th>564513</th>
      <td>2014-04-30 23:31:00</td>
      <td>40.7443</td>
      <td>-73.9889</td>
      <td>B02764</td>
      <td>30</td>
      <td>2</td>
      <td>23</td>
    </tr>
    <tr>
      <th>564514</th>
      <td>2014-04-30 23:32:00</td>
      <td>40.6756</td>
      <td>-73.9405</td>
      <td>B02764</td>
      <td>30</td>
      <td>2</td>
      <td>23</td>
    </tr>
    <tr>
      <th>564515</th>
      <td>2014-04-30 23:48:00</td>
      <td>40.6880</td>
      <td>-73.9608</td>
      <td>B02764</td>
      <td>30</td>
      <td>2</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>
