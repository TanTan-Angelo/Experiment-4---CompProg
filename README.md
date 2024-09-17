# 🎓✨ ECE Board Exam Data Wrangling & Visualization Project ✨🎓

**Author**: Chance Angelo Tan

Welcome to my project for the **ECE Board Exam Problem** using data wrangling and visualization techniques with Python. This repository contains the code that cleans, processes, and visualizes data from the provided dataset. Along with this, I've also created various visualizations to understand how different features (like **track**, **gender**, and **hometown**) contribute to the **average grade**. 🚀

---

## 📋 Problem Description 📋

### **Intended Learning Outcomes**:
1. Identify the codes and functions needed in **cleaning** and **visualizing** data.
2. Apply and use different codes in creating a Python program for **data wrangling** and **data visualization**.

### **Instructions**:
- Download the dataset from: [ECE Board Exam 2 Dataset](https://bit.ly/ECEBoardExamDataset) 🗂️.
- Analyze the data using data wrangling and visualization techniques to present different:
   1. **Data frames** 📝.
   2. **Visualizations** 📊 based on the dataset.

---

## 📊✨ Data Wrangling & Visualizations ✨📊

The goal is to solve two problems:

### **Problem 1: Create Data Frames**:
1. **Instru Data Frame**: Filter students from Luzon in the **Instrumentation track** with Electronics grades above 70.
   - **Columns**: Name, GEAS, Electronics > 70.
2. **Mindy Data Frame**: Filter **female students** from **Mindanao** with an average score greater than or equal to 55.
   - **Columns**: Name, Track, Electronics, Average ≥ 55.

### **Problem 2: Create Visualizations**:
Explore how **track**, **gender**, and **hometown** contribute to a higher **average grade**. The visualization compares these categories using bar plots to understand which factors contribute more to students’ success.

---

## 🛠️ Setup & Installation 🛠️

To run the Python scripts and view the data wrangling/visualization:
1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/yourrepo.git
    ```
2. Install dependencies:
    ```bash
    pip install pandas matplotlib seaborn
    ```
3. Run the Jupyter Notebook or Python scripts:
    ```bash
    jupyter notebook
    ```

---

## 🔍 Data Wrangling & Analysis 🔍

### **Sample Data Wrangling Code**:

import pandas as pd

df = pd.read_csv('board2.csv')

df_instru = df.loc[
    (df['Electronics'] > 70) & 
    (df['Track'] == 'Instrumentation') & 
    (df['Hometown'] == 'Luzon'),
    ['Name', 'Electronics', 'GEAS']
]

df['Average'] = df[['Electronics', 'GEAS', 'Math', 'Communication']].mean(axis=1)


df_mindy = df.loc[
    (df['Average'] >= 55) & 
    (df['Gender'] == 'Female') & 
    (df['Hometown'] == 'Mindanao'),
    ['Name', 'Track', 'Electronics', 'Average']
]

df_mindy.head()





import matplotlib.pyplot as plt
import seaborn as sns


track_avg = df.groupby('Track')['Average'].mean()
gender_avg = df.groupby('Gender')['Average'].mean()
hometown_avg = df.groupby('Hometown')['Average'].mean()


plt.figure(figsize=(20, 10))


plt.subplot(1, 3, 1)
plt.bar(track_avg.index, track_avg.values, color='lightblue')
plt.title('Average Grade by Track')
plt.xticks(rotation=45)
plt.ylabel('Average Grade')


plt.subplot(1, 3, 2)
plt.bar(gender_avg.index, gender_avg.values, color='lightgreen')
plt.title('Average Grade by Gender')
plt.ylabel('Average Grade')


plt.subplot(1, 3, 3)
plt.bar(hometown_avg.index, hometown_avg.values, color='lightcoral')
plt.title('Average Grade by Hometown')
plt.ylabel('Average Grade')

plt.tight_layout()
plt.show()
