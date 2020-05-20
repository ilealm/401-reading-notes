[ HOME ](README.md)
# Read 09 - Statistics - Probability

> “What is the chance of an event happening?”

* To calculate the chance of an event happening, we also need to consider all the other events that can occur. e.g. Flipping a heads or Flipping a tails
* These diferent events form the **sample space**: the set of all possible events that can happen. 

> To calculate the probability of an event occurring, we count how many times are event of interest can occur (say flipping heads) and dividing it by the sample space. 

* Thus, probability will tell us that an ideal coin will have a **1-in-2** chance of being heads or tails.
* We can use statistics to calculate **_probabilities_** based on observations from the real world and check how it compares to the ideal.
* A **_trial_** is a set of number of ocurrecies that a event is created, with the intension of gatter data.
* One trial is only one data point.
* As we get more trials, the deviation away from the average decreases.

> Given enough data, statistics enables us to calculate probabilities using real-world observations

 * Probability provides the theory, 
    * While statistics provides the tools to test that theory using data. 
        * The descriptive statistics, specifically mean and standard deviation, become the proxies for the theoretical. 

### The Data and the Distribution
* The **_normal distribution_** refers to a particularly important phenomenon in the realm of probability and statistics. 
* The most important qualities to notice about the normal distribution is its symmetry and its shape:


![](https://i.imgur.com/3vDS2Au.png)
* The **_x-axis_** takes on the values of events we want to know the probability of. 
* The **_y-axis_** is the probability associated with each event, from 0 to 1.
* The high point in a statistical context actually represents the **_mean_**.


## Revisiting the normal
* The normal distribution is significant to probability and statistics thanks to two factors: 
    1. The Central Limit Theorem
    1. The Three Sigma Rule.

### The Central Limit Theorem

>This idea is a key tenet of the Central Limit Theorem. In our coin-tossing example, a single trial of 10 throws produces a single estimate of what probability suggests should happen (5 heads). We call it an estimate because we know that it won’t be perfect (i.e. we won’t get 5 heads every time).

* Central Limit Theorem dictates that the distribution of these estimates will look like a normal distribution. 
* Central Limit Theorem suggests that we can hone in on the theoretical ideal given by probability, even when we don’t know the true probability. 

### Three Sigma Rule

> Is an expression of how many of our observations fall within a certain distance of the mean.
* Also known as the empirical rule or 68-95-99.7
* The Three Sigma rule dictates that given a normal distribution, 68% of your observations will fall between one standard deviation of the mean. 95% will fall within two, and 99.7% will fall within three.
* The key takeaway is to know that the Three Sigma Rule enables us to know how much data is contained under different intervals of a normal distribution.

![](https://i.imgur.com/Mt3RyE0.png)

## Z-score
>Calculation that answers the question, “Given a data point, how many standard deviations is it away from the mean?

 The mean is the exact middle of the normal distribution, so we know that the sum of all probabilites of getting values from the left side up until the mean is 50%. The values from the Three Sigma Rule actually come up if you try to calculate the cumulative probability between standard deviations.