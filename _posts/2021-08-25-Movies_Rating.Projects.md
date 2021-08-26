---
layout: post
title: "Movies Rating"
subtitle: "Rating"
background: '/img/Movies_Rating.Projects/Movies.png'
---



```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
# load data & str of the dataframe
fandango = pd.read_csv("fandango_scrape.csv")
fandango.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 504 entries, 0 to 503
    Data columns (total 4 columns):
     #   Column  Non-Null Count  Dtype  
    ---  ------  --------------  -----  
     0   FILM    504 non-null    object 
     1   STARS   504 non-null    float64
     2   RATING  504 non-null    float64
     3   VOTES   504 non-null    int64  
    dtypes: float64(2), int64(1), object(1)
    memory usage: 13.8+ KB
    


```python
#first 5 row
fandango.head()
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
      <th>FILM</th>
      <th>STARS</th>
      <th>RATING</th>
      <th>VOTES</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fifty Shades of Grey (2015)</td>
      <td>4.0</td>
      <td>3.9</td>
      <td>34846</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jurassic World (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>34390</td>
    </tr>
    <tr>
      <th>2</th>
      <td>American Sniper (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>34085</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Furious 7 (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>33538</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Inside Out (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>15749</td>
    </tr>
  </tbody>
</table>
</div>




```python
#describe of dataframe 
fandango.describe()
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
      <th>STARS</th>
      <th>RATING</th>
      <th>VOTES</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>504.000000</td>
      <td>504.000000</td>
      <td>504.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>3.558532</td>
      <td>3.375794</td>
      <td>1147.863095</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.563133</td>
      <td>1.491223</td>
      <td>3830.583136</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>3.500000</td>
      <td>3.100000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>4.000000</td>
      <td>3.800000</td>
      <td>18.500000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>4.500000</td>
      <td>4.300000</td>
      <td>189.750000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>34846.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#scatterplot for Votes vs Rating
plt.figure(figsize=(15,8))
sns.scatterplot(data = fandango, x= 'RATING', y = 'VOTES',s=100)
```




    <AxesSubplot:xlabel='RATING', ylabel='VOTES'>




    
![png](/img/Movies_Rating.Projects/output_4_1.png)
    



```python
#corr among all columns 
fandango.corr()
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
      <th>STARS</th>
      <th>RATING</th>
      <th>VOTES</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>STARS</th>
      <td>1.000000</td>
      <td>0.994696</td>
      <td>0.164218</td>
    </tr>
    <tr>
      <th>RATING</th>
      <td>0.994696</td>
      <td>1.000000</td>
      <td>0.163764</td>
    </tr>
    <tr>
      <th>VOTES</th>
      <td>0.164218</td>
      <td>0.163764</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#strip 2015 from Film column and create new columns Year
fandango['YEAR'] = fandango['FILM'].map(lambda x: str(x)[-5:-1])
```


```python
fandango['YEAR']
```




    0      2015
    1      2015
    2      2015
    3      2015
    4      2015
           ... 
    499    2015
    500    2015
    501    2015
    502    1964
    503    2012
    Name: YEAR, Length: 504, dtype: object




```python
fandango.head()
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
      <th>FILM</th>
      <th>STARS</th>
      <th>RATING</th>
      <th>VOTES</th>
      <th>YEAR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fifty Shades of Grey (2015)</td>
      <td>4.0</td>
      <td>3.9</td>
      <td>34846</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jurassic World (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>34390</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>2</th>
      <td>American Sniper (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>34085</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Furious 7 (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>33538</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Inside Out (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>15749</td>
      <td>2015</td>
    </tr>
  </tbody>
</table>
</div>




```python
#assign fadango dataframe to df 
df = fandango
```


```python
#count YEAR column
df['YEAR'].value_counts()
```




    2015    478
    2014     23
    2012      1
    1964      1
    2016      1
    Name: YEAR, dtype: int64




```python
df.nlargest(10, 'VOTES' )
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
      <th>FILM</th>
      <th>STARS</th>
      <th>RATING</th>
      <th>VOTES</th>
      <th>YEAR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fifty Shades of Grey (2015)</td>
      <td>4.0</td>
      <td>3.9</td>
      <td>34846</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jurassic World (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>34390</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>2</th>
      <td>American Sniper (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>34085</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Furious 7 (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>33538</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Inside Out (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>15749</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>5</th>
      <td>The Hobbit: The Battle of the Five Armies (2014)</td>
      <td>4.5</td>
      <td>4.3</td>
      <td>15337</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Kingsman: The Secret Service (2015)</td>
      <td>4.5</td>
      <td>4.2</td>
      <td>15205</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Minions (2015)</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>14998</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Avengers: Age of Ultron (2015)</td>
      <td>5.0</td>
      <td>4.5</td>
      <td>14846</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Into the Woods (2014)</td>
      <td>3.5</td>
      <td>3.4</td>
      <td>13055</td>
      <td>2014</td>
    </tr>
  </tbody>
</table>
</div>




```python
#sum zeor votes
zero_votes = df['VOTES'] == 0 
zero_votes.sum()
```




    69




```python
#Create new dataframe be removing all zeor votes
df= df[df['VOTES'] != 0]

```


```python
#chaeck if there any 0
zero_votes = df['VOTES'] == 0 
zero_votes.sum()
```




    0




```python
#creating new column to see the difference between RATING vs STARTS 
df['STARS_DIFF'] = df['STARS']- df['RATING']

```

    <ipython-input-21-61797a8b36e4>:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      df['STARS_DIFF'] = df['STARS']- df['RATING']
    


```python
#round STARS_DIFF to 2 Decimals
decimals = 2    
df['STARS_DIFF'] = df['STARS_DIFF'].apply(lambda x: round(x, decimals))
```

    <ipython-input-22-4bc51af00b3a>:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      df['STARS_DIFF'] = df['STARS_DIFF'].apply(lambda x: round(x, decimals))
    


```python
df
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
      <th>FILM</th>
      <th>STARS</th>
      <th>RATING</th>
      <th>VOTES</th>
      <th>YEAR</th>
      <th>STARS_DIFF</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fifty Shades of Grey (2015)</td>
      <td>4.0</td>
      <td>3.9</td>
      <td>34846</td>
      <td>2015</td>
      <td>0.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jurassic World (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>34390</td>
      <td>2015</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>American Sniper (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>34085</td>
      <td>2015</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Furious 7 (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>33538</td>
      <td>2015</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Inside Out (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>15749</td>
      <td>2015</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>430</th>
      <td>That Sugar Film (2015)</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1</td>
      <td>2015</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>431</th>
      <td>The Intern (2015)</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1</td>
      <td>2015</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>432</th>
      <td>The Park Bench (2015)</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1</td>
      <td>2015</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>433</th>
      <td>The Wanted 18 (2015)</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1</td>
      <td>2015</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>434</th>
      <td>Z For Zachariah (2015)</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>1</td>
      <td>2015</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>435 rows × 6 columns</p>
</div>




```python
#grap STARS_DIFF equls to 1.0
df1 = df.loc[df['STARS_DIFF'] == 1.0]

```


```python
df1
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
      <th>FILM</th>
      <th>STARS</th>
      <th>RATING</th>
      <th>VOTES</th>
      <th>YEAR</th>
      <th>STARS_DIFF</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>381</th>
      <td>Turbo Kid (2015)</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>2</td>
      <td>2015</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#comparing the scores from Fandango to other movies sites and see how they compare
#load data
df_all = pd.read_csv("all_sites_scores.csv")
df_all.head()
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
      <th>FILM</th>
      <th>RottenTomatoes</th>
      <th>RottenTomatoes_User</th>
      <th>Metacritic</th>
      <th>Metacritic_User</th>
      <th>IMDB</th>
      <th>Metacritic_user_vote_count</th>
      <th>IMDB_user_vote_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Avengers: Age of Ultron (2015)</td>
      <td>74</td>
      <td>86</td>
      <td>66</td>
      <td>7.1</td>
      <td>7.8</td>
      <td>1330</td>
      <td>271107</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cinderella (2015)</td>
      <td>85</td>
      <td>80</td>
      <td>67</td>
      <td>7.5</td>
      <td>7.1</td>
      <td>249</td>
      <td>65709</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ant-Man (2015)</td>
      <td>80</td>
      <td>90</td>
      <td>64</td>
      <td>8.1</td>
      <td>7.8</td>
      <td>627</td>
      <td>103660</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Do You Believe? (2015)</td>
      <td>18</td>
      <td>84</td>
      <td>22</td>
      <td>4.7</td>
      <td>5.4</td>
      <td>31</td>
      <td>3136</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hot Tub Time Machine 2 (2015)</td>
      <td>14</td>
      <td>28</td>
      <td>29</td>
      <td>3.4</td>
      <td>5.1</td>
      <td>88</td>
      <td>19560</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_all.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 146 entries, 0 to 145
    Data columns (total 8 columns):
     #   Column                      Non-Null Count  Dtype  
    ---  ------                      --------------  -----  
     0   FILM                        146 non-null    object 
     1   RottenTomatoes              146 non-null    int64  
     2   RottenTomatoes_User         146 non-null    int64  
     3   Metacritic                  146 non-null    int64  
     4   Metacritic_User             146 non-null    float64
     5   IMDB                        146 non-null    float64
     6   Metacritic_user_vote_count  146 non-null    int64  
     7   IMDB_user_vote_count        146 non-null    int64  
    dtypes: float64(2), int64(5), object(1)
    memory usage: 8.6+ KB
    


```python
df_all.describe()
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
      <th>RottenTomatoes</th>
      <th>RottenTomatoes_User</th>
      <th>Metacritic</th>
      <th>Metacritic_User</th>
      <th>IMDB</th>
      <th>Metacritic_user_vote_count</th>
      <th>IMDB_user_vote_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>146.000000</td>
      <td>146.000000</td>
      <td>146.000000</td>
      <td>146.000000</td>
      <td>146.000000</td>
      <td>146.000000</td>
      <td>146.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>60.849315</td>
      <td>63.876712</td>
      <td>58.808219</td>
      <td>6.519178</td>
      <td>6.736986</td>
      <td>185.705479</td>
      <td>42846.205479</td>
    </tr>
    <tr>
      <th>std</th>
      <td>30.168799</td>
      <td>20.024430</td>
      <td>19.517389</td>
      <td>1.510712</td>
      <td>0.958736</td>
      <td>316.606515</td>
      <td>67406.509171</td>
    </tr>
    <tr>
      <th>min</th>
      <td>5.000000</td>
      <td>20.000000</td>
      <td>13.000000</td>
      <td>2.400000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>243.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>31.250000</td>
      <td>50.000000</td>
      <td>43.500000</td>
      <td>5.700000</td>
      <td>6.300000</td>
      <td>33.250000</td>
      <td>5627.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>63.500000</td>
      <td>66.500000</td>
      <td>59.000000</td>
      <td>6.850000</td>
      <td>6.900000</td>
      <td>72.500000</td>
      <td>19103.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>89.000000</td>
      <td>81.000000</td>
      <td>75.000000</td>
      <td>7.500000</td>
      <td>7.400000</td>
      <td>168.500000</td>
      <td>45185.750000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>100.000000</td>
      <td>94.000000</td>
      <td>94.000000</td>
      <td>9.600000</td>
      <td>8.600000</td>
      <td>2375.000000</td>
      <td>334164.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#creating new column to see the difference between RottenTomatoes_User & RottenTomatoes 
df_all['Score_Diff'] = df_all['RottenTomatoes']- df_all['RottenTomatoes_User']
df_all
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
      <th>FILM</th>
      <th>RottenTomatoes</th>
      <th>RottenTomatoes_User</th>
      <th>Metacritic</th>
      <th>Metacritic_User</th>
      <th>IMDB</th>
      <th>Metacritic_user_vote_count</th>
      <th>IMDB_user_vote_count</th>
      <th>Score_Diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Avengers: Age of Ultron (2015)</td>
      <td>74</td>
      <td>86</td>
      <td>66</td>
      <td>7.1</td>
      <td>7.8</td>
      <td>1330</td>
      <td>271107</td>
      <td>-12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cinderella (2015)</td>
      <td>85</td>
      <td>80</td>
      <td>67</td>
      <td>7.5</td>
      <td>7.1</td>
      <td>249</td>
      <td>65709</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ant-Man (2015)</td>
      <td>80</td>
      <td>90</td>
      <td>64</td>
      <td>8.1</td>
      <td>7.8</td>
      <td>627</td>
      <td>103660</td>
      <td>-10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Do You Believe? (2015)</td>
      <td>18</td>
      <td>84</td>
      <td>22</td>
      <td>4.7</td>
      <td>5.4</td>
      <td>31</td>
      <td>3136</td>
      <td>-66</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hot Tub Time Machine 2 (2015)</td>
      <td>14</td>
      <td>28</td>
      <td>29</td>
      <td>3.4</td>
      <td>5.1</td>
      <td>88</td>
      <td>19560</td>
      <td>-14</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>141</th>
      <td>Mr. Holmes (2015)</td>
      <td>87</td>
      <td>78</td>
      <td>67</td>
      <td>7.9</td>
      <td>7.4</td>
      <td>33</td>
      <td>7367</td>
      <td>9</td>
    </tr>
    <tr>
      <th>142</th>
      <td>'71 (2015)</td>
      <td>97</td>
      <td>82</td>
      <td>83</td>
      <td>7.5</td>
      <td>7.2</td>
      <td>60</td>
      <td>24116</td>
      <td>15</td>
    </tr>
    <tr>
      <th>143</th>
      <td>Two Days, One Night (2014)</td>
      <td>97</td>
      <td>78</td>
      <td>89</td>
      <td>8.8</td>
      <td>7.4</td>
      <td>123</td>
      <td>24345</td>
      <td>19</td>
    </tr>
    <tr>
      <th>144</th>
      <td>Gett: The Trial of Viviane Amsalem (2015)</td>
      <td>100</td>
      <td>81</td>
      <td>90</td>
      <td>7.3</td>
      <td>7.8</td>
      <td>19</td>
      <td>1955</td>
      <td>19</td>
    </tr>
    <tr>
      <th>145</th>
      <td>Kumiko, The Treasure Hunter (2015)</td>
      <td>87</td>
      <td>63</td>
      <td>68</td>
      <td>6.4</td>
      <td>6.7</td>
      <td>19</td>
      <td>5289</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
<p>146 rows × 9 columns</p>
</div>




```python
#absolute value of Score_Diff
df_all['Score_Diff'].apply(abs).mean()
```




    15.095890410958905




```python
#showing the smallest Score_Diff for movies
print('Critics love, but Users Hate')
df_all.nsmallest(5, 'Score_Diff')[['FILM', 'Score_Diff']]
```

    Critics love, but Users Hate
    




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
      <th>FILM</th>
      <th>Score_Diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Do You Believe? (2015)</td>
      <td>-66</td>
    </tr>
    <tr>
      <th>85</th>
      <td>Little Boy (2015)</td>
      <td>-61</td>
    </tr>
    <tr>
      <th>105</th>
      <td>Hitman: Agent 47 (2015)</td>
      <td>-42</td>
    </tr>
    <tr>
      <th>134</th>
      <td>The Longest Ride (2015)</td>
      <td>-42</td>
    </tr>
    <tr>
      <th>125</th>
      <td>The Wedding Ringer (2015)</td>
      <td>-39</td>
    </tr>
  </tbody>
</table>
</div>




```python
#showing the largest Score_Diff for movies
print("Users Love but Critics Hate")
df_all.nlargest(5, 'Score_Diff')[['FILM', 'Score_Diff']]
```

    Users Love but Critics Hate
    




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
      <th>FILM</th>
      <th>Score_Diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>69</th>
      <td>Mr. Turner (2014)</td>
      <td>42</td>
    </tr>
    <tr>
      <th>112</th>
      <td>It Follows (2015)</td>
      <td>31</td>
    </tr>
    <tr>
      <th>115</th>
      <td>While We're Young (2015)</td>
      <td>31</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Welcome to Me (2015)</td>
      <td>24</td>
    </tr>
    <tr>
      <th>40</th>
      <td>I'll See You In My Dreams (2015)</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
</div>




```python
## MetaCritic
#we are going to look at MetaCritic rating
```


```python
#IMDB
#we are going to look at IMDB rating
```


```python
# two outliers here in the last plot, the movie with the highest vote count on IMDB only has about 500 Metacritic ratings
# movie with the highest IMDB user vote count
df_all.nlargest(1, 'IMDB_user_vote_count')
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
      <th>FILM</th>
      <th>RottenTomatoes</th>
      <th>RottenTomatoes_User</th>
      <th>Metacritic</th>
      <th>Metacritic_User</th>
      <th>IMDB</th>
      <th>Metacritic_user_vote_count</th>
      <th>IMDB_user_vote_count</th>
      <th>Score_Diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>14</th>
      <td>The Imitation Game (2014)</td>
      <td>90</td>
      <td>92</td>
      <td>73</td>
      <td>8.2</td>
      <td>8.1</td>
      <td>566</td>
      <td>334164</td>
      <td>-2</td>
    </tr>
  </tbody>
</table>
</div>




```python
#movie with the highest Metacritic User Vote coun
df_all.nlargest(1, 'Metacritic_user_vote_count')
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
      <th>FILM</th>
      <th>RottenTomatoes</th>
      <th>RottenTomatoes_User</th>
      <th>Metacritic</th>
      <th>Metacritic_User</th>
      <th>IMDB</th>
      <th>Metacritic_user_vote_count</th>
      <th>IMDB_user_vote_count</th>
      <th>Score_Diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>88</th>
      <td>Mad Max: Fury Road (2015)</td>
      <td>97</td>
      <td>88</td>
      <td>89</td>
      <td>8.7</td>
      <td>8.3</td>
      <td>2375</td>
      <td>292023</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
##Fandago Scores vs. All Sites
#we are going to compere between two data frames to see wethere Fandago has higher rating or not  
```


```python
#merge together both DataFrames based on the FILM columns
com_df = pd.merge(left = fandango, right = df_all, left_on = 'FILM', right_on = 'FILM' )
com_df.head()
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
      <th>FILM</th>
      <th>STARS</th>
      <th>RATING</th>
      <th>VOTES</th>
      <th>YEAR</th>
      <th>RottenTomatoes</th>
      <th>RottenTomatoes_User</th>
      <th>Metacritic</th>
      <th>Metacritic_User</th>
      <th>IMDB</th>
      <th>Metacritic_user_vote_count</th>
      <th>IMDB_user_vote_count</th>
      <th>Score_Diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fifty Shades of Grey (2015)</td>
      <td>4.0</td>
      <td>3.9</td>
      <td>34846</td>
      <td>2015</td>
      <td>25</td>
      <td>42</td>
      <td>46</td>
      <td>3.2</td>
      <td>4.2</td>
      <td>778</td>
      <td>179506</td>
      <td>-17</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jurassic World (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>34390</td>
      <td>2015</td>
      <td>71</td>
      <td>81</td>
      <td>59</td>
      <td>7.0</td>
      <td>7.3</td>
      <td>1281</td>
      <td>241807</td>
      <td>-10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>American Sniper (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>34085</td>
      <td>2015</td>
      <td>72</td>
      <td>85</td>
      <td>72</td>
      <td>6.6</td>
      <td>7.4</td>
      <td>850</td>
      <td>251856</td>
      <td>-13</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Furious 7 (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>33538</td>
      <td>2015</td>
      <td>81</td>
      <td>84</td>
      <td>67</td>
      <td>6.8</td>
      <td>7.4</td>
      <td>764</td>
      <td>207211</td>
      <td>-3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Inside Out (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>15749</td>
      <td>2015</td>
      <td>98</td>
      <td>90</td>
      <td>94</td>
      <td>8.9</td>
      <td>8.6</td>
      <td>807</td>
      <td>96252</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
com_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 145 entries, 0 to 144
    Data columns (total 13 columns):
     #   Column                      Non-Null Count  Dtype  
    ---  ------                      --------------  -----  
     0   FILM                        145 non-null    object 
     1   STARS                       145 non-null    float64
     2   RATING                      145 non-null    float64
     3   VOTES                       145 non-null    int64  
     4   YEAR                        145 non-null    object 
     5   RottenTomatoes              145 non-null    int64  
     6   RottenTomatoes_User         145 non-null    int64  
     7   Metacritic                  145 non-null    int64  
     8   Metacritic_User             145 non-null    float64
     9   IMDB                        145 non-null    float64
     10  Metacritic_user_vote_count  145 non-null    int64  
     11  IMDB_user_vote_count        145 non-null    int64  
     12  Score_Diff                  145 non-null    int64  
    dtypes: float64(4), int64(7), object(2)
    memory usage: 14.7+ KB
    


```python
com_df
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
      <th>FILM</th>
      <th>STARS</th>
      <th>RATING</th>
      <th>VOTES</th>
      <th>YEAR</th>
      <th>RottenTomatoes</th>
      <th>RottenTomatoes_User</th>
      <th>Metacritic</th>
      <th>Metacritic_User</th>
      <th>IMDB</th>
      <th>Metacritic_user_vote_count</th>
      <th>IMDB_user_vote_count</th>
      <th>Score_Diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fifty Shades of Grey (2015)</td>
      <td>4.0</td>
      <td>3.9</td>
      <td>34846</td>
      <td>2015</td>
      <td>25</td>
      <td>42</td>
      <td>46</td>
      <td>3.2</td>
      <td>4.2</td>
      <td>778</td>
      <td>179506</td>
      <td>-17</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jurassic World (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>34390</td>
      <td>2015</td>
      <td>71</td>
      <td>81</td>
      <td>59</td>
      <td>7.0</td>
      <td>7.3</td>
      <td>1281</td>
      <td>241807</td>
      <td>-10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>American Sniper (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>34085</td>
      <td>2015</td>
      <td>72</td>
      <td>85</td>
      <td>72</td>
      <td>6.6</td>
      <td>7.4</td>
      <td>850</td>
      <td>251856</td>
      <td>-13</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Furious 7 (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>33538</td>
      <td>2015</td>
      <td>81</td>
      <td>84</td>
      <td>67</td>
      <td>6.8</td>
      <td>7.4</td>
      <td>764</td>
      <td>207211</td>
      <td>-3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Inside Out (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>15749</td>
      <td>2015</td>
      <td>98</td>
      <td>90</td>
      <td>94</td>
      <td>8.9</td>
      <td>8.6</td>
      <td>807</td>
      <td>96252</td>
      <td>8</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>140</th>
      <td>Kumiko, The Treasure Hunter (2015)</td>
      <td>3.5</td>
      <td>3.5</td>
      <td>41</td>
      <td>2015</td>
      <td>87</td>
      <td>63</td>
      <td>68</td>
      <td>6.4</td>
      <td>6.7</td>
      <td>19</td>
      <td>5289</td>
      <td>24</td>
    </tr>
    <tr>
      <th>141</th>
      <td>The Diary of a Teenage Girl (2015)</td>
      <td>4.0</td>
      <td>3.6</td>
      <td>38</td>
      <td>2015</td>
      <td>95</td>
      <td>81</td>
      <td>87</td>
      <td>6.3</td>
      <td>7.0</td>
      <td>18</td>
      <td>1107</td>
      <td>14</td>
    </tr>
    <tr>
      <th>142</th>
      <td>The Wrecking Crew (2015)</td>
      <td>4.5</td>
      <td>4.2</td>
      <td>38</td>
      <td>2015</td>
      <td>93</td>
      <td>84</td>
      <td>67</td>
      <td>7.0</td>
      <td>7.8</td>
      <td>4</td>
      <td>732</td>
      <td>9</td>
    </tr>
    <tr>
      <th>143</th>
      <td>Tangerine (2015)</td>
      <td>4.0</td>
      <td>3.9</td>
      <td>36</td>
      <td>2015</td>
      <td>95</td>
      <td>86</td>
      <td>86</td>
      <td>7.3</td>
      <td>7.4</td>
      <td>14</td>
      <td>696</td>
      <td>9</td>
    </tr>
    <tr>
      <th>144</th>
      <td>Maps to the Stars (2015)</td>
      <td>3.5</td>
      <td>3.1</td>
      <td>35</td>
      <td>2015</td>
      <td>60</td>
      <td>46</td>
      <td>67</td>
      <td>5.8</td>
      <td>6.3</td>
      <td>46</td>
      <td>22440</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
<p>145 rows × 13 columns</p>
</div>




```python
#normalized columns for all ratings, so they can match up 0-5 stars
com_df['RT_Norm'] = np.round(com_df['RottenTomatoes']/20,1)
com_df['RTU_Norm'] =  np.round(com_df['RottenTomatoes_User']/20,1)
com_df['Meta_Norm'] =  np.round(com_df['Metacritic']/20,1)
com_df['Meta_U_Norm'] =  np.round(com_df['Metacritic_User']/2,1)
com_df['IMDB_Norm'] = np.round(com_df['IMDB']/2,1)
```


```python
com_df.head()
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
      <th>FILM</th>
      <th>STARS</th>
      <th>RATING</th>
      <th>VOTES</th>
      <th>YEAR</th>
      <th>RottenTomatoes</th>
      <th>RottenTomatoes_User</th>
      <th>Metacritic</th>
      <th>Metacritic_User</th>
      <th>IMDB</th>
      <th>Metacritic_user_vote_count</th>
      <th>IMDB_user_vote_count</th>
      <th>Score_Diff</th>
      <th>RT_Norm</th>
      <th>RTU_Norm</th>
      <th>Meta_Norm</th>
      <th>Meta_U_Norm</th>
      <th>IMDB_Norm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fifty Shades of Grey (2015)</td>
      <td>4.0</td>
      <td>3.9</td>
      <td>34846</td>
      <td>2015</td>
      <td>25</td>
      <td>42</td>
      <td>46</td>
      <td>3.2</td>
      <td>4.2</td>
      <td>778</td>
      <td>179506</td>
      <td>-17</td>
      <td>1.2</td>
      <td>2.1</td>
      <td>2.3</td>
      <td>1.6</td>
      <td>2.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Jurassic World (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>34390</td>
      <td>2015</td>
      <td>71</td>
      <td>81</td>
      <td>59</td>
      <td>7.0</td>
      <td>7.3</td>
      <td>1281</td>
      <td>241807</td>
      <td>-10</td>
      <td>3.6</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>3.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>American Sniper (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>34085</td>
      <td>2015</td>
      <td>72</td>
      <td>85</td>
      <td>72</td>
      <td>6.6</td>
      <td>7.4</td>
      <td>850</td>
      <td>251856</td>
      <td>-13</td>
      <td>3.6</td>
      <td>4.2</td>
      <td>3.6</td>
      <td>3.3</td>
      <td>3.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Furious 7 (2015)</td>
      <td>5.0</td>
      <td>4.8</td>
      <td>33538</td>
      <td>2015</td>
      <td>81</td>
      <td>84</td>
      <td>67</td>
      <td>6.8</td>
      <td>7.4</td>
      <td>764</td>
      <td>207211</td>
      <td>-3</td>
      <td>4.0</td>
      <td>4.2</td>
      <td>3.4</td>
      <td>3.4</td>
      <td>3.7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Inside Out (2015)</td>
      <td>4.5</td>
      <td>4.5</td>
      <td>15749</td>
      <td>2015</td>
      <td>98</td>
      <td>90</td>
      <td>94</td>
      <td>8.9</td>
      <td>8.6</td>
      <td>807</td>
      <td>96252</td>
      <td>8</td>
      <td>4.9</td>
      <td>4.5</td>
      <td>4.7</td>
      <td>4.4</td>
      <td>4.3</td>
    </tr>
  </tbody>
</table>
</div>




```python
norm_scores = com_df[['STARS', 'RATING', 'RT_Norm', 'RTU_Norm', 'Meta_Norm', 'Meta_U_Norm', 'IMDB_Norm']]
norm_scores.head()
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
      <th>STARS</th>
      <th>RATING</th>
      <th>RT_Norm</th>
      <th>RTU_Norm</th>
      <th>Meta_Norm</th>
      <th>Meta_U_Norm</th>
      <th>IMDB_Norm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>4.0</td>
      <td>3.9</td>
      <td>1.2</td>
      <td>2.1</td>
      <td>2.3</td>
      <td>1.6</td>
      <td>2.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.5</td>
      <td>4.5</td>
      <td>3.6</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>3.5</td>
      <td>3.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5.0</td>
      <td>4.8</td>
      <td>3.6</td>
      <td>4.2</td>
      <td>3.6</td>
      <td>3.3</td>
      <td>3.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5.0</td>
      <td>4.8</td>
      <td>4.0</td>
      <td>4.2</td>
      <td>3.4</td>
      <td>3.4</td>
      <td>3.7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4.5</td>
      <td>4.5</td>
      <td>4.9</td>
      <td>4.5</td>
      <td>4.7</td>
      <td>4.4</td>
      <td>4.3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# fix legend Position bugg

def move_legend(ax, new_loc, **kws):
    old_legend = ax.legend_
    handles = old_legend.legendHandles
    labels = [t.get_text() for t in old_legend.get_texts()]
    title = old_legend.get_title().get_text()
    ax.legend(handles, labels, loc=new_loc, title=title, **kws)
    
```


```python
#readd FILM column to the data
score_film = com_df[['STARS', 'RATING', 'RT_Norm', 'RTU_Norm', 'Meta_Norm', 'Meta_U_Norm', 'IMDB_Norm', 'FILM']]

```


```python
worst_movies = score_film.nsmallest(10,'RT_Norm')
worst_movies
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
      <th>STARS</th>
      <th>RATING</th>
      <th>RT_Norm</th>
      <th>RTU_Norm</th>
      <th>Meta_Norm</th>
      <th>Meta_U_Norm</th>
      <th>IMDB_Norm</th>
      <th>FILM</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>49</th>
      <td>3.5</td>
      <td>3.5</td>
      <td>0.2</td>
      <td>1.8</td>
      <td>0.6</td>
      <td>1.2</td>
      <td>2.2</td>
      <td>Paul Blart: Mall Cop 2 (2015)</td>
    </tr>
    <tr>
      <th>25</th>
      <td>4.5</td>
      <td>4.1</td>
      <td>0.4</td>
      <td>2.3</td>
      <td>1.3</td>
      <td>2.3</td>
      <td>3.0</td>
      <td>Taken 3 (2015)</td>
    </tr>
    <tr>
      <th>28</th>
      <td>3.0</td>
      <td>2.7</td>
      <td>0.4</td>
      <td>1.0</td>
      <td>1.4</td>
      <td>1.2</td>
      <td>2.0</td>
      <td>Fantastic Four (2015)</td>
    </tr>
    <tr>
      <th>54</th>
      <td>4.0</td>
      <td>3.7</td>
      <td>0.4</td>
      <td>1.8</td>
      <td>1.6</td>
      <td>1.8</td>
      <td>2.4</td>
      <td>Hot Pursuit (2015)</td>
    </tr>
    <tr>
      <th>84</th>
      <td>4.0</td>
      <td>3.9</td>
      <td>0.4</td>
      <td>2.4</td>
      <td>1.4</td>
      <td>1.6</td>
      <td>3.0</td>
      <td>Hitman: Agent 47 (2015)</td>
    </tr>
    <tr>
      <th>50</th>
      <td>4.0</td>
      <td>3.6</td>
      <td>0.5</td>
      <td>1.8</td>
      <td>1.5</td>
      <td>2.8</td>
      <td>2.3</td>
      <td>The Boy Next Door (2015)</td>
    </tr>
    <tr>
      <th>77</th>
      <td>3.5</td>
      <td>3.2</td>
      <td>0.6</td>
      <td>1.8</td>
      <td>1.5</td>
      <td>2.0</td>
      <td>2.8</td>
      <td>Seventh Son (2015)</td>
    </tr>
    <tr>
      <th>78</th>
      <td>3.5</td>
      <td>3.2</td>
      <td>0.6</td>
      <td>1.5</td>
      <td>1.4</td>
      <td>1.6</td>
      <td>2.8</td>
      <td>Mortdecai (2015)</td>
    </tr>
    <tr>
      <th>83</th>
      <td>3.5</td>
      <td>3.3</td>
      <td>0.6</td>
      <td>1.7</td>
      <td>1.6</td>
      <td>2.5</td>
      <td>2.8</td>
      <td>Sinister 2 (2015)</td>
    </tr>
    <tr>
      <th>87</th>
      <td>3.5</td>
      <td>3.2</td>
      <td>0.6</td>
      <td>1.4</td>
      <td>1.6</td>
      <td>1.9</td>
      <td>2.7</td>
      <td>Unfinished Business (2015)</td>
    </tr>
  </tbody>
</table>
</div>




```python
score_film.iloc[25]
```




    STARS                     4.5
    RATING                    4.1
    RT_Norm                   0.4
    RTU_Norm                  2.3
    Meta_Norm                 1.3
    Meta_U_Norm               2.3
    IMDB_Norm                 3.0
    FILM           Taken 3 (2015)
    Name: 25, dtype: object




```python
#sum all sites
0.4+2.3+1.3+2.3+3
```




    9.3




```python
#averge score from all site
#without Fandango rating this film score lowest while on Fandango scores above 4
9.3/5
```




    1.86




```python

```
