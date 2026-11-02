# Team Plan — Problem Analysis Workshop B (K-Means Clustering)

**Course:** PROG8431 — Data Analysis, Mathematics, Modeling and Algorithms  
**Project:** Crop Recommendation Analysis  
**Assignment:** Problem Analysis Workshop B  
**Integration branch:** `assignment-3-kmeans-workshop-b`  
**Notebook:** `Crop_Recommendation_Workshop_B.ipynb`  
**Submission:** Jupyter notebook (`.ipynb`) and GitHub repository URL; no ZIP submission  
**Deadline:** eConestoga portal: November 5, 2026, 8:30 PM; assignment PDF states before November 5, 10 PM. Use the earlier portal deadline unless the instructor confirms otherwise.  
**Presentation:** Seven minutes using the submitted notebook (not PowerPoint). The PDF also contains an inconsistent five-minute reference; its explicit presentation instructions say seven minutes.

## 1. Project goal and research question

We are continuing the same Crop Recommendation Analysis project from Assignments 1 and 2. For Workshop B, we use unsupervised **K-Means clustering** to explore whether similar environmental measurements form understandable groups.

**Research question:** Can K-Means identify meaningful groups of growing conditions in the Crop Recommendation Dataset, and how are crop labels distributed among those groups?

The Kaggle Crop Recommendation Dataset has **2,200 observations, seven numeric variables, and 22 crop labels** (100 observations per crop label). The clustering model uses only **rainfall** and **humidity**, not the crop labels. Labels may be used after fitting to describe which crops appear in each group.

**Interpretation boundary:** Clusters describe patterns in this dataset. They do not establish causation, validated agricultural suitability, irrigation requirements, or real-world farm recommendations. The dataset does not define its rainfall measurement interval, location, sampling design, or season.

## 2. Team members, responsibilities, and speaking order

