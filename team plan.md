# Shared Team Plan — Crop Recommendation Analysis
## Workshop A (Assignment 2): Completed work and historical record

> This document preserves Assignment 2 (Workshop A) methods, team responsibilities and lessons learned. Workshop B is recorded separately in [`team plan - Workshop B.md`](team%20plan%20-%20Workshop%20B.md). Nothing here represents invented contributions, approvals, meetings, or notebook changes.

## 1. Team and responsibilities

| Member | Student ID | Assignment 2 lead | Assignment 2 peer-review responsibility |
| --- | --- | --- | --- |
| Koushik Balne | 9087547 | Sections 1–7: framing, source, preparation, statistical profiling | Review visual-analysis work |
| Rangeetha | 9081357 | Sections 8–11: plots, distributions, QQ plots, Shapiro–Wilk | Review data preparation and clarity |
| Ubaid Ullah | 9110715 | Sections 12–15: F-test, Welch T-test, p-values, final communication | Review statistical interpretation and integrate final notebook |

The names and section ownership reflect the existing Workshop A plan and repository commit history. Every team member must also understand the full notebook, not only their assigned sections.

## 2. Project context and research question

**Dataset:** Kaggle Crop Recommendation Dataset (`Crop_recommendation.csv`), stored at the repository root.

**Broad project question:** Which soil and environmental factors are associated with crop labels?

**Focused Workshop A question:** How do rainfall distributions, variances and mean values differ between rice-labelled and maize-labelled records?

**Intended audience:** A proposed regional agricultural planning committee, agricultural extension officers, public-sector analysts and farmer-association representatives.

**Limits:** This is an exploratory classroom dataset; its rainfall accumulation period, sampling independence, field locations and representativeness are not established. Our findings are not direct irrigation prescriptions or causal effects.

## 3. Assignment 1 foundation retained

- Load and assess the provided crop data (2,200 records; 22 crop labels; seven numerical soil/climate columns).
- Check quality, duplicate rows and missing values.
- Preserve full precision and only round displayed results.
- Use the object-oriented `CropAnalyzer` for mean, median, mode, sample variance, standard deviation and quartiles.
- Preserve box plots, rainfall histogram/KDE, temperature-humidity scatter plot, three-set Venn diagram and analytical discussion.
- Describe the six plotted crops as selected examples, not a rank-ordered list.

## 4. Workshop A notebook mapping

| Notebook sections | Main topic | Lead |
| --- | --- | --- |
| 1–7 | Overview, question, methodology, imports, data validation and statistical profiling | Koushik |
| 8–11 | Existing plots, distribution histograms, rice/maize visual comparisons, QQ plots and Shapiro–Wilk test | Rangeetha |
| 12 | Classical variance-ratio F-test and interpretation | Ubaid |
| 13 | Welch's T-test, confidence interval and interpretation | Ubaid |
| 14 | P-value summary and responsible use of evidence | Ubaid |
| 15 | Summary report and interpretation limits | Shared final discussion / Ubaid integration |

## 5. Statistical choices and verified findings

- Use the same outcome variable, **rainfall (mm)**, for the rice and maize comparisons; both groups contain 100 records.
- Significance threshold: `ALPHA = 0.05`.
- Shapiro–Wilk and QQ plots reject a normal distribution model for both groups at the 5% threshold.
- Rice sample variance is approximately 1,175.929 mm²; maize sample variance is approximately 241.720 mm²; F-statistic ≈ 4.8648.
- **Important:** The current 37-cell Workshop A notebook performs the classical F-test **only**; it does **not** execute Levene's test. Because normality is rejected, its inferential p-value must be treated cautiously.
- Rice mean rainfall is approximately 236.18 mm, maize mean approximately 84.77 mm, and sample mean difference approximately 151.41 mm.
- Welch's T-statistic ≈ 40.21; the 95% confidence interval for the mean difference is approximately 143.97–158.86 mm, conditional on the test assumptions.
- The notebook shows associations in its supplied data, not proven crop water needs. Independence and representativeness cannot be verified from its columns.
- Numerical rescaling is not necessary for a same-unit rainfall comparison; rescaling is not the same as testing normality.

## 6. Repository filenames and reproducible setup

| Path | Purpose |
| --- | --- |
| `assignment 1.ipynb` | Assignment 1 baseline |
| `Crop_Recommendation_Workshop_A.ipynb` | Assignment 2 final notebook in the repository |
| `Crop_recommendation.csv` | Local input data at the repository root |
| `figures/` | Saved plots |
| `Teams_whiteboard_draft.png` | Committed summary image |
| `README.md` | Instructions and repository overview |
| `team plan.md` | Workshop A historical plan and handoff record |
| `team plan - Workshop B.md` | Workshop B completed analysis and collaboration record |
| `requirements.txt` | Python package dependency list **if included in the repository** |

