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

**Note:** ChatGPT_single_function is just a prototype for our extended experiments, not a complete technique!

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
① AlphaRepair is publicly available at [here](https://zenodo.org/records/6819444).

② We added a call to the `add_new_line` method according to the paper. (The original code had the `add new line` method, but it didn't call it.)
<br>
<br>

## 2. ARJA-e:
### 2.1 Environment
- JDK 1.8
- Ubuntu 20.04

### 2.2 Experiment Setup
The original timeout used by ARJA-e was 1 hour, with a maximum number of generations of 50. For the sake of fairness, we multiply both parameters by 5.  
- Timeout: 5h
- Maximum number of generations: 250

### 2.3 Excluded Bug(s)
#### All 41 Closure bugs and All 2 Mockito bugs
> (1) As stated in ARJA-e's paper, ARJA-e ignored Closure because it uses the customized testing format instead of the standard JUnit tests.  
> (2) The implementation of ARJA-e is based on Defects4J (v1.0.1), so ARJA-e cannot work correctly on Mockito.

### 2.4 Source Code Availability
① ARJA-e is publicly available at [here](https://github.com/BaiGeiQiShi/ARJA-e-API.git). We have implemented a test filter on the original ARJA-e to ensure that ARJA-e only checks the same tests as the `Catena4j test`. 

② We fix a [bug](https://github.com/yyxhdy/arja/blob/arja-e/src/us/msu/cse/repair/core/util/Helper.java) (line 389-390) that ignores the case where the package name does not contain `.`, which will cause `index1` and `index2` to become -1.
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

① TBar is publicly available at [here](https://github.com/TruX-DTF/TBar).

② We change the a field ```isTestFixPatterns``` in ```edu.lu.uni.serval.tbar.AbstractFixer``` from **false** to **true**, so that it can generate more plausible patches. This makes it fairer to compare with other tools.

## 6. Recoder:
### 6.1 Environment
- JDK 1.8
- Python 3.8
- CUDA 11.3.1
- cudnn 8.2.1
- torch 1.13.1
### 6.2 Experiment Setup
- Timeout: 5h

### 6.3 Excluded Bug(s)
> None.
### 6.4 Source Code Availability
① Recoder is publicly available at [here](https://github.com/BaiGeiQiShi/RecoderAPI.git).

② We reformat the patches of Recoder according to this [rule](rules.md) for the convenience of result statistics.
<br>
<br>

## 7. SimFix:
### 7.1 Environment
- JDK 1.8
- Defects4J 2.0
- Ubuntu 20.04

### 7.2 Experiment Setup
- Timeout: 5h
- Plausible patches number: 500

### 7.3 Excluded Bug(s)
> None

### 7.4 Source Code Availability
① SimFix is publicly available at [here](https://github.com/BaiGeiQiShi/SimFixAPI.git).

② We have added a parameter to SimFix to indicate the number of generated plausible patches.
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
