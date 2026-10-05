# Road Accident Data Cleaning & Risk Classification

## Table of Contents

- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools Used](#tools-used)
- [Tool - Work](#tool---work)
- [Data Cleaning & Preparation Steps](#data-cleaning--preparation-steps)
- [Results & Findings](#results--findings)
- [Recommendations](#recommendations)

## Project Overview

This project focuses on cleaning, standardizing, and preparing **State/UT-wise road accident data for 2016–2019** for further analysis.

The dataset contains information on:
- Total road accidents by year
- State/UT-wise accident rank for 2019
- Share of each State/UT in total road accidents
- Accidents per lakh population
- Accidents per 10,000 vehicles
- Accidents per 10,000 km of roads

The project also creates an **Accident Incidence Per Lakh Population** measure using the 2016–2019 population-adjusted accident rates and classifies States/UTs into:

- **High Risk**
- **Medium Risk**
- **Low Risk**

The primary objective was to transform the raw dataset into a **clean, consistent, analysis-ready dataset** while preserving unavailable values as null rather than treating them as zero.

## Data Source

**Dataset:** State/UT-wise Road Accident Data, 2016–2019

**Source file:** `RA2019_A2.csv` from data.gov.in

The raw dataset contained **37 rows and 21 columns**, including a total row that was removed during data preparation.

The cleaned dataset contains **36 State/UT-level records and 23 columns**, after cleaning and creation of analytical fields.

## Tools Used

| Tool | Purpose |
|---|---|
| **Microsoft Excel** | Initial table preparation, formatting, analytical calculations and conditional formatting |
| **Power Query** | Data cleaning, standardization, data-type conversion, error handling and rounding |
| **Excel Conditional Formatting** | Visual identification of High and Medium Risk categories |


## Tool - Work

| Tool | Work Performed |
|---|---|
| **Excel** | Converted raw data into a structured table and loaded it into Power Query |
| **Power Query** | Cleaned column names and standardized data |
| **Power Query** | Trimmed and standardized State/UT names |
| **Power Query** | Changed accident-count columns to Whole Number |
| **Power Query** | Changed population-adjusted accident measures to Decimal Number |
| **Power Query** | Removed the Total row |
| **Power Query** | Replaced unavailable-data errors with null |
| **Power Query** | Rounded share and decimal columns to 2 decimal places |
| **Excel** | Added `%` display formatting to accident-share columns |
| **Excel** | Calculated Accident Incidence Per Lakh Population |
| **Excel** | Created High/Medium/Low Risk classification |
| **Excel** | Applied conditional formatting to risk categories |

## Data Cleaning & Preparation Steps

### 1. Column Name Standardization

The original dataset contained several long and inconsistent column names.

Column names were shortened and standardized to make the dataset easier to work with.

Examples:

```text
State/UT-Wise Total Number of Road Accidents during 2016
↓
Road Accidents 2016

Total Number of Accidents Per Lakh Population - 2016
↓
Accidents/Lakh Population (2016)

State/UT-Wise Total Number of Road Accidents during 2019 - Rank
↓
Road Accident Rank (2019)
```

### 2. State/UT Text Cleaning

The `States/UTs` column was cleaned by:

- Removing unnecessary spaces
- Trimming text
- Standardizing capitalization
- Using consistent State/UT naming

### 3. Data Type Standardization

Appropriate data types were assigned to different variables.

| Variable | Data Type |
|---|---|
| State/UT | Text |
| Road Accidents | Whole Number |
| Accident Rank | Whole Number |
| Accident Share | Decimal Number |
| Accidents/Lakh Population | Decimal Number |
| Accidents/10K Vehicles | Decimal Number |
| Accidents/10K Km | Decimal Number |

### 4. Removal of Total Row

The source dataset contained a **Total** row in addition to the State/UT-level observations.

The Total row was filtered out so that the final dataset contained only State/UT-level records.

### 5. Handling Missing/Unavailable Data

Some indicators were unavailable for specific States/UTs.
The following unavailable values were preserved as **null** rather than being replaced with zero:
- **Telangana:** Accidents per Lakh Population for 2016–2019
- **Daman & Diu:** Accidents per 10K Vehicles for 2018–2019
This prevents missing information from being incorrectly interpreted as zero.

### 6. Accident Share Standardization

All columns representing the State/UT's share of total road accidents were rounded to **2 decimal places**.
The four share columns were:
- Accident Share – 2016
- Accident Share – 2017
- Accident Share – 2018
- Accident Share – 2019

After loading the cleaned data into Excel, custom number formatting was applied using:
```text
0.00"%"
```
This displays the percentage symbol while retaining the numeric value for analysis.

### 7. Decimal Standardization

Decimal-based indicator columns were rounded to **2 decimal places** for easier interpretation and presentation.

### 8. Accident Incidence Calculation

A new analytical column was created:

**`Accident Incidence Per Lakh Population`**

This represents the average accident incidence per lakh population across the available 2016–2019 observations.

The measure was used as the primary indicator for categorizing States/UTs according to accident incidence.

### 9. Risk Classification

States/UTs were classified into three risk categories based on accident incidence per lakh population:

| Accident Incidence | Risk Category |
|---:|---|
| **> 50** | High Risk |
| **25–50** | Medium Risk |
| **1–<25** | Low Risk |

Unavailable incidence values were not treated as zero.

### 10. Conditional Formatting

Excel conditional formatting was applied to the risk classification column:

- **High Risk** → Red
- **Medium Risk** → Yellow
- **Low Risk** → No high-risk warning formatting

This provides a quick visual understanding of the risk distribution.

## Results & Findings

### 1. Risk Classification

The cleaned dataset contains **36 State/UT-level records**.

Based on the calculated Accident Incidence Per Lakh Population:

| Risk Category | Number of States/UTs |
|---|---:|
| High Risk | **6** |
| Medium Risk | **5** |
| Low Risk | **25** |

This indicates that the majority of the observed State/UTs fall within the **Low Risk** category under the project's population-adjusted incidence classification.

### 2. States/UTs with Highest Accident Incidence

The highest average accident incidence values in the cleaned dataset include:

| State/UT | Average Accident Incidence |
|---|---:|
| Goa | **147.86** |
| Kerala | **84.58** |
| Tamil Nadu | **75.24** |
| Puducherry | **73.16** |
| Karnataka | **53.41** |
| Madhya Pradesh | **53.11** |

These States/UTs fall into the **High Risk** category according to the project's defined threshold.

### 3. Highest Total Number of Road Accidents in 2019

The States/UTs with the largest absolute number of road accidents in 2019 include:

| Rank | State/UT | Road Accidents – 2019 |
|---:|---|---:|
| 1 | Tamil Nadu | 57,228 |
| 2 | Madhya Pradesh | 50,669 |
| 3 | Uttar Pradesh | 42,572 |
| 4 | Kerala | 41,111 |
| 5 | Karnataka | 40,658 |

This demonstrates why **total accidents and accident incidence should not be interpreted as the same measure**.

A State can have a high total number of accidents because of its population and vehicle exposure, while a smaller State/UT can have a much higher population-adjusted accident incidence.

### 4. Risk Should Not Be Assessed Using Total Accidents Alone

The project demonstrates the difference between:

- **Absolute accident burden** — Total Road Accidents
- **National contribution** — Accident Share (%)
- **Population-adjusted incidence** — Accidents per Lakh Population
- **Vehicle-adjusted incidence** — Accidents per 10K Vehicles
- **Road-network-adjusted incidence** — Accidents per 10K Km of Roads

For identifying relative accident incidence across States/UTs, **Accidents per Lakh Population** provides a more useful normalized measure than simply comparing total accident counts.

## Recommendations

### 1. Use Multiple Indicators

Road accident risk should not be evaluated using a single metric.
Future analysis should consider:
- Accident incidence per lakh population
- Accidents per 10K vehicles
- Accidents per 10K km of roads
- Total accident volume
- Accident share
Using multiple indicators provides a more comprehensive assessment.

### 2. Prioritize High-Incidence States/UTs
States/UTs classified as **High Risk** should be prioritized for deeper investigation into:
- Road safety infrastructure
- Traffic management
- Vehicle density
- Road conditions
- Enforcement
- Accident-prone locations
The risk classification should be treated as a **screening indicator**, rather than a definitive measure of causation.

### 3. Preserve Missing Data Correctly
Unavailable values should remain **null/missing** rather than being converted to zero.
This prevents incorrect conclusions and preserves the distinction between:

### 4. Extend the Analysis
The cleaned dataset can be further developed into a road-safety dashboard containing:

- State/UT ranking
- Accident trends from 2016–2019
- Accident incidence
- Risk-category distribution
- Accident share
- Vehicle-adjusted accident rates
- Road-density-adjusted accident rates

This would allow policymakers and analysts to identify States/UTs requiring further road-safety investigation.

## Project Outcome

The raw road accident dataset was transformed into a **cleaned and analysis-ready dataset** through structured data preparation in Excel and Power Query.

## 📸 Data Cleaning: Before & After

### Before Cleaning

![Data Before Cleaning](Data%20Before%20Cleaning.png)

### After Cleaning

![Data After Cleaning](Data%20after%20Cleaning.png)

The project demonstrates practical skills in:

- Data cleaning
- Data standardization
- Power Query
- Data type management
- Missing-value handling
- Data validation
- Feature creation
- Conditional logic
- Risk classification
- Excel formatting
- Analytical data preparation

The final dataset is suitable for subsequent **exploratory data analysis, visualization, dashboard development, and road-safety risk analysis**.

### Author

Swasti
Data Analyst | Public Policy & Governance

This project combines data analytics and public-policy analysis to demonstrate how structured data cleaning can prepare government datasets for meaningful decision-making.