**Setup check:** If `requirements.txt` is present, install dependencies with `python -m pip install -r requirements.txt`; otherwise install the packages imported by the notebook. Launch Jupyter from the repository root and use Restart Kernel → Run All. The executed notebook expects `Crop_recommendation.csv` at the repository root and does not automatically download the Kaggle dataset. Do not state that a fresh-environment test succeeded until someone performs and records it.

## 7. Assignment 2 presentation and assessment lessons

The instructor's screenshot of Workshop A feedback reports strong coding and analysis scores, but lower marks for narrative clarity, presentation timing, question responses and individually assessed collaboration. The screenshot reports: notebook presentation guide 1/2, presentation attendance/participation/timing 0.5/2, question responses 1/2 and collaboration 2/6, with a displayed overall score of 12.5/20 (62.5%). These are historical feedback items, not predictions for Workshop B.

**Lessons carried forward into Workshop B:**
1. State the problem/question in one sentence before demonstrating charts or code.
2. Link every test or chart to that question and an actionable interpretation.
3. Rehearse a timed seven-minute notebook-only presentation, with a backup presenter ready.
4. Practise explaining and making a small code change live in every teammate's sections.
5. Keep dated issue discussions, PR descriptions, reviews/approvals and meeting notes so individual collaboration is visible.

## 8. Handoff to Workshop B (Assignment 3)

The next assignment returned to the same 2,200-record, 22-label dataset, but used **unsupervised K-Means** on **rainfall** and **relative humidity** rather than comparing preselected crop groups. Its question was: *Can similar recorded moisture conditions be grouped meaningfully, and how are the crop labels distributed among those groups?*

The final uploaded Workshop B notebook has 37 cells, including a completed K = 6 model, cluster centroids in original units, six named groups, crop-by-cluster analysis, figures, and a final recommendation. It excludes crop labels from model fitting and uses them only to interpret the output. For details, see [`Crop_Recommendation_Workshop_B.ipynb`](Crop_Recommendation_Workshop_B.ipynb) and the separate Workshop B team plan.

**Roles recorded for Workshop B** (these are different from the preliminary role proposals in the original handoff plan):

| Member | Workshop B area | Recorded pull request |
|---|---|---|
| Ubaid Ullah | Quality checks, EDA, input selection, scaling, elbow and comparison of candidate K values | [#3 — merged](https://github.com/UbaidUllah777/Crop_Recommendation_Analysis/pull/3) |
| Rangeetha | Final K = 6 clustering, centroids, cluster profiles, crop-label analysis, figures | [#4 — merged](https://github.com/UbaidUllah777/Crop_Recommendation_Analysis/pull/4) |
| Koushik Balne | Final conclusion and review-oriented improvements | [#5 — merged](https://github.com/UbaidUllah777/Crop_Recommendation_Analysis/pull/5) |

PR #4 and PR #5 have recorded **changes requested followed by approval** from Ubaid. PR #3 is merged but does not have a formal submitted GitHub review in the review record checked for this update. Distinguish PR descriptions from the exact final notebook: earlier PR #3 refers to silhouette analysis, whereas the **final uploaded notebook does not compute silhouette scores**; its final K decision uses inertia/elbow analysis, variation explained, cluster sizes and visual interpretation.

## 9. What the completed Workshop B showed

- Seven numerical soil/environment variables were retained for profiling, while **rainfall and humidity** were standardized by z-score and used to fit K-Means.
- Candidate values **K = 1–10** were assessed. The final recommendation is **K = 6** (inertia **552.36**, **87.4%** of the variation in the two standardized inputs, cluster sizes **190–541**).
- The six groups were described in terms of their moisture measurements, not as verified farming zones or crop prescriptions.
- The original Workshop A rice–maize rainfall contrast can be discussed alongside the grouping of rice records in the very-high-rainfall cluster and most maize records in a lower-rainfall cluster.

This is a **historical handoff summary**, not a replacement for Workshop B results or the README. The dataset does not identify region, season, rainfall accumulation interval, or agricultural outcomes; no causal or practical crop-suitability claim is supported.

## 10. Final repository and submission checks

- Retain this document as the Workshop A history; do not rewrite the completed Workshop A notebook to match Workshop B.
- Retain [`team plan - Workshop B.md`](team%20plan%20-%20Workshop%20B.md) as the separate Workshop B record.
- Confirm the final Workshop B notebook, updated `README.md`, both team plans and input CSV are on the **branch linked for assessment**. When this document was checked, the final notebook was present on `assignment-3-kmeans-workshop-b` but **not yet on `main`**.
- Confirm a local **Restart Kernel → Run All** of the exact final notebook and keep the actual result; saved outputs alone do not prove a fresh-environment run.
- Do not mark rehearsal, submission or further independent checks complete without evidence.

**Document update:** November 5, 2026. Workshop A facts and original statistical results above have been preserved; obsolete future-work instructions were replaced with the completed Workshop B handoff and verified PR history.
