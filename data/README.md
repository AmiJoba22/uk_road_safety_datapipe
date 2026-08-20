# Data

The CSVs are **not** stored in this repository. The two raw files are about 1.3 GB combined and
the cleaned files about 1.1 GB, and GitHub rejects any single file over 100 MB. Everything in
`raw/` and `preprocessed/` is gitignored.

Each folder keeps a `.gitkeep` so the structure survives a clone.

## One-time setup

**1. Download the raw data** from Kaggle:
[UK Road Safety: Traffic Accidents and Vehicles](https://www.kaggle.com/datasets/tsiaras/uk-road-safety-accidents-and-vehicles)

**2. Put both files in `data/raw/`**, keeping their original names:

```text
data/raw/Accident_Information.csv
data/raw/Vehicle_Information.csv
```

**3. Generate the cleaned files** by running Sections 1–6 of
[`notebooks/leomary_eda.ipynb`](../notebooks/leomary_eda.ipynb). That writes:

```text
data/preprocessed/accidents_clean.csv
data/preprocessed/vehicles_clean.csv
```

Every other notebook reads from `data/preprocessed/`, so this only needs doing once.

## Path convention

All notebooks live in `notebooks/`, so paths are one level up:

```python
pd.read_csv('../data/raw/Accident_Information.csv')
pd.read_csv('../data/preprocessed/accidents_clean.csv')
```

Please don't use absolute paths (`/Users/yourname/...`) — they only work on one machine.

## What the cleaning does

Full reasoning is in `leomary_eda.ipynb`. In short:

- Placeholder text that means "missing" — `'Data missing or out of range'`, `'Unknown'`,
  `'Not known'`, `'NA'` — is replaced with `np.nan`. Without this, `.isnull()` finds nothing and
  those words become real categories in charts and models.
- `Date` and `Time` are parsed into datetimes, with `Month` and `Hour` derived from them.
- The files are **not** joined or filtered — that stays in the analysis notebooks.

## Known data issues

- The accident file covers 2005–2017; the vehicle file covers 2004–2016. Joining on
  `Accident_Index` drops 118,797 vehicle rows, all from 2004.
- `Vehicle_Type` has numeric codes (`109`, `106`, `108`) that appear only in 2004. `109` is
  `Car` under the pre-2005 coding scheme.
- `Age_of_Vehicle` runs up to 111 years and `Engine_Capacity_.CC.` up to 96,000cc. Both are
  impossible and need handling before modeling.
