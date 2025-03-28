# Project_Avi

# **README: Aviation Risk Analysis Code Explanation**

## **Project Overview**
This project analyzes aviation accident data to identify the safest aircraft models for commercial and private use. The analysis includes data cleaning, visualization, and risk assessment using Python. The insights are then used to create a Tableau dashboard for decision-making.

---

## **Code Breakdown**

### **1. Importing Required Libraries**
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```
- `pandas` is used for data manipulation and analysis.
- `matplotlib.pyplot` and `seaborn` are used for data visualization.

---

### **2. Loading the Dataset**
```python
df = pd.read_csv("aviation_data.csv")
df.head()
```
- Reads the dataset into a DataFrame.
- Displays the first few rows for a quick preview.

---

### **3. Data Cleaning**
```python
df.isna().sum()
df.fillna("Unknown", inplace=True)
df.drop_duplicates(inplace=True)
```
- Identifies missing values.
- Fills missing values with "Unknown" to avoid analysis errors.
- Removes duplicate rows to ensure data integrity.

---

### **4. Exploring Broad Phase of Flight Accidents**
```python
flight_phase_counts = df['Broad.phase.of.flight'].value_counts()
plt.figure(figsize=(10, 5))
plt.bar(flight_phase_counts.index, flight_phase_counts.values, color="steelblue")
plt.xticks(rotation=45)
plt.title("Accidents by Flight Phase")
plt.xlabel("Flight Phase")
plt.ylabel("Number of Accidents")
plt.show()
```
- Counts the number of accidents per flight phase.
- Visualizes accident frequency in different phases (e.g., Takeoff, Landing).

---

### **5. Aircraft Damage by Weather Condition**
```python
df.groupby('Weather.Condition')['Aircraft.damage'].value_counts().unstack().plot(kind='bar', stacked=True, figsize=(12,6))
plt.title("Aircraft Damage by Weather Condition")
plt.xlabel("Weather Condition")
plt.ylabel("Count")
plt.show()
```
- Groups aircraft damage occurrences based on weather conditions.
- Creates a stacked bar chart to show how weather impacts aircraft damage.

---

### **6. Total Casualties per Aircraft Type**
```python
df['Total.Casualties'] = df['Total.Fatal.Injuries'] + df['Total.Serious.Injuries'] + df['Total.Minor.Injuries']
casualty_data = df.groupby('Make')['Total.Casualties'].sum().sort_values(ascending=False)
casualty_data.plot(kind='bar', figsize=(12,6), color='red')
plt.title("Total Casualties per Aircraft Type")
plt.xlabel("Aircraft Make")
plt.ylabel("Total Casualties")
plt.show()
```
- Calculates total casualties by summing fatalities, serious injuries, and minor injuries.
- Groups the data by aircraft manufacturer.
- Displays a bar chart showing which aircraft models have the most casualties.

---

### **7. Filtering Low-Risk Aircraft Models**
```python
safe_aircraft = df.groupby(['Make', 'Model'])['Total.Fatal.Injuries'].sum().sort_values()
print(safe_aircraft.head(10))
```
- Identifies aircraft models with the **lowest fatal injuries**, suggesting them as safer choices.

---

### **8. Exporting Cleaned Data for Tableau**
```python
df.to_csv("cleaned_aviation_data.csv", index=False)
```
- Saves the cleaned and processed data to a new CSV file for use in Tableau.

![Tableau Dashboard](image.png)

**[view interactive dashboard](https://public.tableau.com/app/profile/olin.wachira/viz/Project_Dt/Dashboard1?publish=yes)**
---

## **Summary of Insights**
- **Most accidents occur during Takeoff & Landing.**
- **Certain aircraft models are safer based on casualty data.**
- **Weather conditions significantly impact aircraft damage.**
- **Data-driven decision-making can help choose low-risk aircraft.**



