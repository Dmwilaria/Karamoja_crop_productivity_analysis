# Karamoja Crop Productivity & Food Security Analysis

## Overview

This project analyzes crop productivity across Karamoja to identify regions that should be prioritized for agricultural improvement programs.

## Business Understanding
Stakeholder: Ministry of Agriculture / Development Agencies

Key Questions:
- Which districts/subcounty have low production per capita?
- Where should intervention programs be prioritized?
- How do maize and sorghum yields compare?

## Data Understanding and Analysis

### Data Source
- Uganda subcounty and district shapefiles
- Yield and population datasets
- karamoja_subcounty_cleaned

### Description of Data
- POP: Total population
- S_Yield_Ha: Sorghum yield per hectare
- M_Yield_Ha: Maize yield per hectare
- Crop_Area_Ha: Total crop area



```python
### Key Visualizations

# Data manipulation
import pandas as pd
import numpy as np

# Visualization (for exploration)
import matplotlib.pyplot as plt
import seaborn as sns

# Load datasets
subcounty_df = pd.read_csv("D:\Python\DATA\DATA\TABLES/Uganda_Karamoja_Subcounty_Crop_Yield_Population.csv")
district_df = pd.read_csv("D:\Python\DATA\DATA\TABLES/Uganda_Karamoja_District_Crop_Yield_Population.csv")

# Subcounty level
subcounty_df["Total_Yield_Ha"] = ((subcounty_df["S_Prod_Tot"] + subcounty_df["M_Prod_Tot"])/ subcounty_df["Crop_Area_Ha"])
# District level
district_df["Total_Yield_Ha"] = ((district_df["S_Prod_Tot"] + district_df["M_Prod_Tot"])/ district_df["Crop_Area_Ha"])

#### 1. Yield Comparison

# Subcounty level

plt.figure(figsize=(6, 4))

plt.subplot(2, 1, 1)
plt.hist(subcounty_df["Total_Yield_Ha"], bins=10)
plt.title("Subcounty: Distribution of Total Yield per Hectare")
plt.grid(True)

plt.subplot(2, 1, 2)
plt.hist(district_df["Total_Yield_Ha"], bins=10)
plt.title("District: Distribution of Total Yield per Hectare")
plt.grid(True)

plt.tight_layout()
plt.show()

```


    
![png](output_1_0.png)
    



```python
# subcount level
sns.scatterplot(x="POP",y="Total_Yield_Ha",data=subcounty_df)
plt.title("Subcount level Population vs Yield")
plt.show()

# district level
sns.scatterplot(x="POP",y="Total_Yield_Ha",data=district_df)
plt.title("District level Population vs Yield")
plt.show()
```


    
![png](output_2_0.png)
    



    
![png](output_2_1.png)
    



```python
#### 2. Crop Area Heatmap

# Set District as index
heat_data = district_df.set_index("NAME")[["POP", "Total_Yield_Ha"]]

sns.heatmap(heat_data, annot=True)

plt.title("District-Level Population and Yield Heatmap")
plt.show()
```


    
![png](output_3_0.png)
    


## Conclusion

Key Findings:
1. Significant variation in production per capita across districts.
2. Crop performance varies regionally.
3. Land allocation does not always correlate with yield efficiency.

## Recommendations

1. Target low-performing districts with yield improvement programs.
2. Promote crop specialization.
3. Optimize land allocation using efficiency metrics.

## Future Work
- Include rainfall data.
- Develop predictive yield models.





```python

```
