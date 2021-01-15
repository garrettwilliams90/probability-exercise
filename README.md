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

**The above dataframe** represents the joint road conditions for two neighboring streets over a time frame of 365 days. 

The index represents `Street 1` and the columns represent `Street  2`

The values represent the number of days the two road conditions for each street occurred on the same day.
>ie. There were 15 days out of 365 that `Street 1` had Clear conditions and `Street 2` had Wet conditions

## Question 1

What is the probability of there being Clear conditions for both streets at the same time?

$P(Street 1= Clear ∩ Street 2=Clear)$


```python
clear_street1_clear_street2 = 180/365 
clear_street1_clear_street2
```




    0.4931506849315068



## Question 2

What is the probability of it not being Icy on `Street1` and Icy on `Street2`?

$P(Street1 ∈ {Clear ∪ Wet} ∩ Street2=Icy)$


```python
not_icy_street1_icy_street2 = 0/365 + 27/365
not_icy_street1_icy_street2
```




    0.07397260273972603



## Question 3

What is the probability of it being Clear on `Street2` <u>regardless of the conditions</u> on `Street1`?

$$P(Street2=Clear) =$$ 
$$P(Street2=Clear ∩ Street1=Clear) + $$
$$P(Street2=Clear ∩ Street1=Wet)+ $$
$$P(Street2=Clear ∩ Street1=Icy)$$


```python
clear_street2 = df.Clear.sum()/365
clear_street2
```




    0.5753424657534246



## Question 4

What is the probability  of it being Clear on ```Street1``` given that it is Clear on ```Street2```?

$P(Street1=Clear|Street2=Clear) = \displaystyle \frac{P(Street1=Clear∩Street2=Clear)}{P(Street2=Clear)}$


```python
clear_street1_given_clear_street2 = clear_street1_clear_street2/clear_street2
clear_street1_given_clear_street2
```




    0.8571428571428571



## Question 5

What is the probability of it being Clear on `Street2` given that it is Clear on `Street1`?

$P(Street2=Clear|Street1=Clear) = \displaystyle \frac{P(Street2=Clear∩Street1=Clear)}{P(Street1=Clear)}$


```python
clear_street1 = df.loc['Clear'].sum()/365
clear_street2_given_clear_street1 = clear_street1_clear_street2/clear_street1
clear_street2_given_clear_street1
```




    0.923076923076923