| Member | Student ID | GitHub username | Assigned Workshop B work | Presentation |
|---|---|---|---|---|
| **Ubaid Ullah** | **9110715** | [`UbaidUllah777`](https://github.com/UbaidUllah777) | Project introduction; data-quality assessment and EDA; choose and justify two variables; z-score standardization; elbow chart, silhouette validation, candidate-K scatter comparisons; recommend K | **First: 0:00–3:00** |
| **Rangeetha** | **9081357** | [`rangeethasajeer-debug`](https://github.com/rangeethasajeer-debug) | Fit final K-Means model; explain final cluster scatter plot and centroids; profile groups using all relevant variables and crop labels; give evidence-based cluster names and key interpretations | **Second: 3:00–6:00** |
| **Koushik Balne** | **9087547** | [`koushikbalne97`](https://github.com/koushikbalne97) | Independently check cluster counts and notebook reproducibility; document limitations and concise concluding insights; assist with final review and integration | **Third: 6:00–7:00** |

Roles describe the agreed work division, **not proof of completion**. Actual work and review evidence must come from real commits, issues, and pull requests. All members should understand the entire notebook and be able to answer questions about it.

## 3. Work completed and recorded results

### Ubaid — Analysis and K selection

The following work is included in Ubaid's open pull request [#3](https://github.com/UbaidUllah777/Crop_Recommendation_Analysis/pull/3), from `workshop-b/ubaid-data-scaling` into `assignment-3-kmeans-workshop-b`:

- Loaded the original CSV and checked data types, missing values, duplicates, and reasonable numeric ranges.
- Explored distributions and scatter plots, including rainfall versus temperature and rainfall versus humidity.
- Selected **rainfall (mm)** and **relative humidity (%)** as the two clustering inputs, with a moisture-related research rationale. Weak Pearson correlations alone were **not** treated as evidence of clustering quality.
- Applied **z-score standardization** to both inputs, following the class-demonstrated method; retained original units for interpreting results.
- Evaluated K-Means inertia for **K = 1–10**, with reproducible `random_state=42` and `n_init=10`.
- Produced the elbow chart and compared scatter plots for **K = 3, 4, 5, 6**.
- Calculated sampled silhouette scores (1,000 observations) for K = 2–10 and subsequently verified **full-dataset silhouette scores** for the shortlisted K = 3–6 models.

| K | Full-data silhouette score | Inertia (WCSS) | Smallest cluster | Largest cluster |
|---|---:|---:|---:|---:|
| 3 | 0.485 | 1,413.29 | 430 | 1,295 |
| 4 | 0.462 | 1,030.73 | 244 | 969 |
| 5 | 0.478 | 757.56 | 240 | 552 |
| **6** | **0.508** | **552.36** | **190** | **541** |

**Recommended K = 6.** The elbow chart has an early bend near K = 3, but K = 6 had the highest full-dataset silhouette score **among the shortlisted K values**, acceptable group sizes for this dataset, and visually distinguishable rainfall–humidity regions. This is a defensible recommendation, **not proof that K = 6 is universally optimal or agriculturally useful**. Final cluster profiling must establish whether the groups are interpretable.

**Verification status:** The numerical results above were produced in the notebook and shared during analysis. A complete independent fresh-kernel run and peer review are still to be confirmed; neither should be marked complete without checking.

### Remaining work — not yet reported as completed

- **Rangeetha:** Final K = 6 fit, cluster assignment to observations, centroid values in original units, profiles across all seven numeric variables, crop-label breakdown, descriptive names, figures, evidence-supported interpretation.
- **Koushik:** Independent validation, limitations, conclusion, notebook rerun verification, and final integration review.
- **Team:** Peer reviews and merges, final README update, seven-minute rehearsal, and submission of the exact validated notebook.

Do not present these tasks as finished until the actual results and supporting commits exist.

## 4. Rubric coverage and notebook acceptance checks

| Requirement | Evidence / acceptance criterion | Current state |
|---|---|---|
| Team identity | All names and IDs in the opening Markdown cell | Included in Ubaid's notebook work; verify final notebook |
| Setup and data source | Imports, relative dataset path, clear data checks and reproducible execution | Implemented; fresh-run verification pending |
| Connection to prior project | Clear research question and why clustering adds insight beyond earlier comparisons | Implemented; review wording in final version |
| Two-variable justification | Distribution review and explicit reasons for rainfall + humidity | Implemented |
| Standardization | Class-demonstrated z-score, why distance scaling matters, before/after evidence | Implemented |
| Selecting K | Elbow chart, further assessment, candidate visualizations and nuanced decision | Implemented; recommended K = 6 |
| Final visualization | Correct fitted K = 6 assignments and centroids | Rangeetha's work pending |
| Comprehensive cluster summary | All seven numeric variables, crop-label distribution, cluster sizes and evidence-based names | Rangeetha's work pending |
| Interpretation | Accurate findings, uncertainty, and agricultural limitations | Partially implemented; final profile-dependent insights pending |
| Collaboration | Real separate branches, commits, reviewed PRs and recorded feedback | PR #3 open; further evidence pending |
| Presentation | Seven-minute walkthrough using the submitted notebook, clear speaking turns | Plan established; rehearsal pending |
| Submission | Exact tested `.ipynb`, GitHub link, on time | Pending |

Avoid adding redundant plots or claiming the final K is certain. Each result shown in the notebook should connect to the research question, methodological decision, or cluster interpretation.

## 5. GitHub collaboration workflow

**Repository:** [Crop_Recommendation_Analysis](https://github.com/UbaidUllah777/Crop_Recommendation_Analysis)

**Branch roles:**

- `main` — preserve completed Assignments 1 and 2 while Assignment 3 is in progress.
- `assignment-3-kmeans-workshop-b` — Assignment 3 integration branch; merge reviewed work here.
- `workshop-b/ubaid-data-scaling` — Ubaid's analysis branch, PR [#3](https://github.com/UbaidUllah777/Crop_Recommendation_Analysis/pull/3).
- `workshop-b/rangeetha-kmeans` — Rangeetha's individual work branch (create from the updated integration branch after PR #3 merges, or safely update an existing branch).
- `workshop-b/koushik-cluster-summary` — Koushik's individual work branch (create from the latest integration branch when it is his turn).

### Sequence for the shared notebook

1. **Ubaid:** Finish his notebook and documentation corrections; push them to his personal branch. PR #3 already targets the integration branch.
2. **Rangeetha:** Review the actual changes in PR #3, leave substantive comments or approval, and merge after resolving any issues. Do not treat a review request as an approval.
3. **Rangeetha:** Pull the latest `assignment-3-kmeans-workshop-b`, then start or update her **own** feature branch. Add her notebook section, make meaningful commits, and push. Open a PR targeting `assignment-3-kmeans-workshop-b`, requesting Ubaid's review.
4. **Ubaid:** Review Rangeetha's notebook outputs, methodology and documentation, request fixes if needed, and merge only after review.
5. **Koushik:** Branch from the latest integration branch, add his verification and conclusion, commit/push, and open a PR for a teammate to review and merge.
6. **Team:** Run the integrated notebook from a fresh kernel, check the final README and all outputs, rehearse, then merge into `main` only when the completed Assignment 3 is ready.

**Conflict prevention:** Since all team members edit the same `.ipynb`, avoid simultaneous editing of that notebook. Work in sequence on the latest integration branch snapshot. Independent planning, review, documentation, and rehearsal can occur in parallel. Avoid force-pushing teammates' work and don't commit directly to `main` for Workshop B.

**Evidence:** Record real issue links, commit links, PR numbers, reviewer comments and approvals. A possible `collaboration/Workshop_B_review_log.md` can be created if the team actually uses it; do not list it as an existing file until committed. Do not fabricate co-authors, meetings, tests, or reviews.

## 6. Seven-minute notebook presentation

The earlier assignments already introduced the dataset. Limit the recap to **15–20 seconds**, then emphasize what the graphs and analyses tell us. Do not read through every line of code; each presenter must still understand their own code and answer questions.

| Time | Presenter | Notebook focus | Main talking points |
|---|---|---|---|
| **0:00–0:20** | Ubaid | Research question / data | Same dataset; new question: can environmental measurements form meaningful groups? |
| **0:20–1:10** | Ubaid | EDA and variable choice | Why rainfall + humidity; what visual comparison showed; why this is exploratory, not crop prediction |
| **1:10–2:00** | Ubaid | Original and standardized data | K-Means uses distances; differing units require scaling; z-scores give comparable scales |
| **2:00–3:00** | Ubaid | Elbow, silhouette and K comparison | Elbow bends near 3; full-data silhouette favours 6 among shortlisted models; explain trade-off and recommendation |
| **3:00–3:50** | Rangeetha | Final K-Means model and scatter | How assignments and centroid markers show groups in rainfall–humidity space |
| **3:50–4:50** | Rangeetha | Cluster centres and sizes | Explain groups in original rainfall and humidity units, avoiding overinterpretation |
| **4:50–6:00** | Rangeetha | Full cluster profiles | Use all variables, crop labels, cluster names and a small number of defensible insights |
| **6:00–7:00** | Koushik | Conclusions and limitations | Summarize major findings, uncertainty, and what further real-world validation would require |

**Timing:** Rehearse to finish substantive content by around 6:30–6:45 and reserve the remaining seconds for notebook navigation and transitions. Actual explanations must be revised to reflect the final integrated results. Each student should be ready for questions about the entire analysis.

## 7. Lessons from Workshop A

Previous feedback identified lost marks for unclear linkage between the problem and statistical test, going over time, difficulty answering questions, and insufficient collaboration evidence, even though technical work was strong.

For Workshop B, our safeguards are:

- Show the research question before explaining the method.
- Explain **why** each pair of variables, scaler and K value was chosen.
- Interpret plots instead of narrating implementation details.
- Limit claims to observed data, including the distinction between crop labels and unsupervised clusters.
- Keep authentic, reviewable contributions in GitHub.
- Rehearse the seven-minute live demonstration together.

## 8. Final quality and submission checklist

- [x] Define the project question and reuse the original dataset without rewriting earlier assignments.
- [x] Review data quality, EDA, and choose rainfall + humidity.
- [x] Explain and apply class-demonstrated z-score standardization.
- [x] Evaluate K = 1–10 with inertia and plot the elbow.
- [x] Compare candidate models visually and with silhouette validation; recommend K = 6 with caveats.
- [ ] Confirm Ubaid's documentation changes and independent notebook review; merge PR #3 after review.
- [ ] Complete final K = 6 cluster fit and scatter/centroid explanation.
- [ ] Create whole-dataset cluster profiles, crop-label analysis and defensible cluster names.
- [ ] Verify the final notebook from **Restart Kernel → Run All**, with no errors and no missing output.
- [ ] Confirm the notebook and README make consistent, supported claims.
- [ ] Complete genuine individual commits, peer reviews and pull-request merges.
- [ ] Independently verify results, write the conclusion, and document meaningful limitations.
- [ ] Rehearse the seven-minute team presentation and prepare for questions.
- [ ] Submit the exact final `.ipynb` and repository link before the applicable deadline.

**Status note (November 1, 2026):** Ubaid's evaluation work is in PR #3 and recommended K = 6 is supported by the reported results. Teammates' final sections, completed peer reviews, integration verification, rehearsal and submission are **not** asserted to be complete.
