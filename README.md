# Explanation-XAI4MTSC-evaluation-actionability

## Overview:
This repository contains the code used in the paper ["Improving the Evaluation and Actionability of
Explanation Methods for Multivariate Time Series Classification"](https://arxiv.org/abs/2406.12507) accepted at ECMLPKDD 2024.

The main paper as a pdf is also available in the repository.

To facilitate the use of the main results of the paper, we have also released a separate library [tsCaptum](https://github.com/mlgig/tscaptum) which adapts the main explanation methods for the scikit-learn / sktime / aeon classifiers along with the ***chunking strategy*** improvement used in the paper.

## Abstract:
Explanation for Multivariate Time Series Classification (MTSC) is an important topic that is under explored. There are very few quantitative evaluation methodologies and even fewer examples of actionable explanations, where the explanation methods are shown to objectively improve specific computational tasks on time series data. In this paper we focus on analyzing InterpretTime, a recent evaluation methodology for attribution methods applied  to MTSC. We reproduce the original paper results, showcase some significant weaknesses of the methodology and propose ideas to improve both its accuracy and efficiency. 
Unlike related work, we go beyond evaluation and also showcase the actionability of the produced explainer ranking, by using the best attribution methods for the task of channel 
selection in MTSC. We find that perturbation-based methods such as SHAP and Feature Ablation work well across a set of datasets, classifiers and tasks and outperform gradient-based methods.
We apply the best ranked explainers to channel selection for MTSC and show significant data size reduction and improved classifier accuracy.

## Results:
Table 8 which shows results for the vanilla InterpretTime results and Table 3 which shows the ground truth results (not included in the original InterpretTime work) are our baselines.

Table 5 shows results for our improved InterpretTime using ***multiple masks*** to perturb data other than $N(0,1)$, as done by the vanilla InterpretTime, and using the ***chunking*** technique, to adapt the explanation methods to Time Series e.g. by considering their locality. 
To be noted the metrics improvement especially for Average Precision (AP) and $AUC\tilde{S}_{top}$ while running time (same for both Table 8 and 3) has shrunk by at least 1 order of magnitude.

![image](https://github.com/mlgig/xai4mtsc_eval_actionability/blob/main/imgs/vanilla_interpretTime_results.png)


![image](https://github.com/mlgig/xai4mtsc_eval_actionability/blob/main/imgs/vanilla_gt_results.png)


![image](https://github.com/mlgig/xai4mtsc_eval_actionability/blob/main/imgs/our_method.png)

Table 7 shows results for our actionability experiment i.e. to have an alternative 
channel selection approach which uses the aggregated attribution to compute channel importance:

![image](https://github.com/mlgig/xai4mtsc_eval_actionability/blob/main/imgs/actionability.png)

## Code:

Code run using python 3.9.18, using the libraries listed in requirements_py3.9.18.txt file. 
Executable files are:

### train_models.py:
Script to train the models. Mandatory arguments are dataset (possible choices are CounterMovementJump, Military press along with synthetic and ECG data used in InterpretTime publication)
and classifier (possible choices are ResNet, dResNet, Rocket, MiniRocket and ConvTran). Optional field is concat i.e. whether to concatenate all channels to get a univariate time series.

### compare_explanations.py
Script used to run the ground truth methodology described in the paper on synthetic data.
No argument is required nut some assumptions are made as
saliency maps are in "explanations" folder" datasets are in "datasets" folder, etc.

### compute_attributions.py
Script to be used for computing the saliency maps.
At the top of the script a dictionary named captum_methods is defined to list the methods to be used (edit it if you want to remove/add methods)
Mandatory fields are datasets (same as before), classifiers (same as before) and ns_chunks i.e. which number of chunks (definition in the paper) to try. Use -1 to compute point-wise i.e. no chunking

### interpretTime.py
Script to be used to run interpretTime method. Some modifications were made for instance adding other masks, as specified in the paper, etc.
Only mandatory argument is datasets (same as before).

## Data:

### Datasets
To create a dir named datasets and place the content found here

https://drive.google.com/drive/folders/18tbVOkbac8Bvr8-8VZLf3fpzzJNc1vss?usp=drive_link

### Trained models
To create a dir named 'saved_models' and place the content found here

https://drive.google.com/drive/folders/1_Ld_6JFriAWLq18xRGzp-uxHOfrM5V5f?usp=drive_link

### Computed explanations
(optional) Saliency maps produced in our experiments, originally placed in a  dir named 'explanations'. Content can be found here 

https://drive.google.com/drive/folders/1B6NmIuekDVwyJxBZQX6uPOulc-_uGvPU?usp=drive_link

### InterpretTime outputs
(optional) Outputs produced in our experiments by InterpretTime, originally placed in a  dir named 'IntepretTime_results'. Content can be found here 

https://drive.google.com/drive/folders/1S4y9_R1S7ba5XTUBEpmqDT4E9eNHuP8b?usp=drive_link

## how to cite:
```
@misc{serramazza2024improving,
    title={Improving the Evaluation and Actionability of Explanation Methods for Multivariate Time Series Classification},
    author={Davide Italo Serramazza and Thach Le Nguyen and Georgiana Ifrim},
    year={2024},
    conference={ECMLPKDD}
    eprint={2406.12507},
    archivePrefix={arXiv},
    primaryClass={cs.LG}
}
```
