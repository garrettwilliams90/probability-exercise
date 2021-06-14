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

What is the probability of there being Clear conditions on street 1 and clear conditions on street 2?

> When solving probability problems, the language is usually very important. In this case, the word `and` is used. 

> Here, we can use the conditional probability formula: $P(B|A) = P(A\space and\space B)/P(A)$, but the terms in the formula will need to be moved around first!


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



# Card Combinatorics

<img src="https://www.denofgeek.com/wp-content/uploads/2020/06/magic-the-gathering-competitive-decks.jpg?fit=1200%2C675" width="600px;">

## Question 6

The rules for the card game Magic the Gathering are as followed:

* A player can have a maximum of 7 cards in their hand
* A deck must have 60 cards

In the cell below, calculate the number of possible 7 card combinations from a deck containing 60 cards.


```python
from math import factorial

factorial(60)/(factorial(60-7) * factorial(7))
```




    386206920.0



## Question 7

A standard magic the gathering deck has 60 cards in total, and is made up of 24 land cards and 36 magic cards.

Given a hand of seven hards, how many possible hand combinations exists that contain exactly two lands?


```python
def nchoosek(n, k):
    return factorial(n)/(factorial(n-k) * factorial(k))

deck_count = 60
land_count = 24
magic_count = 36
lands_in_hand = 2
magic_in_hand = 7 - lands_in_hand


nchoosek(land_count, lands_in_hand) * nchoosek(magic_count, magic_in_hand)
```




    104049792.0



## Question 8

Given a hand of seven cards, what is the probability of drawing a hand with 2 *or more* land cards?

*Hint:* If you're stuck, check out [this thread](https://www.quora.com/How-many-different-hands-can-be-dealt-that-contain-3-aces-A-hand-of-five-cards-is-dealt-from-a-pack-of-52-playing-cards#:~:text=The%20number%20of%20ways%20to%20draw%20two%20Aces%20from%20four,*6*44%20%3D%201%2C584.)


```python
# Your code here
# 0.8573441200898213

deck_count = 60
land_count = 24
magic_count = 36

matching_hands = 0
for num_lands in range(2, 8):
    magic_in_hand = 7 - num_lands
    matching_hands += nchoosek(land_count, num_lands) * nchoosek(magic_count, magic_in_hand)
    
total_hands = nchoosek(60, 7)

matching_hands/total_hands
```




    0.8573441200898213




```python

```
