## Objectives
Hospital readmission is an important indicator of quality of care and contributes substantially to total
medical expenditure. With diabetes prevalent in 11.6% of the U.S population (Centers for Disease Control
and Prevention, 2022), the need to effectively manage and mitigate readmission among diabetic patients is
crucial. Our project focuses on leveraging predictive and prescriptive machine learning models to uncover
insights to enhance overall management of diabetes care and reduce the burden of readmission for patients
and the healthcare system.

## Data
Our analysis utilizes a dataset from the UC Irvine Machine Learning Repository, encompassing ten years
of clinical care (1999-2008) across 130 hospitals and healthcare networks in the United States. The dataset
comprises 101,766 entries, each representing a diabetic patient who stayed for up to 14 days in the hospital.

Originally, the dataset featured a multi-class target variable for readmission,
categorized as within 30 days, post-30 days, or not readmitted at all. We converted this into a binary
classification, focusing on whether patients were simply readmitted or not, for analytical clarity and a more
focused examination of the critical issue of hospital readmissions.

## Feature Engineering
We undertook several feature engineering steps to refine our data for more effective and maintain
interpretability. The key changes we implemented are as follows:

1. Target Variable: 'Readmitted' was transformed into a binary classification, with 0 representing
'not readmitted' and 1 for 'readmitted'.
2. Medications: Initially comprising 22 medication columns with varying dosage statuses ('up',
'down', 'steady', 'no'), we grouped these into 6 broader categories based on dosage status:
Biguanides, Sulfonylureas, Meglitinides, Thiazolidinediones, Alpha-glucosidase Inhibitors, and
Insulin & Combination Products.
3. Primary Diagnosis: We focused on the primary diagnosis column 'diag1' and condensed it into 10
broader categories.
4. Age: Shifted from categorical age groups (ex. 20-30, 30-40) to a continuous variable using median
ages of each group.
5. Admission Type: Reduced into 5 distinct groups.
6. Admission Sources: Reduced into 6 distinct groups.
7. Discharge Disposition: Reduced into 7 distinct groups.

## Predictive Modeling
To identify key drivers of readmission among diabetic patients, we built five predictive models:
1. Sparse Logistic Regression
2. CART
3. Random Forest
4. Optimal Classification Tree
5. XGBoost
   
Our dataset includes patients, each identified by a unique patient ID, with multiple inpatient visits recorded
as separate rows. To prevent data leakage, we employed Sklearn’s GroupShuffleSplit function in our
train/test split.


## Prescriptive Modeling
In the second stage of our project, we developed an Optimal Policy Tree to provide optimal medication
prescription guidelines aimed at reducing readmissions. Our
dataset contained 22 medication columns by dosage status, and we considered each column as a separate
treatment. This led to 257 distinct treatment combinations within the training set. To improve
interpretability, we narrowed our focus to the top 10 treatment combinations and applied the same criteria
to the test set for consistency. The top 10 treatment combinations still covered approximately 76.86% of
the original training set and 77.05% of the original testing set.

Utilizing these filtered datasets, we constructed reward estimators using both the Doubly Robust method
and the Direct Method. This strategy allowed us to focus on a manageable subset of treatment combinations
while still capturing a significant proportion of patients and data.


## Results

Analyzing the top features across the predictive models, the number of inpatient visits, the number of
diagnoses, and the number of emergency visits are consistently the most predictive of hospital readmission. 

In both the doubly-robust and direct method trees, the model is very conservative in modifying existing medication dosages, 
and it reflects a commonapproach where new medications are introduced after a hospital visit, instead of adjusting existing ones. It
also aligns with common prescription patterns, where well-established and foundational medications like
Metformin and Insulin are usually initiated first before considering other medications.

Our predictive and prescriptive models suggest that high healthcare utilization by patients, their overall
case complexity, and the continued management of their diabetes are all integral factors in predicting
hospital readmission. These insights stress the need for improved follow-up care for patients and better
management of complex cases, especially for transferred patients.
