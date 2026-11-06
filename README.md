# Crop Recommendation Analysis

**PROG8431 — Data Analysis, Mathematics, Modeling and Algorithms**  
**Team project | Assignments 1–3**

This repository examines the **Crop Recommendation Dataset** through exploratory data analysis, statistical comparison, and unsupervised learning. The work progresses from understanding the dataset (Assignment 1), to comparing crop-labelled observations statistically (Workshop A), to identifying patterns in environmental measurements using **K-Means clustering** (Workshop B).

> **Scope:** This is an exploratory analysis of a teaching dataset. The clusters describe similarities among the recorded measurements; they are **not** validated crop recommendations, agricultural prescriptions, or evidence of causation.

## Team

| Member | Student ID | GitHub | Workshop A focus | Workshop B focus |
|---|---|---|---|---|
| Ubaid Ullah | 9110715 | [UbaidUllah777](https://github.com/UbaidUllah777) | Statistical comparisons and communication (Sections 12–15) | Data quality, EDA, feature selection, scaling, and cluster-count evaluation |
| Rangeetha | 9081357 | [rangeethasajeer-debug](https://github.com/rangeethasajeer-debug) | Visualizations and normality assessment (Sections 8–11) | Final cluster model, centres, profiles, crop-label analysis, and visualizations |
| Koushik Balne | 9087547 | [koushikbalne97](https://github.com/koushikbalne97) | Setup, data exploration, and statistical profile (Sections 1–7) | Independent validation, conclusions, limitations, and final review |

The focus areas reflect the team's division of responsibilities. The GitHub commit and pull-request history is the record of actual individual changes and reviews.

## Research questions

**Overall question:** What soil-composition and environmental patterns are associated with the crop labels in this dataset?

**Workshop B question:** Can K-Means identify meaningful groups of recorded growing conditions using **rainfall** and **relative humidity**, and what do the resulting groups reveal about the distribution of crop labels?

The model does **not** use crop labels to form clusters. Labels are examined **after** clustering to interpret the groups.

## Dataset

- **Source:** [Crop Recommendation Dataset by Atharva Ingle (Kaggle)](https://www.kaggle.com/datasets/atharvaingle/crop-recommendation-dataset)
- **Local file:** [`Crop_recommendation.csv`](Crop_recommendation.csv) (repository root)
- **Records:** 2,200
- **Crop labels:** 22, with 100 records for each label
- **Columns:** `N`, `P`, `K`, `temperature`, `humidity`, `ph`, `rainfall`, `label`

| Column | Description |
|---|---|
| `N`, `P`, `K` | Numerical soil-nutrient measurements |
| `temperature` | Recorded temperature (°C) |
| `humidity` | Recorded relative humidity (%) |
| `ph` | Soil pH |
| `rainfall` | Recorded rainfall (mm; accumulation period unspecified) |
| `label` | Crop category; **used for interpretation, not K-Means training** |

The Workshop B quality checks found **no missing values, exact duplicate rows, negative N/P/K or rainfall values, humidity outside 0–100%, or pH outside 0–14**. All 2,200 observations were retained. High-rainfall and low-humidity observations were explored with box plots rather than automatically deleted, because they are associated with particular crop-labelled records.

## Assignment progression

### Assignment 1 — Exploratory Data Analysis

**Notebook:** [`assignment 1.ipynb`](assignment%201.ipynb)

Introduced the dataset, explored soil and environmental measurements, calculated descriptive statistics, and used visualizations (including histograms, box plots, scatter plots, and Venn diagrams) to investigate patterns associated with crop labels.

### Assignment 2 — Problem Analysis Workshop A

**Notebook:** [`Crop_Recommendation_Workshop_A.ipynb`](Crop_Recommendation_Workshop_A.ipynb)

Extended the exploratory work with distribution comparisons, Q–Q plots, Shapiro–Wilk normality tests, a classical F-test for rainfall variances, and Welch's t-test with confidence-interval interpretation for **rice versus maize rainfall**.

**Recorded result:** Mean rainfall was approximately **236.18 mm for rice** and **84.77 mm for maize**, a difference of about **151.41 mm**. The tested groups did not satisfy the normality assumption at the 5% level; consequently, the classical F-test needs cautious interpretation. These results describe the dataset and do not establish irrigation requirements.

### Assignment 3 — Problem Analysis Workshop B: K-Means Clustering

**Final notebook:** [`Crop_Recommendation_Workshop_B.ipynb`](Crop_Recommendation_Workshop_B.ipynb)

The completed notebook contains the following stages:

1. **Load and assess the data:** Inspect shape, types, missing values, duplicates, crop balance, and numerical validity.
2. **Perform EDA:** Examine distributions, descriptive statistics, box plots, and scatter plots for rainfall, humidity, and the alternative candidate temperature.
3. **Select features:** Compare rainfall–temperature with rainfall–humidity. Their Pearson correlations were approximately **−0.030** and **0.094**, respectively; the rainfall–humidity plot provided a useful exploratory view of moisture-related concentrations.
4. **Compare transformations:** Demonstrate Min-Max (`sta01()`) and Z-score (`stamn()`) scaling. Use **Z-score-standardized rainfall and humidity** for distance-based K-Means; retain original measurements for interpretation.
5. **Evaluate cluster counts:** Fit K-Means for **K = 1 through 10**, generate the elbow curve, calculate the reduction in inertia and fraction of two-feature variation explained, examine cluster sizes, and visualize **K = 3, 4, 5, and 6**.
6. **Select and describe the final model:** Choose **K = 6**, convert cluster centres back to original units, assign descriptive names, and summarize all seven numerical variables and crop-label distributions.
7. **Interpret results and limitations:** Explain what the six groups show—and what they do not demonstrate about real agricultural suitability.

**K-Means settings:** `n_init=10`, `random_state=42`, with Euclidean-distance clustering on `rainfall_std` and `humidity_std`.

## Workshop B — Final results

### Why Z-score standardization?

Before scaling, rainfall had a mean of **103.46 mm** and standard deviation of **54.96 mm**; humidity had a mean of **71.48%** and standard deviation of **22.26 percentage points**. After Z-score standardization, both variables have a mean of approximately zero and standard deviation of one.

The notebook also shows that Min-Max scaling would give rainfall a standard deviation of **0.197**, versus **0.260** for humidity. Z-score was chosen to give the two features comparable spread in the K-Means distance calculation, without changing the original values used to describe the clusters.

### Choosing the number of clusters

The elbow curve has an early bend near **K = 3**, but the notebook's combined evidence supports **K = 6** as a more detailed and interpretable representation of the moisture patterns.

| K | Inertia (within-cluster SS) | Variation explained in the two standardized features | Smallest cluster | Largest cluster |
|---:|---:|---:|---:|---:|
| 3 | 1,413.29 | 67.9% | 430 | 1,295 |
| 4 | 1,030.73 | 76.6% | 244 | 969 |
| 5 | 757.56 | 82.8% | 240 | 552 |
| **6** | **552.36** | **87.4%** | **190** | **541** |

Adding the sixth cluster reduced inertia by **205.20** compared with K = 5. The following step, from **K = 6 to 7**, reduced inertia by only **87.77**, showing a substantial drop in incremental improvement. The final K = 6 groups also have workable sizes and interpretable centres.

**Important:** The **87.4%** figure is the share of total variation accounted for by the clusters in these **two standardized inputs**. It is **not** classification accuracy, recommendation accuracy, or a measure of crop yield. The final notebook does not report silhouette scores; its selection relies on inertia, incremental improvement, variation explained, cluster sizes, and visual interpretation.

### Final six-cluster scheme

Cluster names are based on their centre **humidity** and **rainfall** values. The numbering orders humidity bands first, then rainfall within each band; it is not one overall dry-to-wet ranking.

| # | Cluster | Records | Share | Centre humidity | Centre rainfall | Examples of crop-label membership |
|---:|---|---:|---:|---:|---:|---|
| 1 | **Very Low Humidity, Moderate Rainfall** | 209 | 9.5% | 19.95% | 93.39 mm | All chickpea and kidneybeans records |
| 2 | **Moderate Humidity, Low Rainfall** | 500 | 22.7% | 59.31% | 68.80 mm | All blackgram, lentil, mango, and mothbeans records; 89% of maize records |
| 3 | **Moderate Humidity, High Rainfall** | 190 | 8.6% | 55.22% | 159.56 mm | 97% of coffee and 80% of pigeonpeas records |
| 4 | **High Humidity, Low Rainfall** | 481 | 21.9% | 85.77% | 51.82 mm | All grapes, muskmelon, mungbean, and watermelon records; 56% of cotton records |
| 5 | **High Humidity, Moderate Rainfall** | 541 | 24.6% | 88.20% | 111.56 mm | All apple, banana, orange, and pomegranate records |
| 6 | **High Humidity, Very High Rainfall** | 279 | 12.7% | 85.93% | 208.26 mm | All rice records; 73% of jute and 61% of coconut records |

*The crop percentages describe how each crop label's **own records** are distributed among clusters; they do not mean that the cluster is suitable for those crops.* The final notebook includes a crop-by-cluster heatmap, cluster-centre scatter plot, full seven-variable means, and box plots for `N`, `P`, `K`, `temperature`, and `ph`.

### Main findings

- **Six groups summarize 22 crop labels:** Humidity produces several broad bands, while rainfall separates groups within the moderate- and high-humidity ranges.
- **Workshop A's rice–maize contrast appears in the broader clustering pattern:** Rice records fall in the very-high-rainfall group; most maize records fall in the moderate-humidity, low-rainfall group.
- **Clusters describe measurements, not botanical categories:** Crop labels from related categories do not necessarily appear together. Some labels, especially papaya, also span several moisture clusters.
- **Other variables differ across the resulting groups:** For example, the very-low-humidity group has a mean temperature near 20°C and relatively low nitrogen, while the high-humidity/low-rainfall group has high mean nitrogen and potassium. These are descriptive associations, **not** causal findings.

## Conclusions and limitations

The final recommendation is **K-Means with K = 6**, trained on **Z-score-standardized rainfall and relative humidity**, with clusters interpreted using the original values and crop-label distributions. This scheme is useful for summarizing environmental patterns in the supplied dataset.

Its limitations are important:

- The dataset is **balanced by crop label** (100 records each); cluster size is not an estimate of real-world farmland frequency.
- Location, date, farming season, sampling method, and rainfall accumulation period are not provided.
- The crop `label` is **not a measured yield or successful growing outcome**; clustering cannot validate which crops will perform best at a location.
- The model uses **only two** environmental features. Soil nutrients, temperature, and pH are profiled afterward, not used to determine membership.
- K-Means imposes geometric partitions. Some boundaries in the high-humidity region are model-dependent rather than natural agricultural borders.
- Neither the cluster assignments nor the observed statistical associations establish cause and effect or replace field trials and locally representative agronomic data.

## Repository files

| File or folder | Purpose |
|---|---|
| [`assignment 1.ipynb`](assignment%201.ipynb) | Assignment 1: exploratory analysis |
| [`Crop_Recommendation_Workshop_A.ipynb`](Crop_Recommendation_Workshop_A.ipynb) | Assignment 2: statistical analysis |
| [`Crop_Recommendation_Workshop_B.ipynb`](Crop_Recommendation_Workshop_B.ipynb) | **Assignment 3: completed K-Means clustering analysis** |
| [`Crop_recommendation.csv`](Crop_recommendation.csv) | Input dataset; keep at repository root |
| `figures/` | Supporting figures from project work, where included |
| `team plan.md` | Existing Workshop A planning notes |
| `team plan - Workshop B.md` | Workshop B planning and task allocation, where included |
| `README.md` | Project overview, methods, results, and reproduction instructions |

The primary deliverables are the **notebooks**; plots, tables, model comparisons, and conclusions for Workshop B are included inside its `.ipynb` file.

## How to run

1. Clone the repository and open its **root directory**.
2. Confirm that `Crop_recommendation.csv` is in that root directory, alongside `Crop_Recommendation_Workshop_B.ipynb`.
3. Use a Python virtual environment, install the required packages, and start JupyterLab (or open the notebook using the VS Code Jupyter extension).
4. Open the Workshop B notebook and select **Restart Kernel → Run All**.

Example for **Windows PowerShell**:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install pandas numpy matplotlib seaborn scikit-learn ipython jupyterlab
jupyter lab
```

For the earlier assignment notebooks, additional libraries such as **SciPy** and **matplotlib-venn** may be needed. If the repository contains an up-to-date `requirements.txt`, `python -m pip install -r requirements.txt` can be used instead.

The Workshop B notebook reads the input using:

```python
from pathlib import Path
import pandas as pd

df = pd.read_csv(Path("Crop_recommendation.csv"))
```

The K-Means outputs are reproducible with the specified parameters and appropriate library versions. Saved notebook outputs document the reported results; running locally still requires the dataset and dependencies.

## Data attribution

**Dataset:** Atharva Ingle, [Crop Recommendation Dataset on Kaggle](https://www.kaggle.com/datasets/atharvaingle/crop-recommendation-dataset).

**Project:** Academic team analysis for PROG8431. Findings should be interpreted as exploratory observations from this dataset, not practical farming advice.
