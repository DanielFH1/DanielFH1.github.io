---
title : "Probability for AI"
date: 2025-09-23
toc: true  # <--- 이 한 줄만 추가하면 됩니다!
toc_sticky : true
use_math: true
categories:
    - ai
---
# Motivation
Since there is no "100%" in any real worlds, the concepts about probability and statistics widely used in not only AI, but physics, engineering, economics and so on.

In AI, lot of concepts are written in probabilities and statistics such as
- The probability that this image is a 'dog' is 85%, a 'cat' is 10%, and a 'fox' is 5%.
- An autonomous vehicle continues driving only if the probability of identifying an object ahead as a 'person' is over 99.9%; otherwise, it stops immediately.
- Based on the analysis of credit card transaction patterns, the probability that this transaction is 'fraudulent' is 78%.
- When analyzing a patient's medical imaging (X-ray), the probability of a 'malignant tumor' being present is estimated at 65%.

---
# Definitions
Now let's have a look at some key concepts.

- Random Variable $$(X,Y)$$ : A quantity that is "uncertain". If the probability of every values in random variable is equal, we call this **uniform** distribution. There are two types of random variables
    - Discrete : dice(1,2,3,4,5,6), coin(H,T)
    - Continuous : weight, height

- Probability Distribution $$P(X)$$ : Probability value comes from closed interval [0,1]
    - Joint Distribution $$P(X,Y)$$ : Two or more events happening together 
    - Marginal Distribution $$P(X) = \sum_Y P(X, Y)$$: Gives the distribution of one variable, and ignoring the other.

- Expectation $E(X)$ : Expected value of a $$f(x)$$ with probability distribution $P(x)$
- Variance $V(X)$ : a measure of dispersion of $X$

## Conditional Probability
Conditional probability is the likelihood of an event happening, given that another event has already occurred.
$$P(A|B)$$ "Probability of event A given that event B has occured"

## Independence
If the random variable X and Y are independent, 
- $$ P(x,y) = P(x)P(y)$$
- $$ P(x|y) = P(x)$$
- $$ P(y|x) = P(y)$$

## Bayes' Rule
>"How do probabilities change when new evidence arrives?"

It gives an mathematical rule for inverting conditional probabilities, allowing the probability of a cause to be found given its effect.

This theorem is used to determine the conditional probability of an event based on prior knowledge and new evidence.

\\[ P(A \mid B) = \frac{P(B \mid A) P(A)}{P(B)} \\]

- $P(A)$ = Prior
- $P(B)$ = Marginal liklihood : Probability of the evidence $B$. 
Since, $P(B) = P(B) = \int P(A,B) \,dA = \int P(B \mid A)P(A) \,dA$
- $P(A\mid B)$ = Posterior : Updated Probability after oberving event $B$.

## Entropy
\\[ H(X) = - \sum_{i} P(x_i) \log P(x_i) = \mathbb{E}[-logP]\\]
- $H(X)$ = Entropy
- $P(x_i)$ = The probability that the random variable X will have a specific value $x_i$.

Entropy is a measure of uncertainty.
High Entropy means high uncertainty and more possible outcomes.

For example, when AI predicts the next word, if the word is so obvious and sure, then the sentence will have low entropy





