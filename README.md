# Probability of road conditions
<img src="roads.jpg" alt="Image of roads" width="500"/>


```python
# Run this cell unchanged
import pandas as pd
from test_background import pkl_dump, test_obj_dict, run_test_dict, run_test

data = [{'Clear': 180, 'Wet': 15, 'Icy': 0},
       {'Clear': 30, 'Wet': 40, 'Icy': 27},
       {'Clear': 0, 'Wet': 22, 'Icy': 51}]

df = pd.DataFrame(data, index = ['Clear', 'Wet', 'Icy'])
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
      <th>Clear</th>
      <th>Wet</th>
      <th>Icy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Clear</th>
      <td>180</td>
      <td>15</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Wet</th>
      <td>30</td>
      <td>40</td>
      <td>27</td>
    </tr>
    <tr>
      <th>Icy</th>
      <td>0</td>
      <td>22</td>
      <td>51</td>
    </tr>
  </tbody>
</table>
</div>



**The above dataframe** represents the joint road conditions for two neighboring streets over a time frame of 365 days. 

The index represents `Street 1` and the columns represent `Street  2`

The values represent the number of days the two road conditions for each street occurred on the same day.
>ie. There were 15 days out of 365 that `Street 1` had Clear conditions and `Street 2` had Wet conditions

## Question 1

What is the probability of there being Clear conditions for both streets at the same time?

$P(Street 1= Clear ∩ Street 2=Clear)$


```python
# Your code here
```

## Question 2

What is the probability of it not being Icy on `Street1` and Icy on `Street2`?

$P(Street1 ∈ {Clear ∪ Wet} ∩ Street2=Icy)$


```python
# Your code here
```

## Question 3

What is the probability of it being Clear on `Street2` <u>regardless of the conditions</u> on `Street1`?

$$P(Street2=Clear) =$$ 
$$P(Street2=Clear ∩ Street1=Clear) + $$
$$P(Street2=Clear ∩ Street1=Wet)+ $$
$$P(Street2=Clear ∩ Street1=Icy)$$


```python
# Your code here
```

## Question 4

What is the probability  of it being Clear on ```Street1``` given that it is Clear on ```Street2```?

$P(Street1=Clear|Street2=Clear) = \displaystyle \frac{P(Street1=Clear∩Street2=Clear)}{P(Street2=Clear)}$


```python
# Your code here
```

## Question 5

What is the probability of it being Clear on `Street2` given that it is Clear on `Street1`?

$P(Street2=Clear|Street1=Clear) = \displaystyle \frac{P(Street2=Clear∩Street1=Clear)}{P(Street1=Clear)}$


```python
# Your code here
```
