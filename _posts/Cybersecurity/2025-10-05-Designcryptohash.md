---
title: "How Secure Hash Functions Are Built: From Merkle-Damgård to SHA-3"
date: 2025-10-05
toc: true
toc_sticky: true
use_math: true
categories:
  - cybersecurity
---

In the last post, we have learned about 3 properties of Cryptographic Hash function. Today, let's have a look about the relation between those properties and some various secure hash functions.

# Relation between properties

As we learned from the last post, the 3 properties of cryptographic hash functions are:
1. Preimage-resistance
2. Second-preimage-resistance
3. Collision-resistance

## [2,3] Second preimage resistance $\nRightarrow$ Collision resistance

There is a counter example that proves this relation.

Assume $H : X \rightarrow \\{0,1\\}^{256}$ is Second preimage resistance.

Let's define some arbitrary function 
$$
H'(x) =
\begin{cases}
  0^{256}, & \text{if } x = 0 \text{ or } x = 1 \\
  H(x), & \text{otherwise}
\end{cases}
$$

$H'$ is second preimage resistant but not collision resistant.

## [2,3] Collision resistance $\Rightarrow$ Second preimage resistance

This relation can be proved by contrapositive: **"If a hash is not Second preimage resistant, it is also not collision resistant".**

1. Suppose an adversary has $x_0$ and its hash $H(x_0)$.
2. The fact that second preimage resistance does not hold means that for a given $x_0$, we can find a different $x_1$ that yields the same digest. So, the adversary successfully found an $x_1$ such that $H(x_0) = H(x_1)$.
3. Since there are two different inputs $x_0, x_1$ that output the same digest, a collision has been found.

## [1,2] Second preimage resistance $\nRightarrow$ preimage resistance

This relation can be also proved by contrapositive.

## Conclusion

Long story short, all we need is a **collision-resistant hash**.

# How can we design a cryptographic hash functions? : The Merkle-Damgård Construction
Blueprint : 구조
Collision resistance는 어떻게 유지되는가? 
생각해야 될 것 : 안전한 압축 함수는 어떻게 만들까? 

## Blueprint of Merkle-Damgård Construction

Since creating complete collision-resistant hash-function \\[H : \\{0,1\\}^* \rightarrow \\{0,1\\}^n \\] is difficult task, 
The key idea is to think of an algorithm that compresses by chaining smaller compression functions.
\\[ h : \\{0,1\\}^{n+b} \rightarrow \\{0,1\\}^n \\]

There is a theorem :
**If h is collision resistant, then so is H.**
It can be proved by contrapositive. If you're looking for the detail of proof, check the [Youtube link](https://www.youtube.com/watch?v=VCOinPlsThw)

