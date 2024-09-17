# 🎓✨ ECE Board Exam Data Wrangling & Visualization Project ✨🎓

**Author**: Chance Angelo Tan

Welcome to the **ECE Board Exam Problem** project, where we leverage Python for data wrangling and visualization. This repository houses the code that cleans, processes, and visualizes data to uncover insights into how factors like **track**, **gender**, and **hometown** influence the **average grade**. Dive in and explore the power of data! 🚀

---

## 📝 Project Overview

### 📋 **Problem Description**

#### **Intended Learning Outcomes**
- Recognize the functions necessary for effective **data cleaning** and **visualization**.
- Employ various Python codes for sophisticated **data wrangling** and **visualization**.

#### **Instructions**
- Access the dataset: [ECE Board Exam 2 Dataset](https://bit.ly/ECEBoardExamDataset) 🗂️.
- Utilize data wrangling and visualization techniques to present:
  - **Data frames** 📝
  - **Visualizations** 📊 derived from the dataset.

---

## 📈 Data Wrangling & Visualizations

### **Objective**

Tackle these two problems:

#### **Problem 1: Data Frame Creation**
1. **Instru Data Frame**: Filter students from Luzon in the **Instrumentation track** with Electronics grades > 70.
   - **Columns**: Name, GEAS, Electronics > 70
2. **Mindy Data Frame**: Select **female students** from **Mindanao** with an average score ≥ 55.
   - **Columns**: Name, Track, Electronics, Average ≥ 55

#### **Problem 2: Visualization Generation**
Analyze how **track**, **gender**, and **hometown** influence average grades using bar plots to identify factors contributing to student success.

---

## ⚙️ Setup & Installation

To execute the Python scripts for data wrangling/visualization, follow these steps:

1. **Clone the repository**:
   git clone https://github.com/yourusername/yourrepo.git

2. **Install Dependencies**:
   pip install pandas matplotlib seaborn

3. **Run the Jupyter Notebook**
   jupyter notebook




import pandas as pd

df = pd.read_csv('board2.csv')

# Filter for Instrumentation track students
df_instru = df.loc[
    (df['Electronics'] > 70) & 
    (df['Track'] == 'Instrumentation') & 
    (df['Hometown'] == 'Luzon'),
    ['Name', 'Electronics', 'GEAS']
]

# Calculate average for all students
df['Average'] = df[['Electronics', 'GEAS', 'Math', 'Communication']].mean(axis=1)

# Filter for Mindanao female students
df_mindy = df.loc[
    (df['Average'] >= 55) & 
    (df['Gender'] == 'Female') & 
    (df['Hometown'] == 'Mindanao'),
    ['Name', 'Track', 'Electronics', 'Average']
]

df_mindy.head()


import matplotlib.pyplot as plt
import seaborn as sns

# Calculate averages
track_avg = df.groupby('Track')['Average'].mean()
gender_avg = df.groupby('Gender')['Average'].mean()
hometown_avg = df.groupby('Hometown')['Average'].mean()

# Plot configurations
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
