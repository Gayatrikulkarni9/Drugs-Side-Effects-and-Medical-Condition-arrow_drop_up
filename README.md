# Drugs-Side-Effects-and-Medical-Condition-arrow_drop_up

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from google.colab import files

try:
    df = pd.read_csv("drugs_side_effects_drugs_com Data.csv")
except FileNotFoundError:
    print("File not found. Please upload the 'drugs_side_effects_drugs_com Data.csv' file.")
    uploaded = files.upload()
    if uploaded:
        # Assuming the user uploads the correct file
        for fn in uploaded.keys():
            print(f'User uploaded file "{fn}" with length {len(uploaded[fn])} bytes')
            df = pd.read_csv(fn)
    else:
        print("No file was uploaded. Please upload the file to proceed.")
        df = None

if df is not None:
    print("Dataset loaded successfully.")

df = pd.read_csv("drugs_side_effects_drugs_com.csv")
print(df.head())
print(df.shape)


df.isnull().sum()

plt.figure(figsize=(8,5))
sns.histplot(df["rating"], bins=10, kde=True)
plt.title("Distribution of Drug Ratings")
plt.xlabel("Rating")
plt.ylabel("Frequency")
plt.show()






top_conditions = df["medical_condition"].value_counts().head(10)

plt.figure(figsize=(10,6))
top_conditions.plot(kind="bar")
plt.title("Top 10 Medical Conditions with Most Drugs")
plt.ylabel("Number of Drugs")
plt.show()




from collections import Counter
import re

def extract_effects(text):
    return [x.strip() for x in text.split(";")]

effects = df["side_effects"].apply(extract_effects).explode()
common_effects = effects.value_counts().head(10)

plt.figure(figsize=(10,6))
common_effects.plot(kind="bar")
plt.title("Top 10 Most Common Side Effects")
plt.ylabel("Count")
plt.show()


plt.figure(figsize=(12,6))
sns.boxplot(x="rx_otc", y="rating", data=df)
plt.title("Ratings Distribution: Rx vs OTC Drugs")
plt.show()


plt.figure(figsize=(10,6))
sns.heatmap(df.corr(numeric_only=True), annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap")
plt.show()














    
