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
| Ubaid Ullah | 9110715 | `UbaidUllah777` | Brief project recap; data quality and selection of two clustering variables; standardization; candidate k evaluation with elbow chart and justification | First (0:00–3:00) |
| Rangeetha | 9081357 | `rangeethasajeer-debug` | Final K-Means model and cluster visualization; supporting evaluation and validation; cluster profiles across all variables; descriptive cluster naming and key insights | Second (3:00–6:00) |
| Koushik Balne | 9087547 | `koushikbalne97` | Independently check cluster counts and notebook rerun; present concise limitations, conclusion and follow-up action | Third (6:00–7:00) |

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

1. **Issue A — Data, feature choice, scaling and elbow comparison**, owner Ubaid, reviewer Rangeetha. Branch `workshop-b/ubaid-data-scaling`.
2. **Issue B — Final K-Means solution, validation, scatter plots and all-feature cluster profiles**, owner Rangeetha, reviewer Ubaid. Branch `workshop-b/rangeetha-kmeans`.
3. **Issue C — Cluster count verification, limitations and conclusion**, owner Koushik, reviewer Rangeetha. Branch `workshop-b/koushik-cluster-summary`.
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

## 6. Presentation structure — 7 minutes (result-first, not code-first)

The audience has already heard the earlier project presentations. Spend **15–20 seconds maximum** reminding them that the team reuses the crop dataset and is now looking for groups of similar growing conditions. Most presentation time goes to *what was done, why, what the plots show, what was decided, and what the results mean*. Do **not** narrate code line-by-line. All team members must still understand the code and be prepared to modify it when questioned.

| Presenter | Time | Show in the **submitted** notebook | Evidence and explanation |
|---|---|---|---|
| **Ubaid (first)** | **0:00–3:00** | Focused question (briefly), data checks, selected two features, before/after standardization, elbow chart | 0:00–0:20: connect to previous work. 0:20–1:10: explain selected variables and why they suit clustering. 1:10–2:00: show why and how standardization was needed, supported by before/after results. 2:00–3:00: interpret the elbow and explain candidate k values and selection tradeoffs. |
| **Rangeetha (second)** | **3:00–6:00** | Final K-Means clustering, optional class-supported second assessment, scatter plots, centroid locations, comprehensive cluster profile and names | 3:00–3:50: explain the chosen k and what K-Means did (not each code statement). 3:50–4:50: interpret scatter plots and centers. 4:50–6:00: compare clusters across all dataset features, give defensible descriptive names, and explain useful patterns and exceptions. |
| **Koushik (third)** | **6:00–7:00** | Final findings, limitations and next steps | State two or three supported insights, explain why clusters are not proven crop prescriptions, and close with what local data or validation would be needed. |

**Do not manufacture results in advance.** Final features, scaler, cluster count, cluster names and observed patterns must be determined only after running the class-demonstrated analysis. Adapt the speaking examples to real outputs.

**Rehearsal:** aim to finish the actual material in 6:30–6:45, leaving navigation buffer before the hard 7:00 cutoff. Transitions should take only a few seconds. Each member should rehearse questions about any part of the notebook, not just their own.

**Workload balance:** Ubaid and Rangeetha each own a comparable technical and interpretive package, although the code volume may differ. Koushik has a smaller *speaking* package but must make a verifiable contribution and be ready for questions. Peer review must be genuine and recorded.

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
