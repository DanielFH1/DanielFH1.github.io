---
title: "Paper review : TransGEM, a molecule generation model"
date: 2025-10-06
toc: true 
toc_sticky : true
use_math: true
categories:
    - med
---
[Transgem Paper Link](https://academic.oup.com/bioinformatics/article/40/5/btae189/7649318){:target="_blank"}
# Motivation

- How can we overcome the limitations of traditional drug design methods?
- How can we improve these methods using AI?

## Previous Research

### Ligand-based design(1960s Corwin Harsh et al.)

Ligands : existing drug

Ligand-based methods are approaches for creating new drugs by analyzing and referencing the structures and properties of ligands ****that are already known to be active against the disease

Limitations in creativity : since, this approach based on existing keys, it’s very difficult to create a completely new drugs.

---

### Receptor-based design(1890s Emil Fisher et al. , 1970s)

In 1890s, Emil Fisher introduced the concept of **Lock and key.**

Specificity : only specific enzyme activates on specific substrate. 

In 1958s, Daniel Koshland introduced the concept of **Induced fit.**

Enzyme’s active site is not initially a perfect structural complement to the substrate. 

Instead, binding induces a conformational change to more precise and optimal fit. 

So, the idea is…

if you know the precise 3D structure of problem-causing protein, then let’s make the precise drugs that perfectly fit into the enzyme

**But…**

It is very hard to know the perfect 3D structure of problem-causing protein.

---

## Limitations on previous methods.

> Nevertheless, molecules generated from these knock-out transcriptomic profiles
exhibited a notable lack of correlation with known inhibitors of the targeted genes
> 

Previously, we used GAN, VAE, AAE models to generate to molecules.

But, the problem is…

1. Only few molecules are actually usable 
2. It showed a little correlation with actual drug efficiency
3. noisy data : *level 5 gene expression data

Also, 8.5 % of success rate(=valid molecules) has obtained by early ai models.

*level

In this paper, “level” refers to the processing stages of gene expression data in the LINCS(ibrary of Integrated Network-based Cellular Signatures) database.

Level 1 : Raw data

Level 2:

Level 3: Multiple replicates are averaged and standardized to produce stable and reproducible gene expression values. It has less noise, and more reliable.

Level 4:

Level 5: A consensus signature by aggregating results from multiple experimental conditions. Too much noise and less stable

---

# PDD : Phenotypic drug design

In this research, we don’t need a perfect structure of problem-causing protein.

Instead, the AI was trained on gene activity data from both normal and diseased cells.

AI analyzes the difference in these two datasets, and generates a new drug

Just like comparing a normal system log with an error log in computer system.

**While identifying the cause of a disease is very difficult, obtaining data on the cellular outcomes of the disease is much easier and more cost-effective.**

*

Genotype : Source code itself. 

Phenotype : Running program. ex) unusually active DNA in specific circumstances

---

## Process

1. Gene expression data
    1. Cell line : one hot encoding vector
        
        $v_c = \text{Linear}(\text{One\_hot}(C))$
        
    2. Gene expression difference values : use specific embedding function. In this study, we use 10-fold binary function(*) for embedding function. 
        
        $v_e = \text{Linear}(f_{\text{emb}}(E))$
        
    3. concatenate these vectors and pass through the Linear layer and Feedforward NN. resulting in matrix $G^\prime$
        
        $G' = \text{FNN}(\text{Linear}(\text{Concat}(v_c, \, v_e)))$
        

1. Molecule embedding
    1. split the molecule data in LINCS 1000 database into tokens. Thus, a molecule M can be represented as a collection of L tokens.
    
    $$
    M = (t_1, t_2, ..., t_L)
    $$
    
    b. Through the molecular embedding layer, the molecule $M$ is embedded as $M^\prime$
    
    $$
    M^\prime = Embed(M)
    $$
    
2. Transformer Decoder : train with the data $M^\prime , G^\prime$. The decoder of the transformer model is composed of N decoder layers.
    1. The Attention mechanism learns the association that "a given molecule causes a specific expression difference.”
    2. Ultimately, it obtains a unified representation $V_N$

1. Generator
    1. based on $V_N$ it either reconstructs the original molecule or generates new ones.

*10-fold binary : This is the methods that convert the number into binary. In this study we used this methods to utilize the first decimal point data.

ex) let’s encode 4.2 into binary using 10-fold binary methods.

1. Multiply by 10 : $42$
2. Convert into binary: $101010$
3. Padding : if the total bit length is 8, : $00101010$

---

# Experiments

## Datasets

- In order to avoid noise data, only 978 expression data has used ( totally, there is 12328 expression data in LINCS1000)
- Level 3 data : less noise and stable
- Train : 200 epoch, batch size 4, learning rate 1e-4
- Baseline : Early AI models(GAN, VAE …)

## Evaluation metrics

- Validity → Is the molecule chemically valid?
- Uniqueness → Is the molecule new and non-duplicate?
- Novelty → Is the molecule completely new, i.e., not present in the training data?
- InDiv → How diverse are the molecules within the set?

$$
\text{IntDiv}(M) = \sqrt{\frac{1}{\|M\|^2} \sum_{m_1, m_2 \in M} \text{sim}(m_1, m_2)}
$$

\\[ M: \text{set of molecules}, \quad m_1, m_2 \in M, \quad \text{sim}(m_1, m_2) :similarity \\]

- QED → Is the molecule drug-like (suitable as a drug)?
- SA → Is the molecule easy to synthesize in a laboratory?

## Benchmarks

In validity and novelty, TransGEM shows the perfect score!!!

*PC : Prostate Cancer, NSCLC: Non small cell lung cancer

- Property distributions of molecules generated by TransGEM are largely consistent with those of FDA-approved drugs.
- Docking experiment: it was confirmed that these molecules also bind well to actual target proteins.
- Genes with high attention scores were found to be associated with cancer onset

---

# Conclusion and Future Research

Transgem model has great potential to generate biologically active molecules.

In this study, the TransGEM model was applied to case studies of prostate cancer (PC) and non-small cell lung cancer (NSCLC).

The genes with high attention scores obtained by TransGEM, were mostly related to the disease itself. 

But…

In this study, only the 978 gene expression difference values were utilized to characterize the expression difference between disease cells and normal tissue cells, which inevitably leads to the loss of a substantial amount of information.