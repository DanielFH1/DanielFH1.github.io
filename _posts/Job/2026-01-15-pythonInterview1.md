---
title: "Preparing Python interview"
date: 2026-01-15
toc: true
toc_sticky: true
use_math: true
categories:
  - job
published : false
---
# 1. What is a Generator in Python, and how is it different from a list?

<details>
  <summary>English</summary>
  
  <div markdown="1">

  A generator is a special type of iterator in Python that returns items one at a time only when requested, rather than storing the entire sequence in memory.

  The key difference lies in memory usage and execution style. 
  **A list** loads all elements into memory at once, which can be inefficient for large datasets. In contrast, a generator uses the yield keyword to produce values one by one on the fly. Which is called lazy evaluation. 

  For example, if I'm training a deep learning model with a dataset of 1M high resolution images, loading them as a list would cause out of memory problem. Using a generator allows me to load and process just one batch at a time. 

  </div>
</details>

# 2. In Python, what is the difference between a list and a tuple? And specifically regarding memory, which one is more efficient and why?

<details>
  <summary>Answer</summary>
  
  <div markdown="1">

  The primary difference is mutability. Lists are mutable, meaning we can change their content, while tuples are immutable. Regarding memory, tuples are more efficient. Because tuples are immutable, Python can allocate a fixed block of memory for them, making them lighter and faster to iterate over. Lists, on the other hand, require extra memory overhead to handle dynamic resizing (like over-allocation) to support operations like append

  </div>
</details>

