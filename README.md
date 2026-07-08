# Custom Multiple Sequence Alignment (MSA) Algorithm for Hemoglobin β Protein Evolution Analysis

![Bioinformatics](https://img.shields.io/badge/Domain-Bioinformatics-green)
![Computational Biology](https://img.shields.io/badge/Field-Computational%20Biology-blue)
![Python](https://img.shields.io/badge/Language-Python-yellow)
![Biopython](https://img.shields.io/badge/Library-Biopython-orange)
![Algorithm](https://img.shields.io/badge/Method-Multiple%20Sequence%20Alignment-red)
![License](https://img.shields.io/badge/License-MIT-lightgrey)


# Overview

Multiple Sequence Alignment (MSA) is a fundamental computational biology problem used for identifying conserved regions, studying evolutionary relationships, and analyzing functional similarities among biological sequences.

This repository presents the design and implementation of a **custom progressive Multiple Sequence Alignment algorithm** for **Hemoglobin subunit beta (HBB) protein sequences** from multiple vertebrate species.

The proposed method integrates classical bioinformatics algorithms with evolutionary sequence analysis:

- Needleman–Wunsch global pairwise alignment
- BLOSUM62 amino acid substitution scoring
- Affine gap penalty optimization
- Evolutionary distance matrix construction
- UPGMA guide tree generation
- Progressive multiple sequence alignment
- Consensus-based alignment refinement

The performance of the developed MSA framework is evaluated against **Clustal Omega**, a widely used standard tool for biological sequence alignment.


---

# Research Motivation

Protein sequence alignment plays a central role in computational biology by enabling:

- Identification of evolutionary conserved regions
- Detection of functional similarity between proteins
- Analysis of molecular evolution
- Investigation of protein families and structural conservation


Hemoglobin β (HBB) was selected as a representative protein because of its strong evolutionary conservation across vertebrate species while still containing informative sequence variations.


---

# Project Objectives

The main objectives of this project are:

- Design and implement an original MSA algorithm
- Develop a complete progressive alignment pipeline
- Optimize alignment parameters using training sequences
- Construct evolutionary relationships through guide tree analysis
- Evaluate alignment quality using conservation metrics
- Compare the proposed method with Clustal Omega
- Analyze conserved regions and gap distribution


---

# Dataset Description

The dataset consists of Hemoglobin β protein sequences obtained from multiple vertebrate species.

The dataset is divided into:

- Training sequences for parameter optimization
- Independent test sequences for final evaluation


---

# Training Dataset

Location:

```
data/proteins_train.fasta
```

Contains HBB sequences from:

| Species | Organism |
|---|---|
| Homo sapiens | Human |
| Mus musculus | Mouse |
| Rattus norvegicus | Rat |
| Canis lupus familiaris | Dog |
| Bos taurus | Cow |
| Gallus gallus | Chicken |
| Xenopus laevis | African clawed frog |
| Danio rerio | Zebrafish |


The training dataset was used for:

- Gap penalty optimization
- Pairwise evolutionary distance estimation
- Guide tree construction


---

# Test Dataset

Location:

```
data/proteins_test.fasta
```

Contains unseen HBB sequences:

| Species | Organism |
|---|---|
| Bos taurus | Cow |
| Sus scrofa | Pig |
| Monodelphis domestica | Opossum |
| Oryzias latipes | Medaka fish |


The test dataset was used exclusively for evaluating the final alignment performance.


---

# Methodology

The complete workflow of the proposed MSA framework is:


```
FASTA Protein Sequences

          |
          v

Sequence Preprocessing

          |
          v

Pairwise Needleman-Wunsch Alignment

          |
          v

BLOSUM62 Scoring + Affine Gap Penalties

          |
          v

Sequence Identity Calculation

          |
          v

Evolutionary Distance Matrix

          |
          v

UPGMA Guide Tree Construction

          |
          v

Progressive Multiple Sequence Alignment

          |
          v

Consensus-Based Refinement

          |
          v

Alignment Evaluation

          |
          v

Comparison with Clustal Omega
```


---

# Algorithm Implementation


## 1. Pairwise Sequence Alignment

Pairwise alignment is implemented using the classical:

**Needleman-Wunsch global alignment algorithm**

The algorithm uses:

- Dynamic programming optimization
- Global sequence comparison
- Affine gap modeling


Scoring scheme:

| Parameter | Value |
|---|---:|
| Substitution Matrix | BLOSUM62 |
| Gap Opening Penalty | 6 |
| Gap Extension Penalty | 0.5 |


---

# 2. BLOSUM62 Substitution Matrix

Protein similarity scoring is performed using the BLOSUM62 amino acid substitution matrix.

The scoring system considers:

- Conservative amino acid substitutions
- Biochemical similarity
- Evolutionary replacement probability


---

# 3. Evolutionary Distance Matrix

After pairwise alignment, sequence similarity is converted into evolutionary distance:


$$
Distance = 1 - Sequence\ Identity
$$


The resulting symmetric distance matrix is used for guide tree construction.


---

# 4. ## UPGMA Guide Tree Construction

A hierarchical clustering approach is applied using:

- **UPGMA (Unweighted Pair Group Method with Arithmetic Mean)**

The guide tree determines the order of progressive sequence alignment.

Generated visualization:

![UPGMA Guide Tree Construction](https://github.com/user-attachments/assets/dbc39b4e-7477-4e45-afaa-5a99d19e5433)


---

# 5. Progressive Multiple Sequence Alignment

Two progressive alignment strategies were implemented:


## Reference Sequence Strategy

The first sequence is used as the alignment representative.

Output:

```
results/custom_msa_first.fasta
```


## Consensus Profile Strategy

The consensus sequence of the current alignment is used as the representative profile.

Output:

```
results/custom_msa_consensus.fasta
```


The consensus-based strategy provides a more stable representation of conserved patterns.


---

# Parameter Optimization

Gap parameters were optimized using the training dataset.

Search space:

```
Gap opening:
6, 8, 10, 12


Gap extension:
0.5, 1.0, 1.5, 2.0
```


Optimal parameters:


| Parameter | Selected Value |
|---|---:|
| Gap Opening | 6 |
| Gap Extension | 0.5 |


The selected parameters achieved high conservation while minimizing unnecessary gap insertion.


---

# Evaluation Metrics

The alignment quality was evaluated using:


## 1. Conserved Columns

A column is considered fully conserved when:

- All sequences contain the same amino acid
- No gap exists in that position


---

## 2. Gap Analysis

The following metrics were calculated:

- Gap fraction
- Average gaps per sequence
- Gap distribution


---

## 3. Shannon Entropy Conservation Analysis

Column-wise Shannon entropy was used to measure conservation.

Lower entropy indicates stronger evolutionary conservation.


---

## 4. Column-wise Identity

The final custom alignment was compared with Clustal Omega using column-level similarity.


---

# Results


## Final Custom MSA Performance


| Metric | Value |
|---|---:|
| Final Alignment Length | 150 amino acids |
| Fully Conserved Columns | 119 |
| Conservation Percentage | 79.33% |
| Average Gaps per Sequence | 2.25 |
| Overall Gap Fraction | 0.0150 |


The results indicate strong evolutionary conservation among HBB protein sequences.


---

# Comparison with Clustal Omega


The proposed algorithm was compared against:

**Clustal Omega**


| Metric | Custom MSA | Clustal Omega |
|---|---:|---:|
| Alignment Length | 150 |150 |
| Fully Conserved Columns |119 |118 |
| Average Gaps per Sequence |2.25 |2.25 |
| Column-wise Identity |98.67% |100% |


## Observations

The developed MSA algorithm achieved results highly comparable with Clustal Omega.

Key findings:

- Similar alignment length
- Nearly identical conserved regions
- Comparable gap placement
- High column-wise similarity


These results demonstrate that the proposed custom alignment framework successfully reproduces biologically meaningful sequence alignments.


---

# Visualization Results


All generated figures are available in:


```
figures/
```


Included analyses:


## Sequence Characteristics

- Raw sequence length distribution


## Evolutionary Analysis

- Pairwise distance matrix
- UPGMA guide tree


## Alignment Evaluation

- Final alignment length
- Conserved column analysis
- Shannon entropy conservation comparison
- Column-wise identity comparison


## Gap Analysis

- Gap distribution per sequence
- Overall gap fraction comparison
- Gap comparison between alignment strategies


---

# Repository Structure


```
Custom-MSA-HBB/

│
├── README.md
├── LICENSE
├── requirements.txt
│
├── data/
│   ├── proteins_train.fasta
│   └── proteins_test.fasta
│
├── notebooks/
│   └── Bioinformatics_MSA.ipynb
│
├── results/
│   ├── custom_msa_first.fasta
│   └── custom_msa_consensus.fasta
│
├── figures/
│   ├── raw_sequence_lengths.png
│   ├── pairwise_distance_matrix.png
│   ├── upgma_guide_tree.png
│   ├── final_alignment_length.png
│   ├── conserved_columns.png
│   ├── conservation_entropy.png
│   ├── column_identity.png
│   ├── gaps_per_sequence.png
│   ├── overall_gap_fraction.png
│   └── gap_comparison.png
│
├── report/
│   └── Bioinformatics-MSA-report.pdf
│
└── screenshots/
    ├── clustalo_alignment1.png
    ├── clustalo_alignment2.png
    ├── clustalo_alignment3.png
    └── clustalo_alignment4.png

```


---

# Installation


Clone repository:


```bash
git clone https://github.com/hannahfathi99/Custom-MSA-HBB.git
```


Install dependencies:


```bash
pip install -r requirements.txt
```


Run notebook:


```
notebooks/Bioinformatics_MSA.ipynb
```


---

# Technologies


Implemented using:


- Python
- Biopython
- NumPy
- SciPy
- Pandas
- Matplotlib
- Seaborn
- Jupyter Notebook


---

# Author


## Hannah Fathi

M.Sc. Artificial Intelligence Student


Research Interests:

- Bioinformatics
- Graph Neural Networks
- Deep Learning
- Computer Vision
- Machine Learning


---

# Academic Relevance

This project demonstrates the integration of algorithmic bioinformatics approaches with computational analysis for studying protein evolution.

The developed framework provides experience in:

- Sequence alignment algorithms
- Evolutionary computation
- Protein sequence analysis
- Computational biology workflows
- Scientific benchmarking against established bioinformatics tools


This repository is part of my research portfolio toward **Artificial Intelligence, Computational Biology, and Bioinformatics research**.


---

# License

This project is released under the MIT License.
