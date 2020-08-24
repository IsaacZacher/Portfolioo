# Demo day 5 : Uber data


```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```


```python
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




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
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




```python
plt.hist(data.dom, bins=30, rwidth=.8, range=(0.5, 30.5))
plt.xlabel('date of the month')
plt.ylabel('frequency')
plt.title('Frequency by DoM - uber - Apr 2014')
plt.show()
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-24-63d12dc91130> in <module>
    ----> 1 plt.hist(data.dom, bins=30, rwidth=.8, range=(0.5, 30.5))
          2 plt.xlabel('date of the month')
          3 plt.ylabel('frequency')
          4 plt.title('Frequency by DoM - uber - Apr 2014')
          5 plt.show()


    /usr/local/lib/python3.6/dist-packages/pandas/core/generic.py in __getattr__(self, name)
       5128             if self._info_axis._can_hold_identifiers_and_holds_name(name):
       5129                 return self[name]
    -> 5130             return object.__getattribute__(self, name)
       5131 
       5132     def __setattr__(self, name: str, value) -> None:


    AttributeError: 'DataFrame' object has no attribute 'dom'



```python
 
def count_rows(rows):
    return len(rows)

by_date = data.groupby('dom').apply(count_rows)
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-7-dbee2be8e1df> in <module>
          2     return len(rows)
          3 
    ----> 4 by_date = data.groupby('dom').apply(count_rows)
    

    /usr/local/lib/python3.6/dist-packages/pandas/core/frame.py in groupby(self, by, axis, level, as_index, sort, group_keys, squeeze, observed, dropna)
       6512             squeeze=squeeze,
       6513             observed=observed,
    -> 6514             dropna=dropna,
       6515         )
       6516 


    /usr/local/lib/python3.6/dist-packages/pandas/core/groupby/groupby.py in __init__(self, obj, keys, axis, level, grouper, exclusions, selection, as_index, sort, group_keys, squeeze, observed, mutated, dropna)
        531                 observed=observed,
        532                 mutated=self.mutated,
    --> 533                 dropna=self.dropna,
        534             )
        535 


    /usr/local/lib/python3.6/dist-packages/pandas/core/groupby/grouper.py in get_grouper(obj, key, axis, level, sort, observed, mutated, validate, dropna)
        775                 in_axis, name, level, gpr = False, None, gpr, None
        776             else:
    --> 777                 raise KeyError(gpr)
        778         elif isinstance(gpr, Grouper) and gpr.key is not None:
        779             # Add key to exclusions


    KeyError: 'dom'



```python
plt.bar(range(1, 31), by_date)
plt.show()
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-8-0dce3db1d054> in <module>
    ----> 1 plt.bar(range(1, 31), by_date)
          2 plt.show()


    NameError: name 'by_date' is not defined



```python
by_date_sorted = by_date.sort_values()
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-9-63b4311d9988> in <module>
    ----> 1 by_date_sorted = by_date.sort_values()
    

    NameError: name 'by_date' is not defined



```python
plt.bar(range(1, 31), by_date_sorted)
plt.xticks(range(1,31), by_date_sorted.index)
plt.xlabel('date of the month')
plt.ylabel('frequency')
plt.title('Frequency by DoM - uber - Apr 2014')
plt.show()
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-10-62ea7c50c86d> in <module>
    ----> 1 plt.bar(range(1, 31), by_date_sorted)
          2 plt.xticks(range(1,31), by_date_sorted.index)
          3 plt.xlabel('date of the month')
          4 plt.ylabel('frequency')
          5 plt.title('Frequency by DoM - uber - Apr 2014')


    NameError: name 'by_date_sorted' is not defined



```python
plt.hist(data.hour, bins=24, range=(.5, 24))
plt.show()
```




![png](uber_demo_files/uber_demo_11_0.png)




```python
plt.hist(data.weekday, bins=7, range =(-.5,6.5), rwidth=.8, color='#AA6666', alpha=.4)
plt.xticks(range(7), 'Mon Tue Wed Thu Fri Sat Sun'.split())
plt.title
plt.show()

```




![png](uber_demo_files/uber_demo_12_0.png)




