# Healthcare-Predictions
## Overview
The dataset contains a comprehensive collection of electronic health records belonging to patients who have been diagnosed with a specific disease. cords comprise a detailed log of every aspect of the patient's medical history, including all diagnoses, symptoms, prescribed drug treatments, and medical tests that they have undergone. These health records comprise a detailed log of every aspect of the patient's medical history, including all diagnoses, symptoms, prescribed drug treatments, and medical tests that they have undergone. Each row represents a healthcare record/medical event for a patient and it includes a timestamp for each entry/event, thereby allowing for a chronological view of the patient's medical history.

The Data has mainly three columns
1) Patient-Uid - Unique Alphanumeric Identifier for a patient
2) Date - Date when the patient encountered the event.
3) Incident - This column describes which event occurred on the day.

There are total 27K unique patients present in train.parquet
Similar to drug_type_7, there is also a drug called ‘Target Drug”, this drug is of interest for the assignment, there are total 9K patients in train.parquet who have taken “Target Drug” at least once.

### Prediction - 1
### Aim
The goal is to develop a predictive model that can determine whether a patient will be eligible for the "Target Drug" within the next 30 days based on their medical history.
### Solution Approach:
#### 1. Data Preprocessing:
* Load the training dataset (train.parquet) and perform necessary preprocessing steps such as handling missing values, converting data types, and handling categorical variables.
* Create a positive set consisting of patients who have taken the "Target Drug" at least once, considering the time aspect.
* Create a negative set of patients who have not taken the "Target Drug" within the next 30 days after their first prescription.
* Split the data into training and validation sets.
#### 2. Model Development:
* Choose an appropriate machine learning algorithm (e.g., logistic regression, random forest, gradient boosting) for classification.
* Train the model using the training dataset and evaluate its performance on the validation set.
* Fine-tune the model parameters, if required, to improve its performance.
#### 3. Evaluation:
* Evaluate the model's performance using appropriate evaluation metrics such as F1-score.
#### 4. Predictions and Submission:
* Apply the trained model to the test dataset (test.parquet) to generate predictions for each patient.
* Label each patient in the test dataset as 1 or 0 using the predictive model.
* Prepare the final submission file (final_submission.csv) containing the patient UIDs and corresponding predictions.

### Prediction - 2
### Aim
To analyze the drop-off rate for "Target Drug" and identify the events driving
patients to stop taking the drug.
### Solution Approach:
#### 1. Calculate the drop-off rate:
* Extracting the relevant columns from the dataset, including "Patient-Uid" and "Date" for drop-off events
* Filtering the data to include only patients who have taken the "Target Drug" at least once.
* Group the data by month and count the number of unique patients who dropped off within each month.
* Calculating the drop-off rate by dividing the number of drop- offs by the total number of patients who started the treatment in each month.
#### 2. Analyze events driving drop-offs:
* Identify the adverse events or other relevant columns in the dataset that might indicate the reasons for drop-offs.
* Extracting the necessary columns for analysis, including "Patient-Uid", "Date", and the relevant event columns.
* Filtering the data to include only patients who dropped off the treatment.
* Analyzing the occurrence and patterns of events leading to drop-offs, such as adverse events or specific conditions.

### Prediction - 3 
A drug is generally administered to a patient in certain patterns or at regular intervals of time. For example, Chemotherapy which is a drug treatment in the case of Cancer is generally given to patients at an interval of 3-4 weeks, i.e. every 3-4 weeks patients are administered the drug. Similarly to Chemotherapy, a “Target Drug” is also administered/prescribed in certain patterns, we want to analyze in what patterns the “Target Drug“ is administered/prescribed to patients, there might be multiple patterns in which “Target Drug” is administered/prescribed, come up with an analysis which to extract the dominant patterns in the data using clustering or other unsupervised techniques. Visualize the prescription patterns with time on X-axis (month) and prescriptions on Y-axis for each of the patterns you are able to extract(Below is an example of a prescription pattern, where a prescription is made at least once in the first two months followed by one prescription for every two months).
### Aim
To analyze the prescription patterns of the "Target Drug" and extract dominant patterns using clustering or other unsupervised techniques.
### Solution Approach:
#### 1. Data Preparation:
* The dataset is loaded from training dataset (train.parquet) and the 'Date' column is converted to a datetime format.
* The 'Month' column is extracted from the 'Date' column to represent the month component of the dates.
#### 2. Pattern Extraction:
* The dataset is grouped by both 'Patient-Uid' and 'Month' columns.
* The number of prescriptions for each group is counted, resulting in a DataFrame with columns 'Patient-Uid', 'Month', and 'Prescriptions'.
* The grouped DataFrame is further grouped by 'Month' to calculate the average number of prescriptions per month.
#### 3. Visualization:
* A figure is created, and a violin plot is generated to visualize the distribution of prescriptions for each month.
* A strip plot is added on top of the violin plot to display individual prescription data points.
* A line plot is created to show the average number of prescriptions per month.
* Axes labels, a title, and a legend are added to the plot.
