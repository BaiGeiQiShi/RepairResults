# Multi-hunk Repair Results
## Overview
This repo includes the repair results of several SOTA multi-hunk and single-hunk repair techniques in 105 CatenaD4j multi-hunk bugs, including:

* **Multi-hunk techniques:**
   * ARJA-e
   * ITER
   * Hercules
* **Pattern-based single-hunk technique:**
   * TBar
* **NMT-based single-hunk technique:**
   * Recoder
* **Search-based single-hunk technique:**
   * SimFix
* **LLM-based single-hunk technique:**
   * AlphaRepair

**Note:** In this repository, we present the plausible and correct patches for each tool. Additionally, we have created a repository for each technique and provided corresponding experimental environment and Dockerfile to replicate our experiments.

<br>

## 1. AlphaRepair
### 1.1 Environment
- JDK 1.8
- python 3.10
- Defects4J 2.0
- Ubuntu 20.04

### 1.2 Experiment Setup
- Timeout: 5h
- beam_width: 5
- Plausible patches number limit at one suspicious location: 5000

### 1.3 Excluded Bug(s)
> None

### 1.4 Source Code Availability
① AlphaRepair is publicly available at [here](https://github.com/give-to/AlphaRepairAPI).

② We added a call to the `add_new_line` method according to the paper. (The original code had the `add new line` method, but it didn't call it.)
<br>
<br>

## 2. ARJA-e:
ARJA-e is a new genetic programming (GP) based program repair approach for Java.
### 2.1 How to reproduce experiments
Our ARJA-e source code, dockerfile, running environment, and setup are publicly available at [here](https://github.com/BaiGeiQiShi/ARJA-e-API.git). 
<br>
<br>

## 3. ITER:
### 3.1 Environment
- JDK 1.8
- Python 3.8
- Pytorch 1.7.1
- CUDA
- transformers
- sentencepiece
### 3.2 Experiment Setup
- Timeout: 5h

### 3.3 Excluded Bug(s)
#### Mockito_13_1 & Mockito_20_1 
> The source code of ITER shows that ITER cannot work correctly on Mockito (It can be proven by the results of ITER's paper, which does not include the results of Mockito).

### 3.4 Source Code Availability
We have learned about ITER from [here](https://arxiv.org/abs/2304.12015). And thanks to the help of [He Ye](https://www.kth.se/profile/heye), we have obtained the prototype of ITER privately. So we cannot publish ITER.
<br>
<br>

## 4. Hercules:
### 4.1 Environment

- JDK 1.8
- Python 3.8
- imbalanced_learn==0.11.0
- imblearn==0.0
- matplotlib==3.7.3
- numpy==1.24.4
- pandas==2.0.3
- scikit_learn==1.3.1
- xgboost==1.6.1
- tqdm==4.66.1

### 4.2 Experiment Setup

- Timeout: 5h

### 4.3 Excluded Bug

> None

### 4.4 Source Code Availability

> We only reproduced the Hercules-MinusHistory.

Hercules is publicly available at [here](https://github.com/give-to/Hercules).

#### 4.4.1 Spectrum Based Fault Localization

We use the [GZoltar](https://github.com/GZoltar/gzoltar) to identify potential repair locations. The formula we used in GZoltar is Ochiai.

#### 4.4.2 Identification of Evolutionary Siblings

① We use [soot](https://github.com/soot-oss/soot) to extract program context.

② When comparing two AST nodes N1 and N2, we only use kind compatibility and name similarity. Because there are some nodes, the JDT cannot get their type. 

#### 4.4.3 Patch Generation

We completed the stages of building an abstract syntax tree and generating patches based on [TBar](https://github.com/TruX-DTF/TBar). 

① We change the a field ```isTestFixPatterns``` in ```edu.lu.uni.serval.tbar.AbstractFixer``` from **false** to **true**, so that it can generate more plausible patches.

② We removed some templates and kept only the templates used in PAR, ACS, Elixir, which are cited by the authors in the Implementation part.

③ We transform the patches generated by TBar according to this [rule](./rules.md).

#### 4.4.4 Ranking of Candidate Patches

We use [ODS](https://dl.acm.org/doi/10.1109/TSE.2021.3071750) to rank the candidate patches, which is also a learning-based ranking model. Because we do not have the ranking model similar to Elixir.

## 5. TBar:
### 5.1 Environment

- JDK 1.8
- Defects4J 2.0
- SVN >= 1.8
- perl >= 5.0.10

### 5.2 Experiment Setup

- Timeout: 5h

### 5.3 Excluded Bug

> None

### 5.4 Source Code Availability

① TBar is publicly available at [here](https://github.com/give-to/TBarAPI.git).

② We change the a field ```isTestFixPatterns``` in ```edu.lu.uni.serval.tbar.AbstractFixer``` from **false** to **true**, so that it can generate more plausible patches. This makes it fairer to compare with other tools.

## 6. Recoder:
Recoder is a syntax-guided edit decoder with placeholder generation.
### 6.1 How to reproduce experiments
Our Recoder source code, dockerfile, running environment, and setup are publicly available at [here](https://github.com/BaiGeiQiShi/RecoderAPI.git).
<br>
<br>

## 7. SimFix:
SimFix is an automatic program repair technique, which leverages exisiting patches from other projects and similar code snippets in the same project to generate patches.
### 7.1 How to reproduce experiments
Our SimFIx source code, dockerfile, running environment, and setup are publicly available at [here](https://github.com/BaiGeiQiShi/SimFixAPI.git).
<br>
<br>

## Repo Structure:
```
   /MultiRepairResults
   |——AlphaReapir
   |	|——correct_patches
   |	|——plausible_patches
   |	|——README.md      // explain correct patches  
   |——ARJA-e
   |	|——plausible_patches
   |	|——README.md      // explain why ARJA-e has no correct patches
   |——Hercules
   |	|——correct_patches
   |	|——plausible_patches
   |	|——README.md      // explain correct patches          
   |——ITER              
   |	|——correct_patches
   |	|——plausible_patches
   |	|——README.md      // explain correct patches
   |——Recoder
   |	|——correct_patches
   |	|——plausible_patches
   |	|——README.md      // explain correct patches              
   |——SimFix
   |	|——correct_patches
   |	|——plausible_patches
   |	|——README.md      // explain correct patches         
   |——TBar
   |	|——correct_patches
   |	|——plausible_patches
   |	|——README.md      // explain correct patches
   |——README.md
   |——rules.md                        
```
