# Crop Recommendation Analysis

Team project for **PROG8431 — Data Analysis, Mathematics, Modeling and Algorithms**.

## Team

| Team member | Student ID | GitHub | Workshop A responsibility | Workshop B proposed responsibility |
|---|---|---|---|---|
| Ubaid Ullah | 9110715 | [UbaidUllah777](https://github.com/UbaidUllah777) | Sections 12–15: statistical comparisons and communication | Data quality, EDA, variable selection, scaling, elbow analysis, silhouette evaluation.|
| Rangeetha | 9081357 | [rangeethasajeer-debug](https://github.com/rangeethasajeer-debug) | Sections 8–11: visuals and normality |Final clustering model, centroids, comprehensive cluster profiles, crop-label interpretation, visualizations. |
| Koushik Balne | 9087547 | [koushikbalne97](https://github.com/koushikbalne97) | Sections 1–7: setup, data and statistical profile | Independent validation, conclusions, limitations, and final review. |

Workshop B responsibilities are a **proposed division**, not an assertion that the work is already complete. Actual individual work and peer review should be traceable through issues, commits and PRs.

## Research scope

**Original research question:** Which soil composition and environmental factors are associated with crop labels?

This teaching dataset supports exploratory comparisons and clustering. It does **not** by itself support causal findings, field-level irrigation prescriptions, or validated crop recommendations.

### Dataset

- **Source:** [Atharva Ingle — Crop Recommendation Dataset, Kaggle](https://www.kaggle.com/datasets/atharvaingle/crop-recommendation-dataset)
- **Committed dataset:** [`Crop_recommendation.csv`](Crop_recommendation.csv), in repository root
- **Columns:** `N`, `P`, `K`, `temperature`, `humidity`, `ph`, `rainfall`, `label`
- **Observed dataset profile in earlier notebook:** 2,200 rows, 22 crop labels, 100 rows per crop, seven numeric variables.
- Missing information includes location/time, rainfall accumulation interval, sampling design, and farm identifiers. Treat all insights as dataset associations.

## Assignment 1 — Exploratory Data Analysis

**Notebook:** [`assignment 1.ipynb`](assignment%201.ipynb)

Includes data loading and cleaning, descriptive statistics, and visualizations such as histograms, box plots, scatter plots and Venn diagrams. The goal was to understand the distributions of growing-condition measurements and how they relate descriptively to crop labels.

## Assignment 2 — Problem Analysis Workshop A

**Notebook:** [`Crop_Recommendation_Workshop_A.ipynb`](Crop_Recommendation_Workshop_A.ipynb)

Extends exploratory analysis with:

- Histograms and distribution comparisons
- QQ plots and Shapiro–Wilk normality tests
- Classical F-test to compare rice and maize rainfall variances
- Welch's T-test, p-value and confidence interval for average rainfall
- Summary report and interpretation limitations

**Recorded finding:** rice-labelled observations have mean rainfall about **236.18 mm**, versus **84.77 mm** for maize, giving a mean difference of about **151.41 mm**. The groups reject normality at the 5% level; the F-test has a violated normality assumption and must be interpreted cautiously. These are not irrigation requirements.


## Assignment 3 — Problem Analysis Workshop B: K-Means Clustering

**Notebook:** [`Crop_Recommendation_Workshop_B.ipynb`](Crop_Recommendation_Workshop_B.ipynb)

**Project question:** Can K-Means clustering identify meaningful groups of growing conditions in the Crop Recommendation Dataset, and what do those groups reveal about crop labels?

### Dataset and feature selection

The analysis uses the original Crop Recommendation Dataset, containing 2,200 observations, seven numerical variables, and 22 crop labels.

Initial exploratory analysis examined rainfall, temperature, and humidity. The final two clustering variables are:

- **Rainfall:** A numerical measurement of recorded rainfall, expressed in millimetres.
- **Humidity:** Relative humidity, expressed as a percentage.

Rainfall and humidity were selected to investigate environmental moisture-related patterns. Crop labels are excluded from the K-Means model inputs and can be used afterwards to interpret the resulting clusters.

### Standardization

Both selected variables were standardized using the z-score method demonstrated in class. Standardization places rainfall and humidity on comparable scales before K-Means calculates Euclidean distances.

The original data values remain available for interpretation.

### Selecting the number of clusters

K-Means models were evaluated for K = 1 through 10 using the elbow method. Additional evaluations included silhouette scores, cluster sizes, and visual comparisons of K = 3, 4, 5, and 6.

The elbow curve suggested an early bend near K = 3. However, K = 6 achieved the highest full-dataset silhouette score among the shortlisted solutions.

| K | Full-dataset silhouette score | Inertia |
|---|---:|---:|
| 3 | 0.485 | 1,413.29 |
| 4 | 0.462 | 1,030.73 |
| 5 | 0.478 | 757.56 |
| 6 | 0.508 | 552.36 |

**Current recommended model:** K = 6 using standardized rainfall and humidity.

The smallest K = 6 cluster contained 190 observations and the largest contained 541. This recommendation is based on the evaluated models and will be considered alongside the final cluster profiles.

### Current progress

Completed analysis:
- Dataset loading and data-quality assessment
- Exploratory analysis and two-variable selection
- Z-score standardization and before/after comparisons
- Elbow analysis for K = 1–10
- Sampled and full-dataset silhouette evaluation
- Visual comparison of shortlisted cluster counts
- Evidence-based recommendation of K = 6

The remaining cluster profiling, crop-label interpretation, final findings, and team integration are not yet reported as completed.

### Interpretation limits

Clusters represent similarity in rainfall and humidity within this dataset. They are not validated farming zones, causal relationships, or independently verified crop recommendations.

The dataset does not specify the rainfall measurement interval, location, sampling design, or farming season, so agricultural conclusions require caution.



## Repository organization

Existing committed material:

- `assignment 1.ipynb` — Assignment 1
- `Crop_Recommendation_Workshop_A.ipynb` — Assignment 2
- `Crop_recommendation.csv` — source data kept in repository root
- `figures/` — generated figures
- `Teams_whiteboard_draft.png` — Workshop A summary figure
- `team plan.md` — existing Workshop A plan (preserve for history)
- `requirements.txt` — environment dependencies, if not already added
- `Crop_Recommendation_Workshop_B.ipynb` — new notebook
- `team plan - Workshop B.md` — project plan and task allocation

Planned Workshop B additions:

- `collaboration/Workshop_B_review_log.md` — genuine work and review records, if created

## Run locally

1. Clone the repository and change to its root folder.
2. Create and activate a virtual environment.
3. Install declared dependencies with `python -m pip install -r requirements.txt` **after** that file is committed, or use your existing working environment in the meantime.
4. Launch Jupyter with `jupyter lab` (or use VS Code's Jupyter extension).
5. Open the desired `.ipynb` and run **Restart Kernel → Run All**.
6. Keep `Crop_recommendation.csv` in the **repository root** for the existing Workshop A notebook, which loads it there.

Example on Windows PowerShell:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
jupyter lab
```

Typical dependencies for the earlier notebooks include NumPy, pandas, Matplotlib, seaborn, SciPy, matplotlib-venn, IPython, and Jupyter. Workshop B may add scikit-learn depending on the exact course demonstration. Verify installation and notebook execution before final submission; do not assume a fresh setup was tested simply because results are saved inside the notebook.

## Team development workflow for Workshop B

- Stable past work stays on `main`.
- Integrate Assignment 3 on `assignment-3-kmeans-workshop-b`.
- Each teammate creates a separate feature branch for their own task, with an appropriately named GitHub issue and one focused pull request.
- A different member adds a substantive comment or approval before merging.
- Cite real issue/PR/commit links in the collaborative log; never invent co-authors, reviews, or meetings.
- Coordinate editing a shared `.ipynb` file, because simultaneous notebook edits can cause difficult merge conflicts.

See [`team plan - Workshop B.md`](team%20plan%20-%20Workshop%20B.md) after it is committed for task assignments, reviewer rotation, seven-minute presentation order, and quality checklist.

## Presentation and submission

- Workshop B: **seven-minute** notebook presentation. Ubaid first (3 min), Rangeetha second (3 min), Koushik last (1 min).
- All three must understand the methods and be able to answer questions and adjust code.
- Submit the **`.ipynb` file itself (not zipped)** and GitHub repository URL; present that exact submitted notebook.
- **Deadline clarification:** the portal screenshot shows Nov 5, 2026 at **8:30 PM**, while the assignment PDF says before Nov 5 at **10 PM**. Follow the earlier time unless your instructor confirms otherwise.
- The PDF also contains an inconsistent five-minute phrase, but its explicit mandatory presentation instructions state **seven minutes**.

## Academic and technical caution

Cluster labels describe patterns in the selected measurements; they are not verified crop requirements. Sample independence, data representativeness, farming season and rainfall period remain unknown. Final claims must be limited to what the observed dataset supports.
