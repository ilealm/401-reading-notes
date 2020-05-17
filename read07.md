# Read 07, Game of Greed 2

> Code examples to generate random numbers

#### Generate a random number from 1 to 6.
```
import random
print(random.randint(1,6))
```


#### Simulate the rolling of 1000 dice. Now, count the number of times you roll 6. Print that number out.
```
import random
count = 0

def roll():
    return random.randint(1,6)

for i in range(1, 1001):
    if roll() == 6:
        count += 1
```

#### Die tomorrow game
He is going to roll 1 die tomorrow, 2 dice two days from now, 3 dice three days from now, and so on so that he rolls $a$ dice $a$ days from now. He gets tired rolling dice after rolling dice for 365 days (so the last day he rolls 365 dice). In Python, simulate this. How many times does he roll 3 after 365 days of rolling dice?
```
import random

def roll():
    return random.randint(1,6)

def count(amount):
    count_ = 0
    for i in range(1, amount+1):
        if roll() == 3:
            count_ += 1
    return count_

total = 0

for i in range(1, 366):
    total += count(i)

print(total)
```

#### 20 times Die tomorrow game
```
20 of my friends love rolling dice. They are all going to roll 1 die each tomorrow, 2 dice each two days from now, 3 dice each three days from now, and so on so that they roll $a$ dice each $a$ days from now. But, one of my friends gets tired very quickly and he only rolls dice for 1 day and stops. Another friend only will roll dice for 2 days, and another will roll dice for three days only, and so on up to the fact that my last friend will roll dice for 20 days. In Python, simulate this. How many times does someone roll 3 after everything?
```


