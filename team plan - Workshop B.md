# Team Plan — Problem Analysis Workshop B (K-Means Clustering)

**Course:** PROG8431 — Data Analysis, Mathematics, Modeling and Algorithms  
**Project:** Crop Recommendation Analysis  
**Assignment:** Problem Analysis Workshop B  
**Working branch (proposed):** `assignment-3-kmeans-workshop-b`  
**Submission:** Jupyter notebook and repository URL. No ZIP submission.  
**Deadline:** eConestoga displays November 5, 2026 at 8:30 PM; the PDF says before November 5, 10 PM. Use earlier portal time unless instructor confirms otherwise.  
**Presentation:** 7 minutes, with the submitted notebook (no PowerPoint). The PDF also contains an inconsistent 5-minute phrase; the explicit presentation instructions say 7 minutes.

## 1. Team and ownership

| Member | Student ID | GitHub username | Proposed primary task | Presentation |
|---|---|---|---|---|
| Ubaid Ullah | 9110715 | `UbaidUllah777` | Research framing; source verification; variable selection rationale; standardization with clear justification; integration and quality review | First (0:00–3:00) |
| Rangeetha | 9081357 | `rangeethasajeer-debug` | K-Means implementation; elbow and supporting cluster evaluation; scatter plots; draft cluster interpretation | Second (3:00–6:00) |
| Koushik Balne | 9087547 | `koushikbalne97` | Check dataset quality; review cluster counts and descriptive profiles; prepare clear limitations/conclusion; verify notebook run | Third (6:00–7:00) |

**Ownership is a proposal, not proof of completed work.** Everyone should contribute commits, review a teammate's work, understand the full notebook, and be able to make basic code changes. Do not claim anyone reviewed or attended a meeting unless it actually occurred.

## 2. Continuity from earlier assignments

- Assignment 1: `assignment 1.ipynb` — exploratory analysis, cleaning, statistics and visualizations.
- Assignment 2: `Crop_Recommendation_Workshop_A.ipynb` — rainfalls of rice vs maize, normality, F-test, Welch t-test, p-values and communication.
- Workshop B: new notebook `Crop_Recommendation_Workshop_B.ipynb`, based on the same `Crop_recommendation.csv` and extending the project with unsupervised K-Means clustering.
- **Do not overwrite or revise old submitted notebooks** for Workshop B.

**Proposed question:** Can K-Means identify meaningful groups of growing conditions, and how are crop labels distributed among those groups?

**Important:** K-Means produces clusters of similar input measurements, not verified growing requirements or a trained supervised crop recommender.

## 3. Rubric-to-notebook checklist

| Professor requirement | Planned work and acceptance evidence |
|---|---|
| 3(a): Names/IDs first | First notebook Markdown cell includes all three members and IDs |
| 3(b): Setup | Explicit imports, reproducibility settings, dependencies, relative paths; fresh-run validation |
| 3(c): Refine data source | Reuse the committed Kaggle CSV; inspect missing, duplicates, data types, distribution, and limitations; add sources only if justified |
| 3(d): Follow class demonstration | Match techniques and sequence in the Week 7 clustering demo; document any deviations |
| 3(e): Explain clustering value | Markdown explains what grouping similar field conditions can reveal and cannot prove |
| 3(f): Choose two variables | Select *after reviewing the demonstration and distributions*; explicitly justify both; show units and cluster-centre interpretation |
| 3(g): Describe and standardize | Inspect before-scaling summary/plots; use one of the **two class-demonstrated methods**; explain why and show after-scaling checks |
| 3(h): Choose k | Run K-Means; elbow plot plus class-supported secondary assessment; justify final k and show scatter plots |
| 3(i): Summary and names | Profile clusters across **all available features**, not only the two clustering variables; assign descriptive, evidence-based names and discuss limitations |
| 3(j): Other algorithms | Prefer class-demonstrated algorithms; if deviating, document and be ready to explain differences |
| 4: Presentation | Rehearse a 7-minute live notebook walkthrough; each member has a working laptop and knows entire workflow |

