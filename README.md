# Wine_Data_Pandas101

A hands-on pandas and linear-regression practice notebook working through exploratory data analysis on a historical weather dataset and a red-wine-quality dataset. It demonstrates loading CSV data with pandas, cleaning missing values, correlation analysis, visualization, and fitting simple/multiple linear regression models with scikit-learn.

## Overview

This is an educational EDA and modeling exercise built around two questions:

1. **Weather** — Can `MaxTemp` be predicted from `MinTemp`? The notebook explores the relationship, fits a simple linear regression, and analyzes the prediction error (mean, standard deviation, and error binned by 10-degree intervals).
2. **Wine quality** — Which chemical attributes drive a wine's `quality` score? The notebook fits multiple linear regression models over different feature subsets and uses correlation/coefficient heatmaps to reason about why using every available variable is not always optimal.

The work is framed as a practice / coursework-style notebook rather than a production pipeline.

## Data

### `winequality.csv`
Red-wine physicochemical measurements with a sensory quality score (~1,599 rows). Columns:

| Column | Description |
| --- | --- |
| `fixed acidity` | Non-volatile (tartaric) acids |
| `volatile acidity` | Acetic acid content; high levels give a vinegar taste |
| `citric acid` | Adds freshness and flavor |
| `residual sugar` | Sugar remaining after fermentation |
| `chlorides` | Salt content |
| `free sulfur dioxide` | Free form of SO2 (prevents microbial growth) |
| `total sulfur dioxide` | Total SO2 (free + bound) |
| `density` | Density of the wine |
| `pH` | Acidity/basicity on the pH scale |
| `sulphates` | Additive contributing to SO2 levels |
| `alcohol` | Alcohol percent by volume |
| `quality` | Target: sensory quality score |

### `Weather.csv`
Historical daily weather records (~119,040 rows) with station, date, temperature, precipitation, and many derived/coded measurement columns. Columns most used in the notebook:

| Column | Description |
| --- | --- |
| `MinTemp` | Minimum temperature (regression feature) |
| `MaxTemp` | Maximum temperature (regression target) |
| `MeanTemp` | Mean temperature |
| `Precip` | Precipitation |
| `WTE` | Sparse column with many NaNs, used to practice `fillna` |

The file also includes `STA`, `Date`, `WindGustSpd`, `Snowfall`, and numerous additional coded measurement fields (`PRCP`, `MAX`, `MIN`, `MEA`, `SNF`, `RHX`, `RHN`, etc.).

## Approach

Pandas and modeling operations demonstrated in the notebook:

- **Loading** CSV data with `pd.read_csv` (including `low_memory=False`).
- **Missing-value handling** — `fillna(0)` on a single column and `fillna(method='ffill')` for forward-fill imputation; `isnull().any()` for null detection.
- **Correlation analysis** — `Series.corr()` between `MinTemp` and `MaxTemp`.
- **Visualization** — scatter plots via `DataFrame.plot` and matplotlib, regression-line overlays, and seaborn heatmaps / `JointGrid` for feature relationships.
- **Train/test split** — `train_test_split` (80/20) from scikit-learn.
- **Linear regression** — `LinearRegression` fit, inspecting intercept and coefficients.
- **Error analysis** — building an `Actual` / `Predicted` / `Error` DataFrame, computing `mean()` and `std()`, and **binning** errors with `pd.cut` followed by `groupby` aggregation.
- **Feature-subset comparison** — refitting the wine model on progressively smaller feature sets and comparing coefficient heatmaps and mean error to discuss multicollinearity and feature selection.

## Repository structure

| File | Purpose |
| --- | --- |
| `wine_data_pandas_basics.ipynb` | Main Jupyter notebook with all EDA, plotting, and regression code and commentary |
| `winequality.csv` | Red-wine physicochemical dataset (regression target: `quality`) |
| `Weather.csv` | Historical daily weather dataset (`MinTemp` vs `MaxTemp` regression) |
| `requirements.txt` | Python dependencies |
| `.gitignore` | Ignored files and directories |
| `LICENSE` | MIT License |
| `README.md` | This file |

## Tech stack

- Python 3
- Jupyter Notebook
- pandas, numpy
- matplotlib, seaborn
- scikit-learn
- scipy

## Setup & usage

```bash
# 1. (Optional) create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch Jupyter and open the notebook
jupyter notebook wine_data_pandas_basics.ipynb
```

Run the cells top to bottom. The notebook expects `Weather.csv` and `winequality.csv` to be in the same directory.

## License

Released under the MIT License. See [LICENSE](LICENSE) for details.
