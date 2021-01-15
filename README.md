# Probability of weather in two cities
<img src="https://i.ytimg.com/vi/6MGRkUlFZws/maxresdefault.jpg" alt="Weather cartoon" width="500"/>


```python
# Run this cell unchanged
import pandas as pd
from test_background import pkl_dump, test_obj_dict, run_test_dict, run_test

data = [{'Sunny': 6, 'Cloudy': 2, 'Rainy': 0},
       {'Sunny': 1, 'Cloudy': 5, 'Rainy': 2},
       {'Sunny': 0, 'Cloudy': 1, 'Rainy': 3}]

df = pd.DataFrame(data, index = ['Sunny', 'Cloudy', 'Rainy'])
df.head()
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
      <th>Sunny</th>
      <th>Cloudy</th>
      <th>Rainy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Sunny</td>
      <td>6</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Cloudy</td>
      <td>1</td>
      <td>5</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Rainy</td>
      <td>0</td>
      <td>1</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



**The above dataframe** represents the joint weather events for two neighboring cities over a time frame of 20 days. 

The index represents ```Town 1``` and the columns represent ```Town 2```

The values represent the number of days the two weather events in each town occurred on the same day.
>ie. There were 2 days out of 20 it was Sunny in ```Town 1``` and Cloudy in ```Town 2```

## Question 1

What is the probability of it being Sunny in both towns at the same time?

$P(Town1=Sunny ∩ Town2=Sunny)$


```python
sunny_town1_sunny_town2 = 6/20
sunny_town1_sunny_town2
# #used for tests
# pkl_dump([
#     (sunny_town1_sunny_town2,
#      'sunny_town1_sunny_town2')
# ]
# )
```




    0.3



## Question 2

What is the probability of it not being Rainy in ```Town1``` and Rainy in ```Town2```?

$P(Town1 ∈ {Sunny ∪ Cloudy} ∩ Town2=Rainy)$


```python
no_rain_town1_rain_town2 = 0/20 + 2/20
no_rain_town1_rain_town2
# #used for tests
# pkl_dump([
#     (no_rain_town1_rain_town2,
#      'no_rain_town1_rain_town2')
# ]
# )
```




    0.1



## Question 3

What is the probability of it being Sunny in ```Town2``` <u>regardless of the weather</u> in ```Town1```?

$$P(Town2=Sunny) =$$ 
$$P(Town2=Sunny ∩ Town1=Sunny) + $$
$$P(Town2=Sunny ∩ Town1=Cloudy)+ $$
$$P(Town2=Sunny ∩ Town1=Rainy)$$


```python

sunny_town2 = df.Sunny.sum()/20
sunny_town2

# #used for tests
# pkl_dump([
#     (sunny_town2,
#      'sunny_town2')
# ]
# )
```




    0.35



## Question 4

What is the probability  of it being Sunny in ```Town1``` given that it is Sunny in ```Town2```?

$P(Town1=Sunny|Town2=Sunny) = \displaystyle \frac{P(Town1=Sunny∩Town2=Sunny)}{P(Town2=Sunny)}$


```python

sunny_town1_given_sunny_town2 = sunny_town1_sunny_town2/sunny_town2
sunny_town1_given_sunny_town2

# #used for tests
# pkl_dump([
#     (sunny_town1_given_sunny_town2,
#      'sunny_town1_given_sunny_town2')
# ]
# )
```




    0.8571428571428572



## Question 5

What is the probability of it being Sunny in ```Town2``` given that it is Sunny in ```Town1```?

$P(Town2=Sunny|Town1=Sunny) = \displaystyle \frac{P(Town2=Sunny∩Town1=Sunny)}{P(Town1=Sunny)}$


```python
sunny_town1 = df.loc['Sunny'].sum()/20
sunny_town2_given_sunny_town1 = sunny_town1_sunny_town2/sunny_town1
sunny_town2_given_sunny_town1

# #used for tests
# pkl_dump([
#     (sunny_town2_given_sunny_town1,
#      'sunny_town2_given_sunny_town1')
# ]
# )
```




    0.7499999999999999