![image](https://res.cloudinary.com/dvjifrdjf/image/upload/v1759677975/markdown-images/oaqhtogffidozwddavv8.png)
*image from lecture slide*

- preprocessing (padding, length) : As the image shown above, add specific padding bits and message length $|M|$ 
to the end of the message. So that each block($M_1, M_2, ...$) has the same size.

The equation can be written as:
\\[ H(M) := h(h(\dots h(h(\text{IV} || M_1)) || M_2) \dots || M_n) || \text{padding} \& |M|\\]

MD5,SHA1,SHA2 algorithms used this Merkle-Damgård construction. 
SHA3 used totally different construction called sponge.

## How can we design the collision resistance compression function h?

There is 2 ways to construct these function $h$.

1. Design from scratch
- design a totally new compression function designed solely for hashing, without relying on other algorithms.
- early hash functions like MD4, MD5 used this method.

2. Use block cipher (symmetic key encryption)
- This is a method of creating a compression function using block cipher technology, which has already been proven to be secure for a long time, as a component, such as AES.
- Davies Meyer , Miyaguchi-Preneel

## Block cipher
A symmetric key encryption technology, like AES, uses a key to convert a block of plaintext into ciphertext. Of course, decryption is also possible if you have the key.

## Davies-Meyer

![image](https://res.cloudinary.com/dvjifrdjf/image/upload/v1759736173/markdown-images/feggnjrd0yzftpfqnzab.png)

\\[ h(V_i,m) := E(m, V_i) \oplus V_i \\]

- $m$ : message block, this is used as a **key** for encryption.
- $V_i$ : former hash value, this is used as a **plaintext** for encryption.
- $E(m, V_i)$ : use $m$ as a key, and $V_i$ as a plaintext, create a ciphertext.
- $\oplus V_i$ : this XOR makes the method to be non-reversible.(If there is no XOR, then it can easily decrypted because every block cipher has its own decrypt function $D$)

**Theorem** : If the $E$ is ideal(unpredictable output), the compression function $h$ built with Davies-Meyer structure is mathematically proven to be collision-resistant up to the Birthday Attack level : $O(2^{\frac{n}{2}})$ 
This means it has the theoretical best resistance to brute-force attack.

# SHA : Secure Hash Algorithm
## SHA-1

![image](https://res.cloudinary.com/dvjifrdjf/image/upload/v1759737095/markdown-images/cbolgoe00ekvldtakvzq.png)

$$
\{0,1\}^{512} \times \{0,1\}^{160} \rightarrow \{0,1\}^{160}
$$

Just like Davies-Meyer structure, SHA1 creates hash value using former hash value and the plaintext.
Each size of the block is 512bits, and it repeats the diagram 80 times.

Size of the digest is 160bits.

## SHAttered attack : End of SHA-1

Since 2005, theoretical attacks have been published that claim to require far fewer operations to find a SHA-1 collision than a brute-force birthday attack : $2^{80}$ . In the research, they have shown collisions can be found in $2^{63}$ operations.

Also in 2017, Stevens&Karpman and Google have found the collision by operating $2^{63.1}$ times. 
They have found the collision in the hash value of two different pdf file using SHA-1. 
[Paper link](https://shattered.io/static/shattered.pdf)

## SHA-2
- Longer digest : SHA-256 outputs 256 bits and SHA-512 outputs 512 bits, so the number of operation needs to perform Birthday attack is $2^{128}, 2^{256}$
- More complicate structure 

## SHA-3 
![image](https://res.cloudinary.com/dvjifrdjf/image/upload/v1759752034/markdown-images/hwzgocoz8lqb1zbfvt5u.png)
- SHA-3 use completely differnet structure called sponge. 
- Absorbing : It absorbs input block by block and changes the state.
- Squeezing : After absorbing all input, it **outputs a digest of the desired length**, like squeezing water out of a sponge.

The biggest feature of SHA-3 is that it can choose their digest length, so it can used in random number generator

# Padding
As we learned above, padding is used in Merkle-Damgård, and SHA.
We use padding because: 
- Merkle-Damgård is processed by dividing it into fixed blocks, but it is not given in exact multiples of the block size.
- For security, we have to add the information about the length of the message.

## Exercise
\\[ |P| = (-|M|-\text{recording length}) \mod \text{block size} \\]

In the case of SHA-512, the padding length equation is : 

\\[ \|P\| = (-\|M\|-128) \mod 1024 \\] 

- $ \|M\| $ : The bit length of input
- $128$ : 128 bits are used for recording the length of message
- $1024$ : block size 

### 1 : Padding length
Let's consider the case that in SHA-512, the length of original message is $2590$ bits, and block-size is $1024$ bits.
The formula should be : 
$$
\begin{aligned}
  |P| = (-|M|-128) \mod 1024 &= (-2590-128) \mod 1024 \\
           &= -2718 \mod 1024 \\
           &= 354
\end{aligned}
$$

So the padding bits are $354$ bits. 
The padding consists of one $1$ followed by 353 of $0$'s. So, $10000000000...$

### 2 : length of original message is already a multiple of 1024 bits
In this case, we still need to add the length field. So, still the padding is needed.

### 3 : Least and Max value of padding
**Least** padding bit is 1 bit. \\
ex. $895$ bits : original message($895$) + padding($1$) + length information($128$)

**Max** padding bits are 1024 bits.\\
ex. $896$ bits : original message($896$) + padding($1$) + length information($128$) = $1025$ bits. 
so, we need to aim for the next multiple of 1024 : $2048$.

### 4. Ambiguous Hashing

We can make the hash value in terminal, 
Let's make the message "Alice send Bob $\\$100$ and the fee is $\\$15$" into hash value
```ps
echo -n "Alice""Bob""100""15" | openssl dgst -sha3-256
```
by this code. This is recorded as Hash(AliceBob10015)
But is this safe?

No! receiver can understand this as "Alice send Bob $\\$1001$ and the fee is $\\$5$" 

So the solution is, use the delimiter(pipe)
Hash("Alice|Bob|100|15") just like this. 

