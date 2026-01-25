---
title: "Preparing ML/DL interview"
date: 2026-01-10
toc: true
toc_sticky: true
use_math: true
categories:
  - job
published : false
---

# 1. Training data and testing data in the context of machine learning.

<details>
  <summary>Answer</summary>
  
  <div markdown="1">

  Training data generally refers to the portion of the data that a machine learning algorithm uses to learn patterns. For example, the parameters of a logistic regression algorithm can be chosen such that the error is minimized on the training set. The testing set is data that is not seen by the actual algorithm and is used purely to gauge the algorithm's performance.

  </div>
</details>

# 2. If you need to tune parameters, do you tune it on the training data? What do you do instead?

<details>
  <summary>Answer</summary>
  
  <div markdown="1">

  Generally, those are called hyperparameters. What people typically do is take out a portion of the training data and call it a validation set. Then they tune those hyperparameters to maximize the performance on the validation set.

  </div>
</details>

# 3. Which dataset do you actually evaluate the final model on?

<details>
  <summary>Answer</summary>
  
  <div markdown="1">

  Typically, you evaluate it on your test dataset at the final step. You should only be using your validation set to tune hyperparameters, and you should have a holdout set that never has any information used to inform the learning of the algorithm or the hyperparameters.

  </div>
</details>

# 4. Could you tell me about the differences between batch gradient descent, mini batch gradient descent, and stochastic gradient descent?

<details>
  <summary>Answer</summary>
  
  <div markdown="1">
  Certainly. While all three are optimization algorithms used to minimize the loss function, the key difference lies in how much data is used to calculate the gradient for a single parameter update. This affects both the training speed and the stability of convergence.
  
  Batch Gradient Descent uses the entire dataset to compute the gradient for a single step. 
  This produces a very stable error gradient and a direct path to the minimum, but it can be extremely slow and memory-intensive for large datasets.

  Stochastic Gradient Descent (SGD), in its purest form, uses a single training example (batch size of 1) for each update.
  This makes it very fast and memory-efficient. However, the gradients are very noisy, causing the loss to fluctuate or 'zigzag' towards the minimum. Interestingly, this noise can sometimes help the model escape local minima.

  Mini-batch Gradient Descent is the sweet spot between the two. It splits the data into small batches (e.g., 32 or 64 samples).
  It combines the stability of Batch Gradient Descent with the speed of SGD. In practice, this is the most common approach because it also allows us to leverage matrix vectorization for computational efficiency."

  </div>
</details>

# 5. 왜 이런 서로 다른 gradient descent 방식들이 존재하나요? 언제 각각을 선택하나요?

<details>
  <summary>Answer</summary>
  
  <div markdown="1">

  Typically, 

  </div>
</details>


# 6. Can you explain what Back-propagation is and how it works?

<details>
  <summary>Answer</summary>
  
  <div markdown="1">

  Sure. Back-propagation is the core algorithm used to train neural networks. It essentially calculates the gradient of the loss function with respect to each weight in the network.

  The process happens in two main steps: First, in the forward pass, the input data travels through the network to generate a prediction, and the loss is calculated by comparing this prediction to the actual target.

  Second, in the backward pass, we propagate this loss backward from the output layer to the input layer. Using the chain rule of calculus, we compute the gradient of the loss for each weight. These gradients tell us how much we need to adjust each weight to minimize the error. 
  
  Finally, an optimizer like SGD or Adam updates the weights using these gradients.

  </div>
</details>

# 7. Let's touch on CNNs. What is the role of 'Global Average Pooling' (GAP), and why might we prefer it over fully connected layers at the end of a network?

<details>
  <summary>Answer</summary>
  
  <div markdown="1">

  Global Average Pooling, or GAP, is an operation typically used before the final classification layer. It calculates the average value of each feature map in the last convolutional layer. We often prefer GAP over Fully Connected (FC) layers for two main reasons: 
  
  First, Parameters: GAP has no learnable parameters, whereas FC layers can contain millions, leading to overfitting. GAP acts as a structural regularizer. 
  Second, Input Flexibility: GAP allows the network to accept images of variable resolutions, whereas standard FC layers require a fixed input size. This is crucial for object detection tasks where image sizes vary.

  </div>
</details>

# 8. Can you explain the 'Self-Attention' mechanism in Transformers? specifically, what represent Query, Key, and Value?

<details>
  <summary>Answer</summary>
  
  <div markdown="1">

  Self-Attention is the mechanism that allows the model to weigh the importance of different words in a sentence relative to one another. It contains, so called Query, Key and Value. Essentially, the model asks, 'How much should I focus on this word (Key) given my current context (Query)?'
  
  The Query (Q) is the current word we are processing, that we would like to know about.
  The Key (K) is all other words in the sentence.
  The Value (V) is the actual content or information of those items.

  We calculate the dot product between the Query and Keys to get attention scores (weights). Then, we multiply these weights by the Values to get the final representation.


  </div>
</details>







