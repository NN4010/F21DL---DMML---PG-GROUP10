# Datasets

The datasets are **not** stored in this repo (too large, and the image set
especially). Code lives in GitHub; data lives in Google Drive.

**Team members:** the data is in a shared Google Drive folder named
`DM&MLcsvfile` (three tabular files) plus the ultrasound `images` folder. Ask the
repo owner for access, then in Google Drive go to **Shared with me →
right-click the folder → Organise → Add shortcut to Drive → My Drive**. Each Colab
notebook mounts it like this:

```python
from google.colab import drive
drive.mount('/content/drive')
DATA = '/content/drive/MyDrive/DM&MLcsvfile'
```

**Teaching staff / anyone without Drive access:** download the three datasets
directly from their public sources below — they are the authoritative copies and
reproduce the project on any machine.

## 1. Maternal Health Risk

- Target: risk level — low / mid / high (1,014 records, 6 vitals)
- Source: UCI Machine Learning Repository — "Maternal Health Risk"
  (https://archive.ics.uci.edu/dataset/863/maternal+health+risk), also on Kaggle.
- File: `Maternal Health Risk Data Set.csv`

## 2. Cardiotocography (CTG)

- Target: fetal state — normal / suspect / pathologic (2,126 records)
- Source: UCI Machine Learning Repository — "Cardiotocography"
  (https://archive.ics.uci.edu/dataset/193/cardiotocography)
- File: `CTG.xls` — load the **`Raw Data`** sheet (`sheet_name='Raw Data'`); needs
  `xlrd`. Target column `NSP` = 1 (normal) / 2 (suspect) / 3 (pathologic). Drop the
  trailing blank rows and the leakage columns (`CLASS, A–E, AD, DE, LD, FS, SUSP`)
  and metadata (`FileName, Date, SegFile, b, e, LBE, DR`); keep the 21 FHR features.

## 3. Fetal ultrasound planes (FETAL_PLANES_DB)

- Target: 6 anatomical planes (brain, abdomen, femur, thorax, cervix, other)
- Source: Zenodo — https://zenodo.org/record/3904280
- Includes the images, the plane labels (`FETAL_PLANES_DB_data.csv`, **`;`-separated**),
  and a **predefined train/test split that respects patients** — the `Train` column
  (1 = train, 0 = test). Use that split — do not make your own random image split, or
  the same patient leaks into both train and test and inflates accuracy.

> Confirm the UCI links resolve before relying on them; if a dataset ID has changed,
> search the dataset name on the UCI repository. The Zenodo link is the one cited in
> the source paper (Burgos-Artizzu et al., 2020).
