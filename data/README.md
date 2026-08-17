# Data

The full dataset is **not stored in this repository**. The two raw CSVs are roughly 1.3 GB
combined, and GitHub rejects any single file over 100 MB.

## Getting the data

1. Download the **UK Road Safety: Traffic Accidents and Vehicles** dataset from Kaggle:
   https://www.kaggle.com/datasets/tsiaras/uk-road-safety-accidents-and-vehicles/data
2. Unzip it and place both CSVs directly in `data/raw/`:

```
data/raw/
├── Accident_Information.csv    (~705 MB)
└── Vehicle_Information.csv     (~644 MB)
```

3. Run the notebooks in `notebooks/` in order. The EDA notebook reads from `data/raw/` and
   writes its cleaned output to `data/processed/`, which the later notebooks read from.
   Paths are relative, so no editing is needed as long as you keep the folder layout below.

## Folder layout

| Folder | Contents | Committed? |
|---|---|---|
| `data/raw/` | Original Kaggle CSVs, unmodified | No — gitignored |
| `data/processed/` | Cleaned output written by the EDA notebook | No — gitignored |
| `data/sample/` | 10,000-row samples for quick inspection | **Yes** |

## Sample files

`data/sample/` holds a small extract so the repository is not completely empty of data and
so code can be smoke-tested without the full download:

- `accidents_sample.csv` — 10,000 accident rows (2.8 MB)
- `vehicles_sample.csv` — 10,000 vehicle rows (2.5 MB), of which 3,978 join to the
  accident sample on `Accident_Index`

**These samples are for inspection and testing only.** They are drawn from the first portion
of the files and are not representative of the full dataset — do not compute findings from
them.

## Notes on the raw files

Things worth knowing before you load these, all documented in detail in
[`notebooks/eda_notebooks/eda_lr_uk_road_safety.ipynb`](../notebooks/eda_notebooks/eda_lr_uk_road_safety.ipynb):

- **`Vehicle_Information.csv` is not UTF-8.** It is Windows-1252 and must be read with
  `encoding="cp1252"`, or pandas raises a `UnicodeDecodeError`. `Accident_Information.csv`
  reads fine with the default encoding.
- **The two files cover different years.** Accidents span 2005–2017, vehicles 2004–2016. An
  inner join on `Accident_Index` keeps 94.54% of vehicle rows; the 118,797 dropped are all
  from 2004.
- **Missing values are often stored as text**, not blanks — `"Data missing or out of range"`,
  `"Unknown"`, `"Not known"`, and `"NA"` appear across 22 columns. `.isna()` alone will not
  find them.
- **`Carriageway_Hazards` and `Special_Conditions_at_Site` are ~98% blank by design.** A blank
  means *no hazard was present*, not that the value is unknown.
- Use `low_memory=False` on both files to stop pandas inferring different dtypes for different
  chunks of the same column.

## Source and licence

UK Department for Transport road safety data (STATS19), published via Kaggle under the
[Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).
