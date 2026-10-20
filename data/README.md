# Datasets

The datasets are **not** stored in this repo. Download each one and place it in
`data/raw/`. After this, `data/raw/` should contain the three files below.

```
data/
├── README.md        # this file
└── raw/             # gitignored — data lives here, never committed
    ├── Maternal Health Risk Data Set.csv
    ├── CTG.xls
    └── FETAL_PLANES_DB_data.csv   (+ the image folders)
```

## 1. Maternal Health Risk

- Target: risk level — low / mid / high (1,014 records, 6 vitals)
- Source: UCI Machine Learning Repository — "Maternal Health Risk"
  (https://archive.ics.uci.edu/dataset/863/maternal+health+risk), also on Kaggle.
- File: `Maternal Health Risk Data Set.csv`

## 2. Cardiotocography (CTG)

- Target: fetal state — normal / suspect / pathologic (2,126 records)
- Source: UCI Machine Learning Repository — "Cardiotocography"
  (https://archive.ics.uci.edu/dataset/193/cardiotocography)
- File: `CTG.xls` — use the raw CTG sheet; label column `NSP` = 1 (normal) /
  2 (suspect) / 3 (pathologic).

## 3. Fetal ultrasound planes (FETAL_PLANES_DB)

- Target: 6 anatomical planes (brain, abdomen, femur, thorax, cervix, other)
- Source: Zenodo — https://zenodo.org/record/3904280
- Includes the images, the plane labels (`FETAL_PLANES_DB_data.csv`), and a
  **predefined train/test split that respects patients**. Use that split — do not
  make your own random image split, or the same patient leaks into both train and
  test and inflates accuracy.

> Confirm the UCI links resolve before relying on them; if a dataset ID has changed,
> search the dataset name on the UCI repository. The Zenodo link is the one cited in
> the source paper (Burgos-Artizzu et al., 2020).
