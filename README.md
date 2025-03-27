# DemographicConfoundmentCXR
This repository contains the notebooks and resources for our manuscript "Confounding Effects of Demographic and Disease Variables on AI-Based Race Detection in Chest X-rays". Specifically, this repository contains the training and validation notebooks for Deep Learning models trained to classify demographic variables (age, sex, race) on the MIMIC and CheXpert publicly available datasets. In addition, it holds the notebooks used to assess the susceptibilty to confoundment by our trained demographic classifying models with respect to other demographic variables and disease labels.

# Data Availability
This study utilizes two publicly available chest X-ray datasets. The CheXpert dataset can be accessed by signing a data use agreement and following the instructions at https://stanfordmlgroup.github.io/competitions/chexpert/. Similarly, the MIMIC-CXR dataset requires signing a data use agreement and completing a credentialing process, with access details available at https://physionet.org/content/mimic-cxr/2.0.0/.

# Model Training and Validation
The dataset splits and model training code for the MIMIC and CheXpert-trained models can be found in the MIMIC_Model_Training and CheXpert_Model_Training folders. The labeling schemes were based on the work of Seyyed-Kalantari et al.* and Gichoya et al.** Each dataset was divided into a 70/10/20 train-validation-test split for each demographic variable (race, age, sex). A separate ResNet34 classification model was trained for each variable within each dataset. The trained models were then evaluated on both datasets, with the evaluation code located in the 'Testing on MIMIC Data' and 'Testing on CheXpert Data' folders. The predicted probabilities for each class, along with the model results, were saved as CSV files for confounding analysis.

# Confounding Analysis
Confounding analysis examines whether a model trained to classify one demographic variable (e.g., race) is inadvertently influenced by another (e.g., sex or age). This is done by modifying the dataset’s demographic distributions and observing changes in model performance.

The procedure involves the following steps:
1. Subset the test data based on a primary demographic attribute (e.g., race, sex, or age).
2. Introduce bias in the dataset by systematically altering the proportion of certain demographic groups (e.g., increasing or decreasing the representation of White individuals, females, or specific age groups). This is done using functions like create_race_biased_test_set and create_sex_biased_test_set, which artificially modify demographic distributions.
3. Evaluate classifiers using AUCROC on the modified datasets to measure the impact of demographic shifts on model predictions.
4. Repeat pipeline with respect to disease labels.
   
By applying this approach, we quantify the extent to which extraneous demographic attributes or disease states influence our demographic classifying models' outcomes.

![image](https://github.com/user-attachments/assets/7e0ce0d9-46a3-4b53-8fcb-42cbb4625fe5)


# Terminology Notes
In our documentation, we sometimes use the terms gender and sex interchangeably, though they are distinct concepts.
Similarly, race and ethnicity may be conflated at times. This is due to differences in how these categories were recorded in publicly available datasets.
Age categories are defined as follows:
0 → 0-20 years old; 
1 → 21-40 years old; 
2 → 41-60 years old; 
3 → 61-80 years old; 
4 → 81+ years old. 

Finally, throughout our variable names and documentation, the term 'bias' is occasionally used. However, after further consideration, we have decided to adopt the term 'skew' to more accurately reflect the intent of our procedures. This change is reflected in our manuscript.

*Seyyed-Kalantari L, Zhang H, McDermott MBA, Chen IY, Ghassemi M. Underdiagnosis bias of artificial intelligence algorithms applied to chest radiographs in under-served patient populations. Nat Med. 2021;27(12):2176-2182. doi:10.1038/s41591-021-01595-0
**Gichoya JW, Banerjee I, Bhimireddy AR, et al. AI recognition of patient race in medical imaging: a modelling study. Lancet Digit Health. 2022;4(6):e406-e414. doi:10.1016/S2589-7500(22)00063-2
