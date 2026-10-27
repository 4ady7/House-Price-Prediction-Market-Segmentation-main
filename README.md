# House Price Prediction and Market Segmentation

Coursework notebooks that explore California district housing data, train regression models, and practice K-Means clustering. The notebooks follow [Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow](https://www.oreilly.com/library/view/hands-on-machine-learning/9781098125967/) (Aurélien Géron), chapters 2, 4, and 9, with extra analysis on the housing files in this repo.

Run every notebook from the project root. Paths such as `datasets/housing/housing.csv` are relative to that directory.

## Notebooks

| Notebook | What it covers |
| --- | --- |
| `Data_processing_as1.ipynb` | Load the California housing set, build a stratified train/test split, plot geography and correlations, engineer `rooms_per_house`, `bedrooms_ratio`, and `people_per_house`, then impute missing values, one-hot encode `ocean_proximity`, and scale numeric features. A later section reloads `housingAs1.csv` and looks at how `total_bedrooms` and `ocean_proximity` relate to `median_house_value`. Week 2 starts the same inspection on the US listings file. |
| `regression_1_as1.ipynb` | Fit ordinary least squares on a synthetic line, then implement batch, stochastic, and mini-batch gradient descent (including `SGDRegressor.partial_fit`). The last section fits polynomial regression and compares degree 1, 2, and 300 to show underfitting and overfitting. |
| `clustering_as1.ipynb` | Fit K-Means on synthetic blobs, compare hard and soft clustering, and choose `k` with inertia and silhouette score. The Olivetti faces exercise picks a cluster count from silhouette scores and checks which clusters contain photos of a single person. The notebook also loads `housepriceAs1.csv`. |

`Notes.txt` is a short reminder of what a `KMeans` label is and what `silhouette_score` measures.

## Data

All files live under `datasets/housing/`.

**California districts** (`housing.csv`, `housingAs1.csv`, and `housing.tgz`) — 20,640 census-block groups from the StatLib California housing set used in the Géron book.

| Column | Meaning |
| --- | --- |
| `longitude`, `latitude` | District centroid |
| `housing_median_age` | Median age of houses in the district |
| `total_rooms`, `total_bedrooms` | Counts for the district. `total_bedrooms` has missing values |
| `population`, `households` | People and households in the district |
| `median_income` | Median income, in tens of thousands of dollars |
| `median_house_value` | Target, in dollars. Capped at 500,001 |
| `ocean_proximity` | `<1H OCEAN`, `INLAND`, `NEAR OCEAN`, `NEAR BAY`, or `ISLAND` |

`Data_processing_as1.ipynb` downloads `housing.tgz` from the [ageron/data](https://github.com/ageron/data) repository if `datasets/housing/housing.tgz` is missing, then extracts `housing.csv`. The copy is already in this repo, so a fresh download is only needed if that archive is removed.

**US listings** (`housepriceAs1.csv`) — 30,006 property listings. Columns: `Price`, `Sqr Ft`, `Longitude`, `Latitude`, `Lot Size`, `Beds`, `Bath`, `Year Built`, `Last Sold Year`, `Last Sold For`, `Address`, `City`, `State`, `Zipcode`, `Address Full`. Price, square footage, and lot size are stored as formatted strings (for example `$895,900` and `3,447 sqft`).

Plots saved by the data notebook are in `images/end_to_end_project/`.

## Setup

Python 3.7 or newer, and the libraries imported by the notebooks:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install "numpy" "pandas" "matplotlib" "scikit-learn>=1.0.1" "packaging" "jupyter"
```

Start Jupyter from the project root and open a notebook:

```bash
jupyter notebook
```

Or run a notebook without the UI:

```bash
jupyter nbconvert --to notebook --execute Data_processing_as1.ipynb --output Data_processing_as1.out.ipynb
```

`clustering_as1.ipynb` calls `sklearn.datasets.fetch_olivetti_faces()`, which downloads the Olivetti faces set on first use (about 400 images, 64×64). That step needs network access. The other two notebooks run from the files already in `datasets/`.

## Layout

```
.
├── Data_processing_as1.ipynb
├── regression_1_as1.ipynb
├── clustering_as1.ipynb
├── Notes.txt
├── datasets/
│   └── housing/
│       ├── housing.csv
│       ├── housingAs1.csv
│       ├── housing.tgz
│       └── housepriceAs1.csv
└── images/
    └── end_to_end_project/
```
