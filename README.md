# Google-Play-Store-EDA

## Overview

This project performs **Exploratory Data Analysis (EDA)** on the Google Play Store dataset containing **10,841 apps**. The analysis covers data cleaning, feature engineering, univariate and bivariate analysis, and answers key business questions about app categories, installations, ratings, and pricing.

---

## Dataset

| Detail | Info |
|---|---|
| **Source** | [Google Play Store Dataset](https://raw.githubusercontent.com/krishnaik06/playstore-Dataset/main/googleplaystore.csv) |
| **Records** | 10,841 apps |
| **Columns** | 16 (after cleaning) |

### Features

| Column | Description |
|---|---|
| App | Name of the app |
| Category | Category the app belongs to |
| Rating | App rating on Play Store (out of 5) |
| Reviews | Number of user reviews |
| Size | Size of the app |
| Installs | Number of installs |
| Type | Free or Paid |
| Price | Price of the app (0 if Free) |
| Content Rating | Target audience (Everyone, Teen, etc.) |
| Genres | Genre of the app |
| Last Updated | Date the app was last updated |
| Current Ver | Current version of the app |
| Android Ver | Minimum Android version required |
| Day | Day extracted from Last Updated |
| Month | Month extracted from Last Updated |
| Year | Year extracted from Last Updated |

---

## Libraries Used

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

---

## Steps Followed

### 1. Data Loading & Initial Exploration
- Loaded dataset from GitHub raw URL using `pd.read_csv()`
- Checked shape, info, dtypes using `.shape`, `.info()`, `.describe()`
- Identified missing values using `.isnull().sum()`

### 2. Data Cleaning

**Reviews Column:**
- Detected 1 non-numeric value (`3.0M`) using `str.isnumeric()`
- Dropped the faulty record at index 10472
- Converted datatype to `int`

**Size Column:**
- Replaced `M` with `000` to convert MB values to KB units
- Removed `K` suffix
- Replaced `'Varies with device'` with `NaN`
- Used `pd.to_numeric(errors='coerce')` to safely handle invalid entries
- Converted to `float`

**Installs & Price Columns:**
- Removed special characters `+`, `,`, `$` using string replacement loop
- Converted Installs to `int` and Price to `float`

**Last Updated Column:**
- Converted to `datetime` using `pd.to_datetime()`
- Extracted 3 new columns: `Day`, `Month`, `Year`

**Duplicates:**
- Found and removed duplicate app records using `drop_duplicates(subset=['App'], keep='first')`

### 3. Feature Engineering
- Created `Day`, `Month`, `Year` columns from `Last Updated`
- Saved cleaned dataframe to `google_cleaned.csv`

### 4. EDA — Univariate Analysis
- Identified numeric and categorical features programmatically
- **Numeric features:** KDE plots for distribution analysis
- **Categorical features:** Count plots for Type and Content Rating

**Univariate Analysis of Numerical Features:**

<img width="1498" height="1505" alt="Image" src="https://github.com/user-attachments/assets/76a05e1d-f2d4-4015-a9ac-611ddfdee319" />

**Observations from Numerical KDE plots:**
- **Rating** — left-skewed, most apps rated between 4.0–5.0
- **Reviews, Size, Installs, Price** — right-skewed → outliers present
- **Year** — majority of apps last updated in **2017–2018**
- **Month** — updates peak around **July (month 7)**

**Univariate Analysis of Categorical Features:**

<img width="1600" height="676" alt="Image" src="https://github.com/user-attachments/assets/8a3df831-1c14-4d0f-ba8f-c494f3dbac4c" />

**Observations from Categorical plots:**
- **~10,000** apps are **Free** vs ~800 Paid
- **Everyone** is the dominant Content Rating with ~9,000+ apps

### 5. EDA — Key Questions Answered

**Q1. Which is the most popular app category?**

**Pie Chart — Category Distribution:**

<img width="1300" height="1182" alt="Image" src="https://github.com/user-attachments/assets/71697d69-0627-473b-8bb5-66878796ed96" />

**Top 10 App Categories — Bar Chart:**

<img width="1247" height="661" alt="Image" src="https://github.com/user-attachments/assets/b46b7787-056c-4a1a-a3db-8ff6c5327f1e" />

**Q2. Which category has the largest number of installations?**

**Most Popular Categories by Installations (in Billions):**

<img width="1399" height="884" alt="Image" src="https://github.com/user-attachments/assets/5050d45f-81f5-4b23-9edd-77500a8f78fa" />

**Q3. What are the Top 5 most installed apps in each popular category?**

**Top 5 Apps in GAME, COMMUNICATION, PRODUCTIVITY, SOCIAL:**

<img width="1600" height="606" alt="Image" src="https://github.com/user-attachments/assets/b686ddcb-4e2e-49cd-b38e-56ecf5a731ae" />

**Q4. How many apps have a perfect 5-star rating?**
- Filtered apps with Rating == 5.0

---

## Key Insights

### App Categories
- **Family** category has the most apps — **19%** of total apps (~2,000 apps)
- **Game** is second with ~1,150 apps (**9.9%**)
- **Tools** is third with ~850 apps (**8.6%**)
- **Beauty** has the least apps — less than **1%**

### Installations
- **GAME** is the most installed category with **~14 Billion** installations
- **COMMUNICATION** is second with **~11 Billion** installations
- **TOOLS** is third with **~8 Billion** installations

### Top Apps per Category
| Category | Top Apps |
|---|---|
| Game | Subway Surfers, Candy Crush Saga, Pou, Temple Run 2, My Talking Tom |
| Communication | Skype, WhatsApp Messenger, Hangouts, Google Chrome, Gmail |
| Productivity | Google Drive, Microsoft Word, Google Calendar, Dropbox, Cloud Print |
| Social | Facebook, Google+, Instagram, Snapchat, Facebook Lite |

### Ratings
- **271 apps** have a perfect **5.0 rating**
- Top rated app: **CT Brain Interpretation** (Family category)

### App Type
- Majority of apps on Play Store are **Free**

---

## Files in this Repository

| File | Description |
|---|---|
| `GooglePlayStore.ipynb` | Jupyter Notebook with complete EDA code |
| `google_cleaned.csv` | Cleaned dataset saved after data cleaning steps |
| `README.md` | Project documentation |

---

## How to Run

1. Clone the repository:
```bash
git clone https://github.com/nikitajadhav0022-afk/Google-Play-Store-EDA.git
```

2. Install required libraries:
```bash
pip install pandas numpy matplotlib seaborn
```

3. Open the notebook:
```bash
jupyter notebook GooglePlayStore.ipynb
```

---

## Tools & Technologies

- Python 3
- Pandas — data manipulation
- NumPy — numerical operations
- Matplotlib — data visualization
- Seaborn — statistical visualizations
- Jupyter Notebook