```python
by_cross = data.groupby('weekday hour'.split()).apply(count_rows).unstack()
by_cross.head(20)

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>hour</th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>...</th>
      <th>14</th>
      <th>15</th>
      <th>16</th>
      <th>17</th>
      <th>18</th>
      <th>19</th>
      <th>20</th>
      <th>21</th>
      <th>22</th>
      <th>23</th>
    </tr>
    <tr>
      <th>weekday</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>518</td>
      <td>261</td>
      <td>238</td>
      <td>571</td>
      <td>1021</td>
      <td>1619</td>
      <td>2974</td>
      <td>3888</td>
      <td>3138</td>
      <td>2211</td>
      <td>...</td>
      <td>3117</td>
      <td>3818</td>
      <td>4962</td>
      <td>5574</td>
      <td>4725</td>
      <td>4386</td>
      <td>3573</td>
      <td>3079</td>
      <td>1976</td>
      <td>1091</td>
    </tr>
    <tr>
      <th>1</th>
      <td>765</td>
      <td>367</td>
      <td>304</td>
      <td>516</td>
      <td>887</td>
      <td>1734</td>
      <td>3766</td>
      <td>5304</td>
      <td>4594</td>
      <td>2962</td>
      <td>...</td>
      <td>4489</td>
      <td>6042</td>
      <td>7521</td>
      <td>8297</td>
      <td>7089</td>
      <td>6459</td>
      <td>6310</td>
      <td>5993</td>
      <td>3614</td>
      <td>1948</td>
    </tr>
    <tr>
      <th>2</th>
      <td>899</td>
      <td>507</td>
      <td>371</td>
      <td>585</td>
      <td>1003</td>
      <td>1990</td>
      <td>4230</td>
      <td>5647</td>
      <td>5242</td>
      <td>3846</td>
      <td>...</td>
      <td>5438</td>
      <td>7071</td>
      <td>8213</td>
      <td>9151</td>
      <td>8334</td>
      <td>7794</td>
      <td>7783</td>
      <td>6921</td>
      <td>4845</td>
      <td>2571</td>
    </tr>
    <tr>
      <th>3</th>
      <td>792</td>
      <td>459</td>
      <td>342</td>
      <td>567</td>
      <td>861</td>
      <td>1454</td>
      <td>3179</td>
      <td>4159</td>
      <td>3616</td>
      <td>2654</td>
      <td>...</td>
      <td>4083</td>
      <td>5182</td>
      <td>6149</td>
      <td>6951</td>
      <td>6637</td>
      <td>5929</td>
      <td>6345</td>
      <td>6585</td>
      <td>5370</td>
      <td>2909</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1367</td>
      <td>760</td>
      <td>513</td>
      <td>736</td>
      <td>932</td>
      <td>1382</td>
      <td>2836</td>
      <td>3943</td>
      <td>3648</td>
      <td>2732</td>
      <td>...</td>
      <td>4087</td>
      <td>5354</td>
      <td>6259</td>
      <td>6790</td>
      <td>7258</td>
      <td>6247</td>
      <td>5165</td>
      <td>6265</td>
      <td>6708</td>
      <td>5393</td>
    </tr>
    <tr>
      <th>5</th>
      <td>3027</td>
      <td>2479</td>
      <td>1577</td>
      <td>1013</td>
      <td>706</td>
      <td>704</td>
      <td>844</td>
      <td>1110</td>
      <td>1372</td>
      <td>1764</td>
      <td>...</td>
      <td>3042</td>
      <td>4457</td>
      <td>5410</td>
      <td>5558</td>
      <td>6165</td>
      <td>5529</td>
      <td>4792</td>
      <td>5811</td>
      <td>6493</td>
      <td>5719</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4542</td>
      <td>2936</td>
      <td>1590</td>
      <td>1052</td>
      <td>685</td>
      <td>593</td>
      <td>669</td>
      <td>873</td>
      <td>1233</td>
      <td>1770</td>
      <td>...</td>
      <td>2934</td>
      <td>3400</td>
      <td>3489</td>
      <td>3154</td>
      <td>2795</td>
      <td>2579</td>
      <td>2276</td>
      <td>2310</td>
      <td>1639</td>
      <td>1018</td>
    </tr>
  </tbody>
</table>
<p>7 rows × 24 columns</p>
</div>




```python
sns.heatmap(by_cross)
plt.show()
plt.savefig('heatmap.png')
```




![png](uber_demo_files/uber_demo_14_0.png)






    <Figure size 864x504 with 0 Axes>




```python
plt.hist(data['Lat'], bins=100, range = (40.5, 41))
plt.show()
```




![png](uber_demo_files/uber_demo_15_0.png)




```python
plt.hist(data['Lon'], bins=100, range = (-74.1, -73.9))
plt.show()
```




![png](uber_demo_files/uber_demo_16_0.png)




```python
plt.hist(data['Lon'], bins=100, range = (-74.1, -73.9), color='g', alpha=.5, label = 'longitude')
plt.grid()
plt.legend(loc='upper left')
plt.twiny()
plt.hist(data['Lat'], bins=100, range = (40.5, 41), color='r', alpha=.5, label = 'latitude')
plt.legend(loc='best')
plt.show()
```




![png](uber_demo_files/uber_demo_17_0.png)




```python
plt.figure(figsize=(20, 20))
plt.plot(data['Lon'], data['Lat'], '.', ms=1, alpha=.5)
plt.xlim(-74.2, -73.7)
plt.ylim(40.7, 41)
plt.ylabel('')
plt.show()
```




![png](uber_demo_files/uber_demo_18_0.png)




```python

```


```python

```
