# Multimodal AI for Maternal-Fetal Health Triage

**F21DL — Data Mining and Machine Learning (2026/2027) · Group Coursework**

Machine learning as **decision support for maternal-fetal triage — never a replacement for
clinicians**. Early risk signals in pregnancy are spread across maternal vitals, fetal
heart-rate monitoring, and ultrasound imaging. We build one module per signal and evaluate
each on its own public dataset.

> **Framing (important):** the three datasets are independent cohorts with **no shared
> patients**, so we do **not** fuse them. This is a pipeline of three separate modules, each
> handling one stage of the same clinical workflow. True multimodal fusion is future work.

---

## Datasets

| Dataset | Type | Size | Target | Source |
| --- | --- | --- | --- | --- |
| Maternal Health Risk | Tabular | 1,014 records, 6 vitals | Risk level: low / mid / high | UCI / Kaggle |
| Cardiotocography (CTG) | Tabular | 2,126 records | Fetal state: normal / suspect / pathologic | UCI |
| Fetal ultrasound planes | Images | 12,400 images | 6 anatomical planes | FETAL_PLANES_DB (Zenodo) |

The datasets are **not committed** to this repo. See [`data/README.md`](data/README.md) for
download links and where to place the files.

---

## Research questions

| # | Question | Hypothesis |
| --- | --- | --- |
| RQ1 | Can routine vitals predict a mother's risk level? | Blood sugar strongest; blood pressure weaker. |
| RQ2 | Do non-linear models beat linear ones on the tabular data? | Trees and ensembles win (feature interactions). |
| RQ3 | Can a CNN recognise the ultrasound plane despite uneven class sizes? | Transfer learning does well; rare planes hardest. |
| RQ4 | Do natural clusters match the clinical labels? | Only partly — risk is a gradient, not three tidy groups. |

---

## How the coursework requirements are covered

| Req | What it asks | Where it lives |
| --- | --- | --- |
| **R1** | Topic, questions, objectives | This README + the pitch |
| **R2** | Clean, explore, cluster | `01`, `02` (EDA), `03` (k-means + GMM/EM, scored with silhouette and ARI/NMI) |
| **R3** | ≥3 classical models, compared | `04`, `05` (Logistic Regression, Naïve Bayes, k-NN, Decision Tree, Random Forest + Gradient Boosting) |
| **R4** | Neural networks | `06` (MLP on tabular), `07` (transfer-learning CNN on ultrasound) |

Generative + discriminative are both covered: Naïve Bayes and GMM/EM are generative; the
rest are discriminative.

---

## Repository structure

```
.
├── README.md
├── environment.yml          # dependency list (local runs only; Colab has these)
├── .gitignore
├── data/
│   ├── README.md            # download instructions (raw data is gitignored)
│   └── raw/                 # not committed
├── notebooks/
│   ├── 01_eda_maternal.ipynb
│   ├── 02_eda_ctg.ipynb
│   ├── 03_clustering.ipynb
│   ├── 04_baselines_maternal.ipynb
│   ├── 05_baselines_ctg.ipynb
│   ├── 06_mlp_tabular.ipynb
│   └── 07_cnn_ultrasound.ipynb
├── src/                     # shared helpers (loaders, metrics, plots)
├── results/                 # saved figures and metrics tables
└── report/                  # 6-page PDF report
```

---

## Setup

**We run the notebooks on Google Colab** (free GPU for the CNN). The notebooks live in
this GitHub repo; the datasets live in a shared Google Drive folder.

1. Open a notebook in Colab: **File → Open notebook → GitHub tab**, paste this repo URL,
   pick the notebook. Save back with **File → Save a copy to GitHub**.
2. The data lives in a shared Drive folder `MyDrive/DMML-data/` (two CSVs, the CTG `.xls`,
   and the `images/` folder). Ask the repo owner to share it with you.
3. Every notebook's first cell mounts Drive:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   DATA = '/content/drive/MyDrive/DMML-data'
   ```

Colab already has pandas, scikit-learn and PyTorch installed, so `environment.yml` is only
for anyone who prefers to run locally (`conda env create -f environment.yml`).

## How to run

Run the notebooks in order. `01`–`03` cover R2 (clean, explore, cluster), `04`–`05` cover R3
(classical baselines), `06`–`07` cover R4 (MLP and CNN). Figures and metrics tables are saved
to `results/` for the report.

> **Note on the ultrasound split:** use the dataset's predefined patient-respecting train/test
> split. Do **not** make a random image split — one patient has many images, and mixing them
> across train and test inflates accuracy.

---

## Team

| Member | Responsibility |
| --- | --- |
| _TBD_ | Maternal Health Risk — EDA + baselines |
| _TBD_ | Cardiotocography — EDA + baselines |
| _TBD_ | Clustering + MLP |
| _TBD_ | Ultrasound CNN |
| _TBD_ | Repo + report lead, shared `src/`, results |

---

## Ethics

All data is public and anonymised. This project is an educational exploration of decision
support only; it is not a medical device and must not be used for real clinical decisions.
