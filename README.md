# sharks_attack_project
![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Project | Coastal Opportunity Analysis


## Overview

Project "Coastal Opportunity Analysis" analyzes global shark attack data to identify optimal geographic expansion opportunities for our water sports equipment business.

The core objective is to determine where high ocean activity and low fatality rates create strong revenue potential and high Customer Lifetime Value (CLV).


## Business Hypothesis

If we expand into markets with:

- High shark attack frequency (proxy for high ocean activity)
- Low fatality rates (indicating manageable risk and sustained participation)

Then sales will increase due to:

- Strong water sports participation
- Ongoing customer engagement
- Higher repeat purchase potential (CLV)

**Note**: The United States emerges as a primary market candidate under this framework.

## Dataset Description

This project uses the Shark Attack dataset, which includes global records of shark–human interactions.

Key variables that we considered for analysis are the following:

- Country/location
- Activity type (e.g., surfing, swimming, diving)
- Injury severity
- Fatal vs. non-fatal outcome
- Species involved (where available)

**Note**: The dataset enables geographic, temporal, and risk-level analysis.

## Data Cleaning & Preparation

To ensure accuracy and consistency, the following preprocessing steps were applied:

- Standardized country/location names

      df.columns = df.columns.str.strip().str.lower().str.replace(" ", "_")

- Normalized injury outcomes into binary fatal/non-fatal classification

      fatal_replacements = {"Y x 2": "Y", " N": "N", "Nq":"N", "M": np.nan, "F": np.nan, "2017": np.nan, "UNKNOWN": np.nan}
df["fatal_y/n"] = (df["fatal_y/n"].replace(fatal_replacements).str.strip().str.upper())
print(df["fatal_y/n"].value_counts(dropna = False))

- Grouped unstructured data into standardized categories

      fatality_rate = df.groupby('country')['fatal_numeric'].mean() * 100

      or

      def clean_activity(row):
          activity = row['Activity']  # Récupérer l'activité de la ligne
          if pd.isna(activity):  # Si la valeur est NaN, la laisser inchangée
              return row['activity_clean']
          if "swimming" in activity.lower():
              return "Swimming"
          elif "fishing" in activity.lower():
              return "Fishing"
          elif "surfing" in activity.lower():
              return "Surfing"
          elif "wading" in activity.lower():
              return "Wading"
          elif "Diving" in activity.lower():
              return "Diving"
          else:
              return row['activity_clean']
  
- Removed records with missing data

      fatality_rate = fatality_rate.dropna()

      or
      df = df.replace("?","")

- Cleaned text fields (lowercasing, trimming, removing special characters)

      df.loc[:, "country"] = df["country"].str.replace(r"[^a-z\s]", "", regex=True)


**Note**: These steps improved reliability for cross-country comparison and fatality rate analysis.

## Analytical Approach

1. Calculated shark incident frequency by country
2. Computed fatality rates per country
3. Identified high-incident, low-fatality markets
4. Evaluated expansion attractiveness based on:
- Activity volume (proxy for demand)
- Risk sustainability
- Potential CLV impact

## Key Insight

Markets with high shark activity but low fatality rates indicate:

- Strong ocean sports culture
- Sustained consumer participation
- Repeat equipment purchase potential
- Long-term revenue growth opportunity

**Note**: The United States ranks highly under this strategic model.

## Project Structure

1. /data
- https://www.sharkattackfile.net/spreadsheets/GSAF5.xls

2. /notebooks
-Shark Project.ipynb

4. README.md

## Tools

- Python
- Pandas
- NumPy
- Jupyter Notebook
- Google Cloud
- Excel

## Authors

Anne Leschallier de Lisle, Beatriz Fernandes, Francisca Andrade, Ofelia Akopian


Presentation



[Voir le Google Slides](https://docs.google.com/presentation/d/12ZLWrjnhwVKk2rFj-aXpakW4i4qqt_Bxq5F-MpGcfbk/edit?usp=sharing)
