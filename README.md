# Data Analysis and Visualization with Titanic Dataset

**This guide provides a comprehensive overview of data cleaning and exploratory data analysis (EDA) using the Titanic dataset. We will load the dataset, clean the data, and perform EDA to explore relationships and patterns within the data. This analysis includes visualizations using matplotlib and seaborn.**

## Table of Contents

  1. Setup
  2. Data Loading
  3. Data Cleaning
  4. Exploratory Data Analysis (EDA)
  5. Visualizations

## Setup

Ensure you have the required libraries installed. You can install them using pip:

```sh
pip install pandas numpy matplotlib seaborn
```

## Data Loading

Load the dataset from an Excel file. Ensure the file path is correct.

```sh
import pandas as pd
filepath = "/home/pulicherla/Documents/titanic.xlsx"
df = pd.read_excel(filepath)
print(df.head())
```

## Data Cleaning

**Checking for Missing Values**

Identify missing values in the dataset.

```sh
print(df.isnull().sum())
```

**Handling Missing Values**

Fill missing values using different strategies based on the context of the data.

```sh
# Filling missing values with a specific value
df_filled = df.fillna({'Age': 20, 'Cabin': 'E105'})
print(df_filled.head())

# Filling missing values with the mean value for the 'Age' column
df['Age'] = df['Age'].fillna(df['Age'].mean())
print(df['Age'].head())
```
**Removing Duplicates**

Remove duplicate rows from the dataset.

```sh
df = df.drop_duplicates()
print(df.head())
```

## Exploratory Data Analysis (EDA)

**Summary Statistics**

Get summary statistics of the dataset.

```sh
print(df.describe())
```

**Univariate Analysis**

Analyze individual variables like Age.

```sh
import matplotlib.pyplot as plt
import seaborn as sns

# Distribution of Age
plt.figure(figsize=(10, 6))
sns.histplot(df['Age'], bins=30, kde=True)
plt.title('Distribution of Age')
plt.show()

# Countplot for Survived
plt.figure(figsize=(10, 6))
sns.countplot(x='Survived', data=df)
plt.title('Count of Survived')
plt.show()
```

**Bivariate Analysis**

Explore relationships between two variables, such as Survived and Pclass.

```sh
# Survival rate by Sex
plt.figure(figsize=(10, 6))
sns.barplot(x='Sex', y='Survived', data=df)
plt.title('Survival Rate by Sex')
plt.show()

# Survival rate by Pclass
plt.figure(figsize=(10, 6))
sns.barplot(x='Pclass', y='Survived', data=df)
plt.title('Survival Rate by Pclass')
plt.show()
```

## Visualizations

Create various plots to visualize the data.

**Subplots for Age Data**

```sh
# Create subplots
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(12, 6))

# Bar plot for Age
age_counts = df['Age'].value_counts().sort_index()
axes[0].bar(age_counts.index, age_counts.values, color='brown')
axes[0].set_xlabel("Age")
axes[0].set_ylabel("Frequency")
axes[0].set_title("Visualize the Age Data Using Bar Graphs")

# Histogram for Age
age_data = df['Age'].dropna()
axes[1].hist(age_data, bins=20, color='skyblue')
axes[1].set_title('Visualize the Age Data Using Histograms')
axes[1].set_xlabel('Age')
axes[1].set_ylabel('Frequency')
plt.show()
```

**Scatter Plot and Bar Plot**

```sh
# Scatter Plot: Age vs. Fare
fig, axes = plt.subplots(1, 2, figsize=(14, 6))
sns.scatterplot(x='Age', y='Fare', hue='Survived', data=df, palette='dark', ax=axes[0])
axes[0].set_title('Scatter Plot of Age vs Fare')
axes[0].set_xlabel('Age')
axes[0].set_ylabel('Fare')

# Bar plot for Age vs. Fare
sns.barplot(x='Age', y='Fare', hue='Survived', data=df, ax=axes[1])
axes[1].set_title('Bar Plot of Age vs Fare')
axes[1].set_xlabel('Age')
axes[1].set_ylabel('Fare')
plt.show()
```

**Pairplot**

```sh
sns.pairplot(df[['Age', 'Fare', 'Pclass', 'Survived']], hue='Survived', palette='dark')
plt.suptitle('Pairplot of Selected Variables', y=1.02)
plt.show()
```

**Violin Plot**

```sh
fig, ax = plt.subplots(figsize=(10, 6))
sns.violinplot(x='Pclass', y='Fare', hue='Survived', data=df, palette='dark', split=True, ax=ax)
ax.set_title('Violin Plot of Fare by Pclass')
ax.set_xlabel('Pclass')
ax.set_ylabel('Fare')
plt.tight_layout()
plt.show()
```

























