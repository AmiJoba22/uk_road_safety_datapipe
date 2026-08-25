# Mapping and Modeling UK Road Safety

We are diving into the official **UK Road Safety Dataset** from the [UK Department for Transport](https://www.kaggle.com/datasets/tsiaras/uk-road-safety-accidents-and-vehicles/data) to uncover hidden patterns behind over a decade of traffic incidents.

Our mission? Turn messy, multi-million-rows of data into a machine learning pipeline and an interactive dashboard that lets stakeholders know exactly how to make British roads safer.

## Intended Stakeholder or Audience

- **Primary Stakeholders:** Department of Transportation planners, road safety engineers, and emergency services dispatch directors in the United Kingdom.
- **Usage:** Stakeholders can use these risk profiles to intelligently deploy highway patrols, optimize speed limits, and allocate emergency response

## Tools / Technologies Used

- **Programming Language:** Python
- **Machine Learning Libraries:** `scikit-learn` (specifically `HistGradientBoostingRegressor`, `RandomForestRegressor`, and `SimpleImputer`)
- **Data Wrangling:** `pandas` and `numpy`
- **Data Visualization & Dashboards:** Tableau Public / Tableau Desktop

## High-Level Methodology / Approach

- **Data Prep & Join:** Cleaned raw data, turned them into `accidents_clean.csv` and `vehicles_clean.csv`. Each member did exploratory data analysis to understand patterns and trends
  . Created a main EDA file to display unique findings.

- **Unsupervised Profiling:** Grouped thousands of rows into five clean, distinct driving environments using clustering algorithms.

- **Supervised Risk Modeling:** Trained and compared supervised models(regression and classfication) to predict a continuous accident fatality risk percentage.

- **Interactive Dashboarding:** Exported final aggregated results into a lightweight Tableau dashboard to visually track model accuracy and trends.

---

## Our Team & Individual Contributions

| Member                      | Primary responsibility                                                                                                                                                                                                                                                                                                                                | Where to see it                                                                                                                                                                                          |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Leomary Rodriguez**       | Built the cleaning pipeline for both raw files — the hidden-missing-value fix, type parsing and join logic that every other notebook depends on. Led EDA on severity, speed limit, lighting, weather, driver age and time trends. Co-built the unsupervised clustering. Contributed to the Tableau dashboard. Wrote a large part of the Final Report. | [`notebooks/leomary_eda.ipynb`](notebooks/leomary_eda.ipynb) · [`models/unsupervised_clustering.ipynb`](models/unsupervised_clustering.ipynb) · [`report/final_report.ipynb`](report/final_report.ipynb) |
| **Oluwafikunayomi Adeniji** | EDA on the severity distribution and how severity varies with speed limit, light conditions and urban vs rural setting. Co-built the unsupervised clustering. Contributed to the Tableau dashboard.                                                                                                                                                   | [`notebooks/oluwafikunayomi_eda.ipynb`](notebooks/oluwafikunayomi_eda.ipynb) · [`models/unsupervised_clustering.ipynb`](models/unsupervised_clustering.ipynb)                                            |
| **Amina Jobarteh**          | Led project management and technical documentation goals. Built EDA on day of week, journey purpose, weather conditions and severity over time. Built the supervised model, and wrote the supervised sections of the Final Report. Assembled and finalised the Tableau dashboard.                                                                     | [`notebooks/amina_ukeda.ipynb`](notebooks/amina_ukeda.ipynb) · [`models/supervised_regression.ipynb`](models/supervised_regression.ipynb) · dashboard                                                    |
| **Ye (Morris) Ou**          | EDA on road and vehicle factors — road surface conditions, junction detail, vehicle manoeuvre and vehicle age — and how each relates to accident severity. Contributed to the Tableau dashboard and to the supervised sections of the Final Report.                                                                                                   | [`notebooks/morris_eda.ipynb`](notebooks/morris_eda.ipynb)                                                                                                                                               |

All four contributed findings to [`notebooks/main_eda.ipynb`](notebooks/main_eda.ipynb), the collected
team EDA, and all four contributed views to the Tableau dashboard, which Amina assembled and
finalised.

---

## Repository Structure

```text
├── README.md
├── requirements.txt
├── data/
│   ├── README.md                       ← one-time data setup (CSVs are gitignored)
│   ├── raw/                            ← Accident_Information.csv, Vehicle_Information.csv
│   └── preprocessed/
│       ├── accidents_clean.csv
│       ├── vehicles_clean.csv
│       └── accident_clusters.csv.gz    ← cluster labels, small enough to commit
├── notebooks/
│   ├── leomary_eda.ipynb               ← cleaning pipeline + EDA
│   ├── oluwafikunayomi_eda.ipynb
│   ├── amina_ukeda.ipynb
│   ├── morris_eda.ipynb
│   └── main_eda.ipynb                  ← collected team findings
├── models/
│   ├── unsupervised_clustering.ipynb   ← KMeans, five accident profiles
│   └── supervised_regression.ipynb     ← predicts fatality risk
├── dashboard/
│   └── screenshots/                    ← Tableau Public dashboard captures
└── report/
    ├── final_report.ipynb              ← the full write-up
    └── figures/                        ← charts used in the report
```

**Note on the data.** The raw and cleaned CSVs are ~2.4 GB combined and GitHub caps files at 100 MB,
so they are gitignored — see [`data/README.md`](data/README.md) for the one-time setup. The only
data file in the repo is `accident_clusters.csv.gz`, which is small enough to commit so the
supervised notebook can read it after a `git pull`.

---

## Key Findings / Results

- paste here

## Tableau Dashboard Link & Screenshots

- **Live Interactive Visualization:** [View the Live Tableau Dashboard](INSERT_YOUR_TABLEAU_PUBLIC_URL_HERE)
- _Alternatively, see the screenshot below displaying our final model validation curves mapping actual versus predicted trends:_

![Model Validation Chart](INSERT_PATH_TO_YOUR_SCREENSHOT_IMG_HERE)

## Recommendations / Implications

- paste here

## Brief Limitations & Next Steps

- paste here

## Link to Full Final Report

- For an in-depth review of our equations, data cleaning notebooks, and granular evaluation curves, read our complete [Final Project Report Document](INSERT_LINK_TO_YOUR_FINAL_REPORT_PDF_OR_MD_HERE).

## Data Source: Quick Start Guide

### Clone the Repo

```bash
git clone https://github.com/AmiJoba22/uk_road_safety_datapipe].git
cd [uk_road_safety_datapipe]
```

### Fetch the Data

Download the data directly from [Kaggle](https://www.kaggle.com/datasets/tsiaras/uk-road-safety-accidents-and-vehicles/data), drop the raw files into `data/raw/`, and step through the notebooks sequentially!

The CSVs are too large to commit (GitHub caps files at 100 MB), so they are gitignored and every clone starts empty. See **[`data/README.md`](data/README.md)** for the full one-time setup and the path convention all notebooks use.
