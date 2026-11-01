# Shared Team Plan — Crop Recommendation Analysis
## Workshop A (Assignment 2): Final documentation and handoff to Workshop B

> This document records the existing Assignment 2 work and prepares a documented workflow for Assignment 3. It does **not** retroactively claim unrecorded approvals, meetings, or code contributions. Workshop A notebooks remain unchanged.

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
| `team plan.md` | Team responsibilities and workflow |
| `requirements.txt` | Python package dependency list **once committed** |

**Setup check:** Install dependencies with `python -m pip install -r requirements.txt`, launch Jupyter from the repository root, and use Restart Kernel → Run All. The executed notebook expects `Crop_recommendation.csv` at the repository root and does not automatically download the Kaggle dataset. Do not state that a fresh-environment test succeeded until someone performs and records it.

## 7. Assignment 2 presentation and assessment lessons

The instructor's screenshot of Workshop A feedback reports strong coding and analysis scores, but lower marks for narrative clarity, presentation timing, question responses and individually assessed collaboration. The screenshot reports: notebook presentation guide 1/2, presentation attendance/participation/timing 0.5/2, question responses 1/2 and collaboration 2/6, with a displayed overall score of 12.5/20 (62.5%). These are historical feedback items, not predictions for Workshop B.

**Changes for Workshop B:**
1. State the problem/question in one sentence before demonstrating charts or code.
2. Link every test or chart to that question and an actionable interpretation.
3. Rehearse a timed seven-minute notebook-only presentation, with a backup presenter ready.
4. Practise explaining and making a small code change live in every teammate's sections.
5. Keep dated issue discussions, PR descriptions, reviews/approvals and meeting notes so individual collaboration is visible.

## 8. Workshop B collaboration protocol (to use from now on)

**Working branch:** `assignment-3-kmeans-workshop-b` (create from `main`; no branch is claimed as created until it appears on GitHub).

**For each meaningful task:**
1. Create a GitHub Issue describing the deliverable, acceptance criteria, owner and deadline.
2. Make changes in a separate descriptive task branch (e.g. `workshop-b/data-standardization`).
3. Open **one pull request per task**, reference its issue (`Closes #...` when appropriate), and describe actual work, screenshots or outputs, and testing.
4. Ask another teammate to review. Record a real comment or approval before merging; do not invent reviews or approvals.
5. Merge approved changes into the shared Workshop B working branch. The team then reviews a final PR to `main` when ready.
6. For genuine paired changes, describe shared work in the PR and use `Co-authored-by` trailers only if both authors actually contributed to that commit.
7. Maintain an issue/PR evidence log in `docs/workshop_b_collaboration.md` with dates, meeting decisions, review evidence and links.

**Proposed owners for Workshop B (confirm together before opening assigned issues):** Koushik — data inspection and standardization; Rangeetha — variable choice and clustering visualizations; Ubaid — cluster evaluation, interpretation, notebook narration, submission coordination. All three review one another's work and prepare for questions. These are proposed future roles, not work already completed.

## 9. Workshop B deliverables to track

- Read Unit 4 Time Series and Unit 5 Clustering; run the instructor's demonstration.
- Keep team names/IDs at the top of the new notebook; include setup and compatible data loading.
- Explain in markdown how clustering will deepen project understanding.
- Choose and justify two clustering variables.
- Examine and standardize input features using a class-taught method, with justification.
- Use instructor-style K-means, elbow chart, scatter plots and any further evaluation needed to justify the number of clusters.
- Summarize **all clusters**, give descriptive names and discuss insights using other relevant dataset columns.
- Present **the same submitted Jupyter Notebook** in seven minutes. Every member must connect to the projector, understand the code and be ready for questions.
- Submit the notebook unzipped and include the GitHub repository link before the posted deadline.

## 10. Presentation and review record template (fill in with real evidence)

| Date | Task / decision | Participants | Issue / PR link | Reviewer and actual feedback | Status |
| --- | --- | --- | --- | --- | --- |
| TBD | Assign clustering tasks | TBD | TBD | TBD | Planned |
| TBD | Review feature scaling | TBD | TBD | TBD | Planned |
| TBD | Review number of clusters | TBD | TBD | TBD | Planned |
| TBD | Timed seven-minute rehearsal | TBD | TBD | TBD | Planned |

Do not replace placeholders with invented meetings, completed tests or approvals.

## 11. Next steps

1. Commit this updated `team plan.md`, the cleaned `README.md` and the new `requirements.txt` as documentation-only changes.
2. Verify a fresh local run of Workshop A, noting any dependency or path errors; preserve the submitted notebook unless changes are explicitly agreed.
3. Create the Workshop B branch, issues and task branches.
4. Work through the new PDF and instructor's clustering demonstration before choosing the clustering scheme.