**Don't predetermine the two variables, scaler or number of clusters:** choose them after inspecting the demonstration code and the data; explain tradeoffs.

## 4. Individual PR / issue workflow (proposed)

Use one GitHub issue for each scoped task, with an owner, checklist, and links to the completing PR. Examples:

1. **Issue A — Data, question, and standardization**, owner Ubaid, reviewer Rangeetha. Branch `workshop-b/ubaid-data-scaling`.
2. **Issue B — K-Means and evaluation**, owner Rangeetha, reviewer Ubaid. Branch `workshop-b/rangeetha-kmeans`.
3. **Issue C — Cluster profile and conclusion**, owner Koushik, reviewer Rangeetha. Branch `workshop-b/koushik-cluster-summary`.
4. **Issue D — Integration and seven-minute rehearsal**, shared task. Track real contributions in comments and the final PR.

PR description should include: linked issue, changed files, approach, screenshots/plots if useful, how it was tested, and outstanding limitations. Have another member leave a **real** approval or substantive review comment before merging into the Workshop B integration branch. Never fabricate reviews, co-author lines, meetings, or time entries.

**Suggested log:** `collaboration/Workshop_B_review_log.md` with date, task, participant, evidence (issue/PR/commit link), review decision, and whether any follow-up was needed. Only add genuine records.

## 5. Branch structure

- `main`: stable Assignment 1 and Workshop A materials.
- `assignment-3-kmeans-workshop-b`: Workshop B integration branch, created from `main`.
- `workshop-b/ubaid-data-scaling`: Ubaid's individual feature branch.
- `workshop-b/rangeetha-kmeans`: Rangeetha's individual feature branch.
- `workshop-b/koushik-cluster-summary`: Koushik's individual feature branch.

A personal branch is **not** a substitute for a PR or substantive review. Start teammates' branches from the current integration branch, coordinate notebook cell editing to minimize merge conflicts, and pull changes before coding.

## 6. Presentation structure — 7 minutes

| Presenter | Time | Show in submitted notebook | Key message |
|---|---|---|---|
| Ubaid | 0:00–3:00 | Team/title; focused research question; dataset checks; two variables; before/after standardization | What problem we ask, what two dimensions we chose, and why scaling is appropriate |
| Rangeetha | 3:00–6:00 | K-Means cell; elbow; secondary evaluation; scatter plots; cluster descriptions | Why this number of clusters and what patterns were found |
| Koushik | 6:00–7:00 | All-feature cluster summary, limitations and conclusions | What the clusters mean, what they do not prove, and how to investigate next |

**Rehearsal targets:** practice with a 6:30–6:45 target to leave room for notebook navigation; hard stop by 7:00. Present only key cells/charts, not every line. Every member keeps a backup notebook copy and tests the classroom connection. All members practice questions about scaling, k selection, feature choice, cluster labels, and limitations.

## 7. Feedback from Workshop A to address

Prior rubric: technical work scored well; the team lost marks for unclear connection between the problem and test, notebook narrative, exceeding time, difficulty answering questions, and individual collaboration evidence. Workshop B remedies: put the research question above the clustering procedure, explicitly connect every plot to the decision, assign speakers and rehearse, and retain authentic issue/PR/review evidence.

## 8. Review gates

- [ ] Inspect Unit 4 and Unit 5 notes and Week 7 demonstration notebook; verify chosen APIs match class.
- [ ] Verify data file, imports, and fresh-kernel run.
- [ ] Keep all values and selection/scaling decisions reproducible.
- [ ] Confirm all deliverable Markdown explanations and plots exist.
- [ ] Confirm proposed clusters are justified, correctly named, and profiled using the whole dataset.
- [ ] Peer-review all code and narrative; track actual review links.
- [ ] Rehearse 7 minutes and practice professor questions.
- [ ] Submit the exact `.ipynb` used for the presentation, plus the GitHub repository URL.
