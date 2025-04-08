```markdown
# 🎢 Roller Coaster Dataset Project

## 🧹 Data Cleaning Summary

This project involves cleaning and preparing a roller coaster dataset for analysis using Python and pandas.

### ✅ Cleaning Steps

1. **Load the Dataset**

   ```python
   import pandas as pd
   df = pd.read_csv("roller_coasters.csv")
   ```

2. **Initial Data Inspection**

   ```python
   df.head()
   df.info()
   df.describe()
   df.columns
   ```

3. **Rename Columns for Consistency**

   ```python
   df.columns = df.columns.str.strip().str.replace(' ', '_').str.replace('(', '').str.replace(')', '')
   ```

4. **Drop Unnecessary Columns**

   ```python
   columns_to_drop = ['status', 'Opening_Date', 'Type', 'Design', 'Park', 'City', 'State', 'Country']
   df.drop(columns=columns_to_drop, inplace=True, errors='ignore')
   ```

5. **Remove Duplicates**

   ```python
   df.drop_duplicates(inplace=True)
   ```

6. **Handle Missing Values**

   ```python
   df = df[df['Speed_mph'].notna()]
   df = df[df['height_ft'].notna()]
   ```

7. **Convert Data Types**

   ```python
   df['Year_Introduced'] = pd.to_numeric(df['Year_Introduced'], errors='coerce')
   df['Opening_Date'] = pd.to_datetime(df['Opening_Date'], errors='coerce')
   ```

8. **Split or Combine Columns (Optional)**

   ```python
   df[['Park', 'Country']] = df['Location'].str.split(',', expand=True)
   ```

9. **Standardize Text Columns**

   ```python
   df['Coaster_Name'] = df['Coaster_Name'].str.strip().str.title()
   df['Manufacturer'] = df['Manufacturer'].str.strip().str.title()
   ```

10. **Outlier and Range Checks (Optional)**

   ```python
   df[df['Speed_mph'] > 150]
   ```

11. **Save Cleaned Data**

   ```python
   df.to_csv("coaster_cleaned.csv", index=False)
   ```

---

## 📘 User Manual

This section helps you understand how to use the cleaned dataset for analysis.

### 🗂️ Dataset Overview

| Column Name       | Description                                |
|-------------------|--------------------------------------------|
| `Coaster_Name`    | Name of the roller coaster                 |
| `Location`        | Park or place where the coaster is located |
| `Manufacturer`    | Company that built the coaster             |
| `Year_Introduced` | Year the ride was introduced               |
| `latitude` / `longitude` | Geo-coordinates for mapping         |
| `Type_Main`       | Main type of the coaster (e.g., Steel)     |
| `Opening_Date`    | Opening date as a datetime object          |
| `Speed_mph`       | Speed in miles per hour                    |
| `height_ft`       | Height in feet                             |
| `Inversions`      | Number of loops or flips                   |
| `Gforce`          | Max G-force during the ride                |

---

### 🔧 How to Use the Dataset

#### 1. Load the Cleaned Data

```python
import pandas as pd
df = pd.read_csv("coaster_cleaned.csv")
```

#### 2. Explore the Data

```python
df.head()
df.info()
df.describe()
```

#### 3. Visualize Coaster Trends

**Top 10 Manufacturers by Count**

```python
df['Manufacturer'].value_counts().head(10).plot(kind='barh')
```

**Speed vs Height Scatter Plot**

```python
import seaborn as sns
sns.scatterplot(data=df, x='Speed_mph', y='height_ft', hue='Type_Main')
```

**Inversions Over Time**

```python
sns.lineplot(data=df.sort_values('Year_Introduced'), x='Year_Introduced', y='Inversions')
```

#### 4. Plot Locations on a Map

```python
import folium

m = folium.Map(location=[df['latitude'].mean(), df['longitude'].mean()], zoom_start=2)

for _, row in df.dropna(subset=['latitude', 'longitude']).iterrows():
    folium.Marker(
        location=[row['latitude'], row['longitude']],
        popup=row['Coaster_Name']
    ).add_to(m)

m.save("coaster_map.html")
```

---

### ⚠️ Tips

- Use `.dropna()` or `.fillna()` for handling missing data during analysis.
- Be cautious with outliers in `Speed_mph`, `height_ft`, and `Gforce`.
- Use `matplotlib`, `seaborn`, or `plotly` for data visualizations.

---

### 📁 Files Included

- `coaster_cleaned.csv` – Cleaned dataset
- `coaster_analysis.ipynb` – Jupyter notebook with analysis
- `README.md` – Project documentation and user manual

---

Feel free to explore, analyze, and visualize roller coaster data from around the world! 🎡✨
```

---

Let me know if you also want a **preview** of how this will look once rendered on GitHub, or if you'd like a downloadable version of it in `.md` format.
