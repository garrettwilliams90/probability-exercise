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

What is the probability of there being Clear conditions on street 1 and clear conditions on street 2?

> When solving probability problems, the language is usually very important. In this case, the word `and` is used. 

> Here, we can use the conditional probability formula: $P(B|A) = P(A\space and\space B)/P(A)$, but the terms in the formula will need to be moved around first!


```python
# P(A and B) = P(B|A) * P(A)
# P(Clear 1 and clear 2) = P(Clear 2|Clear 1) * P(Clear 1)
# P(Clear 2|Clear 1) = 180/195
# P(Clear 1) = 195/365
clear_street1_clear_street2 = (180/195) * (195/365)
clear_street1_clear_street2
```




    0.4931506849315069



## Question 2

What is the probability of it not being Icy on `Street1` and Icy on `Street2`?

$P(Street1 ∈ {Clear ∪ Wet} ∩ Street2=Icy)$


```python
# P(A and B) = P(B|A) * P(A)
# P(1 = {Clear, Wet} and 2 = {Icy})
# P(1 Clear or Wet and 2 Icy) = P(2 Icy| 1 Clear or Wet) * P(1 Clear or Wet)
# P(2 Icy | 1 Clear or Wet) = 27/292
# P(1 Clear or Wet) = 292/365
not_icy_street1_icy_street2 = (27/292) * (292/365)
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
# P(B|A) = P(A and B)/P(A)
# P(1 Clear|2 Clear) = P(1 Clear and 2 Clear)/P(2 Clear)
# P(1 Clear and 2 Clear) = 180/365
# P(2 Clear) = 210/365
clear_street1_given_clear_street2 = (180/365)/(210/365)
clear_street1_given_clear_street2
```




    0.8571428571428571



clear_street1_clear_street2df.loc['Clear'].sum()## Question 5

What is the probability of it being Clear on `Street2` given that it is Clear on `Street1`?

$P(Street2=Clear|Street1=Clear) = \displaystyle \frac{P(Street2=Clear∩Street1=Clear)}{P(Street1=Clear)}$


```python
# P(B|A) = P(A and B)/P(A)
# P(2 Clear| 1 Clear) = P(2 Clear and 1 Clear)/P(1 Clear)
# P(2 Clear and 1 Clear) = 180/365
# P(1 Clear) = 195/365
clear_street2_given_clear_street1 = (180/365)/(195/365)
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
# n!/((n-k)! * k!)
# 6! = 6 * 5 * 4 * 3 * 2 * 1
# 60 * 59 * 58 * 57

# Solution formula:
# 60!/((60-7)! * 7!)
# total_cards_factorial/(total_cards-hand_size)_factorial * hand_size_factorial

from math import factorial

factorial(60)/((factorial(60 - 7)) * factorial(7))

# 386206b920.0
```




    386206920.0




```python
# Manually
numerator = 60 * 59 * 58 * 57 * 56 * 55 * 54
denominator = 7 * 6 * 5 * 4 * 3 * 2 * 1

numerator/denominator
```




    386206920.0



## Question 7

A standard magic the gathering deck has 60 cards in total, and is made up of 24 land cards and 36 magic cards.

Given a hand of seven hards, how many possible hand combinations exists that contain exactly two lands?


```python
def nchoosek(n, k):
    return factorial(n)/(factorial(n-k) * factorial(k))

deck_size = 60
hand_size = 7
land_cards = 24
magic_cards = deck_size - land_cards
lands_in_hand = 2
magic_in_hand = hand_size - lands_in_hand


nchoosek(land_cards, lands_in_hand) * nchoosek(magic_cards, magic_in_hand)
```




    104049792.0



## Question 8

Given a hand of seven cards, what is the probability of drawing a hand with 2 *or more* land cards?

*Hint:* If you're stuck, check out [this thread](https://www.quora.com/How-many-different-hands-can-be-dealt-that-contain-3-aces-A-hand-of-five-cards-is-dealt-from-a-pack-of-52-playing-cards#:~:text=The%20number%20of%20ways%20to%20draw%20two%20Aces%20from%20four,*6*44%20%3D%201%2C584.)


We can solve this a couple ways. 

1. We can find the number of possible hands that can have 2-7 lands and divide by the total number of possible hands
2. We can find the number of possible hands that have 1-2 lands, subtract that number from the total, and divide by the total number of possible hands.

**Solution 1:**


```python
# Establish our contextualizing parameters
deck_size = 60
hand_size = 7
land_cards = 24
magic_cards = deck_size - land_cards

# Instantiate a variable to keep track of the number
# of possible hands for an x number of lands
matching_hands = 0

# Loop over the numbers 2,3,4,5,6,7
for num_lands in range(2, 8):
    # Calculate the number of magic cards
    # By subtracting the number of lands
    # from the total size of the hand
    magic_in_hand = hand_size - num_lands
    # Calculate the number of matching hands
    matching_hands += nchoosek(land_cards, num_lands) * nchoosek(magic_cards, magic_in_hand)
# Caclulate the total number of possible hands
total_hands = nchoosek(deck_size, hand_size)
# Calculate the probability of a hand with >= 2 lands
matching_hands/total_hands
```




    0.8573441200898213



**Solution 2:**


```python
# The number of hands with exactly one land
possible_hands_lands_1 = nchoosek(magic_cards, 6) * nchoosek(land_cards, 1)
# The number of hands with exactly 0 lands
possible_hands_lands_0 = nchoosek(magic_cards, 7) * nchoosek(land_cards, 0)
# The number of hands with <= 1 land
total_opposite_outcomes = possible_hands_lands_1 + possible_hands_lands_0
# The total number of possible hands
total_hands = nchoosek(deck_size, hand_size)
# The number of events with >= 2 lands
total_matching_outcomes = total_hands - total_opposite_outcomes
# Probability of a hand with >= 2 lands
total_matching_outcomes/total_hands
```




    0.8573441200898213


