# Team Plan — Problem Analysis Workshop B (K-Means Clustering)

**Course:** PROG8431 — Data Analysis, Mathematics, Modeling and Algorithms  
**Project:** Crop Recommendation Analysis  
**Assignment:** Problem Analysis Workshop B (Assignment 3)  
**Final notebook:** [`Crop_Recommendation_Workshop_B.ipynb`](Crop_Recommendation_Workshop_B.ipynb)  
**Working integration branch:** `assignment-3-kmeans-workshop-b`  
**Repository:** [UbaidUllah777/Crop_Recommendation_Analysis](https://github.com/UbaidUllah777/Crop_Recommendation_Analysis)  
**Submission format:** Unzipped Jupyter notebook (`.ipynb`) and repository link  
**Deadline note:** The portal screenshot previously showed **November 5, 2026, 8:30 PM**; the assignment PDF gave a later time. Use the earlier portal deadline unless the instructor has confirmed otherwise.  
**Presentation plan:** Seven minutes using the same submitted notebook, not a separate slide deck.

> **Status (November 5, 2026):** Analysis and notebook sections are complete in the final uploaded copy. PRs #3, #4 and #5 were merged into the Assignment 3 integration branch. Fresh-kernel verification, presentation rehearsal, submission, and visibility of the final files on `main` must be checked separately rather than assumed.

## 1. Project goal and research question

**Research question:** Can K-Means identify meaningful groups of growing conditions in the Crop Recommendation Dataset, and how are crop labels distributed among those groups?

Assignments 1–2 described variables and compared rice and maize rainfall. Workshop B uses **unsupervised clustering** to group records based on similar **rainfall** and **relative humidity**. Crop labels are **excluded from the clustering inputs** and examined only after the clusters have been formed.

The Kaggle Crop Recommendation Dataset contains **2,200 records, 22 crop labels (100 records per label), and seven numerical variables**: `N`, `P`, `K`, `temperature`, `humidity`, `ph`, `rainfall`. The workshop notebook reads `Crop_recommendation.csv` from the repository root.

**Interpretation boundary:** These are descriptive groups in the supplied data, not validated growing zones, irrigation requirements, causal relationships, yield predictions or verified recommendations for actual farms.

## 2. Team members, responsibilities and speaking order

| Member | Student ID | GitHub | Workshop B contribution documented in repository | Presentation order |
|---|---|---|---|---|
| **Ubaid Ullah** | **9110715** | [UbaidUllah777](https://github.com/UbaidUllah777) | Data quality and EDA; choice of rainfall and humidity; scaling; K-Means elbow/evaluation and candidate-K comparisons; coordination and PR reviews | **First — 0:00–3:00** |
| **Rangeetha** | **9081357** | [rangeethasajeer-debug](https://github.com/rangeethasajeer-debug) | Final K = 6 assignments, original-unit centres, full cluster profiles, crop-label distribution and clustering figures | **Second — 3:00–6:00** |
| **Koushik Balne** | **9087547** | [koushikbalne97](https://github.com/koushikbalne97) | Conclusion and review-oriented improvements in the final integrated notebook | **Third — 6:00–7:00** |

The PR history below is the primary evidence of contributions and formal reviews. Every presenter should still understand all sections sufficiently to answer questions.

## 3. Work completed in the final notebook

| Notebook section | Implemented content | Evidence in final uploaded notebook |
|---|---|---|
| 1–3: Overview, setup and cleaning | Context, imports, source CSV, types, missing/duplicate/validity checks | 2,200 × 8; 22 labels; no missing values or exact duplicates; no checked invalid nutrient, rainfall, humidity or pH values |
| 4: Exploratory analysis | Descriptive statistics, histograms, box plots, candidate-variable scatter plots and justification | Rainfall–humidity selected instead of rainfall–temperature for the moisture-focused question |
| 5: Transformation | `sta01()` Min-Max comparison and `stamn()` z-score method | **Only Z-score** rainfall and humidity are used as K-Means inputs; originals are retained |
| 6: K selection | Inertia for K = 1–10, elbow plot, improvement per additional K, variation explained, scatter comparison of K = 3–6 and cluster-size checks | Final recommendation **K = 6** |
| 7: Final grouping | Stored K = 6 model, original-unit centres, six named clusters, counts, means of **all seven** numeric variables, crop heatmap, additional profiles and interpretation | **All six clusters profiled**; figures and tables included |
| 8: Recommendation | Model choice, methodological rationale and limitations | Rainfall + humidity; Z-score; K-Means with `random_state=42`, `n_init=10`; K = 6 |
| 9: Conclusion | Concise answer to the original research question, rice–maize pattern, and limitations | The final integrated notebook includes Koushik's concluding Markdown section |

**Source-version check:** The downloaded **Assignment 3 integration-branch notebook** has **38 cells**, with **19 executed code cells** and **Section 9: Final Conclusion**. The earlier copy without Section 9 is not the final version.

**Important correction:** Older planning text and the original description of PR #3 mentioned **silhouette scores**. The **final uploaded notebook does not import or calculate a silhouette metric**. Its model selection is based on the elbow/inertia evidence, variation explained, sizes, scatter plots and descriptive utility. Do not report 0.508 or make a silhouette-based selection claim when presenting this final notebook.

The downloaded final integrated notebook contains saved outputs for **19 code cells** with execution numbers 1–19 and no stored error outputs. That indicates a completed saved execution, **not** independently verified fresh-kernel reproducibility.

## 4. How K = 6 was chosen

The clustering inputs are `rainfall_std` and `humidity_std`, produced by z-score standardization. Inertia decreases as K increases, so the team compared marginal improvement, variation explained, cluster sizes and visual separation rather than treating the lowest inertia as the answer.

| K | Inertia / within-cluster SS | Variation explained (two standardized inputs) | Smallest cluster | Largest cluster |
|---:|---:|---:|---:|---:|
| 3 | 1,413.29 | 67.9% | 430 | 1,295 |
| 4 | 1,030.73 | 76.6% | 244 | 969 |
| 5 | 757.56 | 82.8% | 240 | 552 |
| **6** | **552.36** | **87.4%** | **190** | **541** |

The graph bends near **K = 3**, but additional clusters still separate visibly different rainfall values. Adding the sixth cluster reduces inertia by about **205.20**, while adding the seventh reduces it by about **87.77**. The K = 6 groups were then checked for reasonable size and interpretable environmental patterns.

The **87.4%** number describes variation accounted for in the **two standardized clustering variables**; it is **not** predictive or crop recommendation accuracy. K = 6 is a documented, defensible choice for this analysis, not a uniquely correct cluster count for agriculture.

## 5. Final six-cluster scheme

The cluster numbers order the humidity bands first and rainfall bands within them. Cluster names are descriptive and based on measured centres only.

| # | Descriptive cluster name | Records | Share of dataset | Centre humidity | Centre rainfall |
|---:|---|---:|---:|---:|---:|
| 1 | Very Low Humidity, Moderate Rainfall | 209 | 9.5% | 19.95% | 93.39 mm |
| 2 | Moderate Humidity, Low Rainfall | 500 | 22.7% | 59.31% | 68.80 mm |
| 3 | Moderate Humidity, High Rainfall | 190 | 8.6% | 55.22% | 159.56 mm |
| 4 | High Humidity, Low Rainfall | 481 | 21.9% | 85.77% | 51.82 mm |
| 5 | High Humidity, Moderate Rainfall | 541 | 24.6% | 88.20% | 111.56 mm |
| 6 | High Humidity, Very High Rainfall | 279 | 12.7% | 85.93% | 208.26 mm |
| **Total** | | **2,200** | **100.0%** | | |

Selected descriptive observations from the notebook:

- Every **rice** record is in cluster 6; **89% of maize** records are in cluster 2. This is compatible with Workshop A's recorded rainfall differences but does not prove crop water requirements.
- All records for chickpea and kidney beans appear in cluster 1; all records for apple, banana, orange and pomegranate appear in cluster 5.
- Some crop labels span groups: papaya records are distributed across clusters 4–6. The groups therefore do **not** correspond one-to-one to crop labels.
- Means of nitrogen, phosphorus, potassium, temperature and soil pH were evaluated **after** the clusters were fitted, rather than used to determine the clusters.

These percentages describe **where each crop label's records appear in this dataset**, not success rates or real-world suitability.

## 6. Actual collaboration and PR review record

| PR | Author / scope | Review evidence | GitHub status |
|---|---|---|---|
| [#3 — Ubaid's initial analysis](https://github.com/UbaidUllah777/Crop_Recommendation_Analysis/pull/3) | Ubaid: EDA, scaling and clustering evaluation | Merged; **no formal submitted GitHub review** was returned for this PR | **Merged November 2, 2026** |
| [#4 — final cluster analysis](https://github.com/UbaidUllah777/Crop_Recommendation_Analysis/pull/4) | Rangeetha: final K-Means model and interpretation | Ubaid requested changes November 3; later **approved** November 4 | **Merged November 4, 2026** |
| [#5 — conclusion and review findings](https://github.com/UbaidUllah777/Crop_Recommendation_Analysis/pull/5) | Koushik: final conclusion and review improvements | Ubaid requested simplification; then **approved** November 4 | **Merged November 4, 2026** |

This table describes verified PR status and review events, not unrecorded meetings or an independently witnessed notebook run. Earlier review requests about silhouette wording or removal of the word *augmented* are historical review comments; the final file content is the authority for what the actual submitted analysis performs.

**Integration practice:** Teammates contributed through distinct branches and their work was combined into `assignment-3-kmeans-workshop-b`. Before final submission, check whether that branch has been merged to `main`; at the last repository check for this update, the Workshop B notebook was **not found on `main`**.

## 7. Seven-minute notebook presentation plan

| Time | Presenter | Focus and explanation |
|---|---|---|
| **0:00–0:20** | Ubaid | Research question: group moisture conditions instead of comparing only two crops |
| **0:20–1:10** | Ubaid | Data checks and why rainfall + humidity were chosen |
| **1:10–2:00** | Ubaid | Compare scaling methods; explain why distance-based K-Means uses Z-scores |
| **2:00–3:00** | Ubaid | Elbow, marginal inertia reductions, candidate plots, and K = 6 trade-off **without a silhouette claim** |
| **3:00–3:50** | Rangeetha | Final K = 6 scatter plot and cluster centres in original units |
| **3:50–4:50** | Rangeetha | Six cluster names, sizes, and moisture characteristics |
| **4:50–6:00** | Rangeetha | Seven-variable profiles, crop-label heatmap and key insights |
| **6:00–7:00** | Koushik | Conclusions, limitations and what would require real farm data |

The order is a **presentation plan**, not a claim a rehearsal happened. Koushik's speaking portion should align with **Section 9**, rather than reading the detailed Section 8 recommendations again. Demonstrate the **exact notebook submitted** and be ready to answer questions about the entire analysis.

## 8. Limitations and responsible interpretation

- Cluster boundaries are based only on rainfall and relative humidity; the remaining five numeric features are summarized afterward.
- Crop labels represent categories in a balanced teaching dataset, not measured yields, farmer outcomes or confirmed suitability at a location.
- The dataset lacks specified date, location, farming season, rainfall accumulation period, sampling method and independent field validation.
- K-Means creates geometric boundaries; the higher-humidity region is relatively continuous and its boundaries may be model-dependent.
- No irrigation prescriptions, causal claims, yield predictions or population-level estimates follow from these groupings.

## 9. Final submission checklist

- [x] All names and IDs appear in the final notebook.
- [x] Data checks, EDA, feature choice and scaling comparison are included.
- [x] K = 1–10 elbow/inertia evaluation and K = 3–6 comparison are included.
- [x] Final K = 6 model, centroids, named groups, seven-variable profiles and crop-label analysis are included.
- [x] Section 9 final conclusion (Koushik), limitations, charts and summary tables are included.
- [x] PRs #3, #4 and #5 are merged; formal approved reviews recorded for #4 and #5.
- [ ] Independently perform **Restart Kernel → Run All** on the final uploaded notebook and confirm all outputs and paths.
- [ ] Place the final `Crop_Recommendation_Workshop_B.ipynb`, `README.md` and both team plans on the branch being submitted; confirm branch visibility on GitHub.
- [ ] Ensure final `README.md` makes **no silhouette-score claim**, matching the final notebook.
- [ ] Confirm seven-minute rehearsal and readiness for professor questions (only if performed).
- [ ] Submit the unzipped `.ipynb` and correct GitHub repository/branch URL before the instructor's deadline.

**Updated for the final integrated notebook:** November 5, 2026. This replaces the November 1 draft. Completed results and verified PR histories are reported; outstanding checks are not misrepresented as complete.
