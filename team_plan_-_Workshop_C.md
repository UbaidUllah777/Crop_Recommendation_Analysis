# Team Plan — Problem Analysis Workshop C (Transformations, Validation and Regression)

**Course:** PROG8431 — Data Analysis, Mathematics, Modeling and Algorithms  
**Project:** Crop Recommendation Analysis  
**Assignment:** Problem Analysis Workshop C  
**Final notebook:** [`PROG8431_CropAnalyzer_Regression.ipynb`](PROG8431_CropAnalyzer_Regression.ipynb)  
**Member branches:** `workshop-cd/rangeetha`, `workshop-cd/ubaid`, `workshop-cd/koushik`  
**Integration branch:** `assignment-4-regression-workshop-c` — each member branch merges only through a reviewed pull request  
**Repository:** [UbaidUllah777/Crop_Recommendation_Analysis](https://github.com/UbaidUllah777/Crop_Recommendation_Analysis)  
**Submission format:** Jupyter notebook (`.ipynb`) confirm against the Workshop C instructions  



## 1. Project goal and research question

**Problem analysis statement:** Nitrogen is the most widely used fertilizer nutrient, yet the soil nitrogen level crops need varies widely — in our data, average `N` ranges from about **19** (lentil, pomegranate) to about **118** (cotton). Without knowing what drives these differences, fertilizer is planned crop by crop from experience, which risks over-applying an expensive input.

**Research question:** Which crop characteristics and growing conditions explain the soil nitrogen (`N`) level at which a crop grows well, and how accurately can `N` be predicted for fields the model has not seen?

Workshop B grouped growing conditions with K-Means. Workshop C moves from description to **prediction**: it augments the dataset with outside sources, transforms the variables, splits the data into training and test sets, and fits simple and multiple linear regression models with `N` as the dependent variable.

The Kaggle Crop Recommendation Dataset contains **2,200 records, 22 crop labels (100 records per label), and seven numerical variables**: `N`, `P`, `K`, `temperature`, `humidity`, `ph`, `rainfall`. The notebook reads `Crop_recommendation.csv` from the repository root and downloads the outside sources into `data/`.

**Method boundary:** Only methods from the Week 10 slides and the two class notebooks (SLR and MLR demos) are used. Assumption checks (residual plots, normality tests) and cross-validation were deliberately removed because they have not yet been taught.

**Interpretation boundary:** Regression results describe associations in this teaching dataset. They are not fertilizer prescriptions, causal effects, yield predictions or verified recommendations for real farms.

## 2. Team members, responsibilities and speaking order

| Member | Student ID | GitHub | Branch | Workshop C responsibility | Presentation order |
|---|---|---|---|---|---|
| **Rangeetha** (Member 1) | **9081357** | [rangeethasajeer-debug](https://github.com/rangeethasajeer-debug) | `workshop-cd/rangeetha` | Title and team table, Project Overview, notebook sections 1–2: setup and configuration, data augmentation (FAO EcoCrop and Statistics Canada), transformations, categorical conversion, study file and data-source discussion | **First — 0:00–2:30** |
| **Ubaid Ullah** (Member 2) | **9110715** | [UbaidUllah777](https://github.com/UbaidUllah777) | `workshop-cd/ubaid` | Notebook sections 3–5: train/test split and comparability checks, dependent variable, two simple linear regression models and their comparison; repository settings as repository owner | **Second — 2:30–5:00** |
| **Koushik Balne** (Member 3) | **9087547** | [koushikbalne97](https://github.com/koushikbalne97) | `workshop-cd/koushik` | Notebook section 6: multiple linear regression, backward and judgemental selection, final-model discussion; final integrated run, HTML export and submission | **Third — 5:00–7:00** |

Every presenter should understand all sections well enough to answer questions about the whole analysis. The pull-request history will be the primary evidence of contributions and reviews.

## 3. Work in the notebook

The assignment lists seven requirements, but the notebook numbers its own sections 1–6, so the two numbers differ. This plan always refers to **notebook sections**.

| Assignment requirement | Notebook section | Owner |
|---|---|---|
| 1. Team names and IDs | Title cell | Member 1 |
| 2. Setup and configuration | 1: Environment setup | Member 1 |
| 3. Augment data, convert categoricals, transform, discuss | 2: Data augmentation (2.1–2.10) | Member 1 |
| 4. Train/test split and comparison | 3: Split into training and test sets | Member 2 |
| 5. Dependent variable | 4: Dependent variable | Member 2 |
| 6. Two simple linear regression models | 5: Simple linear regression | Member 2 |
| 7. Multiple linear regression and variable selection | 6: Multiple linear regression (6.1–6.8) | Member 3 |

| Notebook section | Owner | Planned / implemented content | Status |
|---|---|---|---|
| Title, Project Overview, How Transformations and Regression Help | Member 1 | Team table; Problem Analysis Statement, objective, scope and approach; table linking each technique to the project | Written; add names and IDs; check figures after the full run |
| 1: Environment setup | Member 1 | Install cell, workspace reset, imports, one configuration cell (paths, source URLs, `RANDOM_STATE = 6174`, 80/20 split, α = 0.05), download helper that detects and replaces invalid files | Written; download fix added after a Statistics Canada `BadZipFile` error |
| 2.1–2.3: Sources | Member 1 | Crop data loaded and renamed; FAO EcoCrop requirements matched by scientific name; Statistics Canada tables 32-10-0359-01, 32-10-0364-01, 32-10-0365-01 averaged over 5 years | Code tested; live downloads to be confirmed |
| 2.4–2.5: Merge and missing values | Member 1 | Many-to-one merge on `label`; derived `is_legume`, `P_K_ratio`, `eco_topt_width`, `ph_class`; any FAO field missing for one of our crops is **dropped, not filled** | Code tested |
| 2.6–2.8: Transformations and categorical conversion | Member 1 | Box-Cox with nearest Tukey's-ladder rung; `log(x + 1)` for zero-heavy Canadian columns; dummy coding (k − 1); ordinal pH class | Confirmed on real crop data |
| 2.9–2.10: Study file and discussion | Member 1 | `crop_study_file.csv` with 25+ usable variables; data-source, rationale and transformation discussion | Test run: 30 variables before dummy coding, 53 columns; confirm on full run |
| 3: Train/test split | Member 2 | 80/20 split; KS tests (numeric) and chi-square tests (categorical); discussion of dissimilarities | Confirmed on real data; outside-source rows to confirm |
| 4: Dependent variable | Member 2 | `N` chosen and justified; Spearman correlations with `N` | Written |
| 5: Simple linear regression | Member 2 | `N ~ humid` vs `N ~ is_legume`; F-statistic, R², adjusted R², t-tests, coefficient sense, train/test RMSE | Confirmed on real data; verify against statsmodels output |
| 6: Multiple linear regression | Member 3 | Full model, backward selection (class demo function), judgemental model, comparison table, final model choice and discussion (6.8) | Code tested; results depend on the full run |

**Gap variables, in-range flags and median filling were removed** to keep the transformations closer to the class material. Box-Cox and Tukey's ladder come from the slides; dummy coding and merging are required by the assignment even though the demo notebooks do not show them explicitly.

## 4. How the two simple regression models compare

Training set n = 1,760; test set n = 440 (`random_state = 6174`).

| Measure | Model A: `N ~ humid` | Model B: `N ~ is_legume` |
|---|---:|---:|
| F-statistic (p-value) | 74.5 (≈ 1.4 × 10⁻¹⁷) | **475.3** (≈ 1.8 × 10⁻⁹³) |
| R² / adjusted R² | 0.041 / 0.040 | **0.213 / 0.212** |
| Slope (t) | +0.33 per % humidity (8.6) | **−36.3 (−21.8)** |
| Intercept | 26.4 | 61.9 |
| Train RMSE / test RMSE | 36.1 / 36.7 | **32.7 / 33.7** |

**Model B is superior on every measure.** Non-legumes average about 61.9 `N` and legumes about 36.3 less (≈ 25.7), which matches the biology: legumes fix their own nitrogen. Humidity is significant only because n is large; it explains about 4% of the variation in `N`.

The train/test split is comparable: no variable from the crop dataset differs significantly (all KS p > 0.05), and the crop mix passes the chi-square test (p ≈ 0.29). The closest call is a slightly lower share of legumes in the test set (28.2% vs 32.7%, p ≈ 0.08), which explains Model B's small rise in test RMSE.

The multiple-regression results (section 6) are **not yet available** and must not be quoted until the full run is complete.

## 5. Study file and transformations

| Variable group | Source | Treatment |
|---|---|---|
| `N`, `P`, `K`, temperature, humidity, pH, rainfall | Crop Recommendation dataset | `N` kept in original units (dependent variable) |
| P, K, humidity, rainfall, P/K ratio | Crop dataset / derived | Box-Cox: P → square root (λ 0.39), K → reciprocal square root (λ −0.34), humidity → square (λ 2.12), rainfall and P/K → log (λ 0.22, 0.25) |
| Temperature, pH | Crop dataset | Not transformed (skew below the 0.75 rule) |
| Optimal and absolute temperature, rainfall, pH; crop cycle; life form; category | FAO EcoCrop | Joined on crop; fields missing for any crop dropped; life form and category dummy-coded |
| `grown_in_canada`, Canadian area and farm value | Statistics Canada | Not grown = 0; area and value `log(x + 1)` |
| `is_legume`, `ph_class` | Derived | 0/1 flag; ordinal 0 = acidic, 1 = neutral, 2 = alkaline |
| `label` | Crop dataset | 21 dummy variables; kept in the study file but **not** used in the regressions, because crop-level variables would duplicate them exactly |

## 6. Collaboration and PR review plan

| Branch | Author / scope | Reviewer | Merge order | GitHub status |
|---|---|---|---|---|
| `workshop-cd/rangeetha` | Rangeetha: title, overview, sections 1–2 | Koushik | **First** — other sections need the study file | Not yet opened |
| `workshop-cd/ubaid` | Ubaid: sections 3–5 | Rangeetha | After member1, either order with member3 | Not yet opened |
| `workshop-cd/koushik` | Koushik: section 6, final run and submission | Ubaid | After member1, either order with member2 | Not yet opened |

This table is a plan, not a record. Update the status column with PR numbers, review events and merge dates as they happen, as in the Workshop B record.

**Integration practice**

- Create each branch from an up-to-date `main`: `git checkout main`, `git pull`, `git checkout -b workshop-cd/memberN-name`, `git push -u origin workshop-cd/memberN-name`.
- Edit only your own notebook sections; overlapping edits create merge conflicts that are hard to resolve in an `.ipynb` file.
- Run **Restart Kernel → Run All** before committing, then clear outputs so diffs show only code and text changes.
- Keep `data/`, `crop_study_file.csv`  in `.gitignore`.
- Ubaid, as repository owner, sets `main` to require one approving review per pull request. Reviewers check that the notebook runs, that only class methods are used, and that discussion numbers match the outputs.
- After all merges, Koushik runs the integrated notebook on `main`, commits the run notebook with outputs and the HTML export, and confirms both are visible on `main` before submission.

## 7. Seven-minute notebook presentation plan

| Time | Presenter | Focus and explanation |
|---|---|---|
| **0:00–0:40** | Rangeetha | Problem analysis statement and why `N` matters for fertilizer planning |
| **0:40–1:40** | Rangeetha | Outside sources (FAO EcoCrop, Statistics Canada), join on crop name, 25+ variable study file |
| **1:40–2:30** | Rangeetha | Box-Cox / Tukey's ladder choices and categorical conversion |
| **2:30–3:20** | Ubaid | 80/20 split, KS and chi-square comparability, the legume near-miss |
| **3:20–5:00** | Ubaid | Model A vs Model B: F, adjusted R², t-tests, coefficients, train/test RMSE; why Model B wins |
| **5:00–6:20** | Koushik | Full → backward → judgemental model; comparison table; final model and its measures |
| **6:20–7:00** | Koushik | Conclusions and limitations |

The order is a presentation plan, not a claim that a rehearsal happened. Demonstrate the exact notebook submitted.

## 8. Limitations and responsible interpretation

- Crop-level variables (FAO, Statistics Canada, `is_legume`) take only 22 distinct values, so the models mainly explain differences **between** crops; variation within a crop remains largely unexplained.
- The dataset lacks date, location, season and sampling details; `N` is the dataset's soil nitrogen value where the crop grows well, not a measured fertilizer requirement.
- Statistics Canada variables describe relevance to Canadian agriculture, not growing requirements.
- FAO EcoCrop values are general species requirements, matched by scientific name, and are not specific to the fields in the dataset.
- Box-Cox λ values were estimated on the full data before the split, a small leak accepted to follow the assignment order.
- Regression coefficients show associations, not causal effects; no fertilizer prescriptions follow from these models.

