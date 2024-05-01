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
In this repository, `./AlphaRepair` contains all the plausible and correct patches we generated using AlphaRepair.

### 1.1 How to reproduce experiments

Our AlphaRepair source code, dockerfile, running environment, and setup are publicly available at [here](https://github.com/give-to/AlphaRepairAPI). If you want to replicate our experiments on AlphaRepair, please refer to this repository.
<br>
<br>

## 2. ARJA-e:
ARJA-e is a new genetic programming (GP) based program repair approach for Java. In this repository, `./ARJA-e` contains all the plausible patches we generated using ARJA-e.
### 2.1 How to reproduce experiments
Our ARJA-e source code, dockerfile, running environment, and setup are publicly available at [here](https://github.com/BaiGeiQiShi/ARJA-e-API.git). If you want to replicate our experiments on ARJA-e, please refer to this repository.
<br>
<br>

## 3. ITER:
ITER is a neural program repair system with an original training and inference loop enabling advanced multi-location patches. In this repository, `./ITER` contains all the plausible and correct patches we generated using ITER.
### 3.1 How to reproduce experiments
We have learned about ITER from [here](https://arxiv.org/abs/2304.12015). At that time, the source code of ITER was not publicly available. Thanks to the help of [He Ye](https://www.kth.se/profile/heye), we have obtained the prototype of ITER privately. So we cannot publish the ITER version we used. However, the source code of ITER has recently been made public. If you want to learn more about ITER, you can refer to [ITER](https://github.com/ASSERT-KTH/ITER.git).
<br>
<br>

## 4. Hercules:
In this repository, `./Hercules` contains all the plausible and correct patches we generated using Hercules.

### 4.1 How to reproduce experiments

Our Hercules source code, dockerfile, running environment, and setup are publicly available at [here](https://github.com/give-to/Hercules). If you want to replicate our experiments on Hercules, please refer to this repository.
<br>
<br>

## 5. TBar:
In this repository, `./TBar` contains all the plausible and correct patches we generated using TBar.

### 5.1 How to reproduce experiments

Our TBar source code, dockerfile, running environment, and setup are publicly available at [here](https://github.com/give-to/TBarAPI.git). If you want to replicate our experiments on TBar, please refer to this repository.
<br>
<br>

## 6. Recoder:
Recoder is a syntax-guided edit decoder with placeholder generation. In this repository, `./Recoder` contains all the plausible and correct patches we generated using Recoder.
### 6.1 How to reproduce experiments
Our Recoder source code, dockerfile, running environment, and setup are publicly available at [here](https://github.com/BaiGeiQiShi/RecoderAPI.git). If you want to replicate our experiments on Recoder, please refer to this repository.
<br>
<br>

## 7. SimFix:
SimFix is an automatic program repair technique, which leverages exisiting patches from other projects and similar code snippets in the same project to generate patches. In this repository, `./SimFix` contains all the plausible and correct patches we generated using SimFix.
### 7.1 How to reproduce experiments
Our SimFix source code, dockerfile, running environment, and setup are publicly available at [here](https://github.com/BaiGeiQiShi/SimFixAPI.git). If you want to replicate our experiments on SimFix, please refer to this repository.
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
   |	|——rules.md       // describe the patch format of Recoder
   |——SimFix
   |	|——correct_patches
   |	|——plausible_patches
   |	|——README.md      // explain correct patches         
   |——TBar
   |	|——correct_patches
   |	|——plausible_patches
   |	|——README.md      // explain correct patches
   |——README.md                 
```
