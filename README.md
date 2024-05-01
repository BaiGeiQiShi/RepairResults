# Indivisible Bug Repair

## Overview
This repo contains the artifact materials for our paper Detecting, Creating, Repairing, and Understanding Indivisible Multi-Hunk Bugs accepted by FSE'24. The materials contained in this repo are particularly related to the evaluation of existing repair techniques on 105 indivisible bugs. There are 7 repair techniques involved in the experiment. Below we show the 7 techniques in different categories.

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

In addition to *README.md* (this file), the repo contains for each technique a directory 
containing the plausible and correct patches (if any) we generated using the technique. 
Please refer to the readme file in each directory for the explanation of the patches.

In addition to these results, we also created repos for installing, testing, and 
using the repair techniques for experiment replication. We prepared Dockerfiles
to facilitate the replication. Please see the repos below. We want to clarify that
these techniques are NOT developed by us. They have their own original repos created by
the authors. We created these repos only to help interested users to replicate our experiment.

## 1. AlphaRepair
AlphaRepair is a cloze-style APR approach that uses large pre-trained code models under a zero-shot
learning setting to generate patches. Please refer to [here](https://github.com/give-to/AlphaRepairAPI)
for experiment replication.

## 2. ARJA-e
ARJA-e is a genetic programming (GP) based program repair approach for Java. 
Please refer to [here](https://github.com/BaiGeiQiShi/ARJA-e-API.git) for experiment replication.

## 3. ITER
ITER is a neural program repair system with an original training and inference loop enabling advanced multi-location patches.
By the time we did the experiment, the source code of ITER was not publicly available. Thanks to the help of [He Ye](https://www.kth.se/profile/heye), we obtained the ITER tool privately. We do not want to make the private ITER tool available, and hence, we do not provide a replication experiment. The official ITER tool is now available [here](https://github.com/ASSERT-KTH/ITER.git).

## 4. Hercules
Hercules detects evolutionary siblings and fixes them simultaneously for bug repair.
Please refer to [here](https://github.com/give-to/Hercules) for experiment replication.

## 5. TBar
TBar uses a set of pre-defined templates for bug repair.
Please refer to [here](https://github.com/give-to/TBarAPI.git) for experiment replication.

## 6. Recoder
Recoder is an NMT-based approach that uses a syntax-guided edit decoder for patch generation. 
Please refer to [here](https://github.com/BaiGeiQiShi/RecoderAPI.git) for experiment replication.

## 7. SimFix
SimFix leverages exisiting patches from other projects and similar code snippets in the same project to generate patches. 
Please refer to [here](https://github.com/BaiGeiQiShi/SimFixAPI.git) for experiment replication.

## Repo Structure
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
