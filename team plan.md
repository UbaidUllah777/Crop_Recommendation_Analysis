# Shared team plan: Crop Recommendation Analysis — New Lab

## Team details

| Member | Name | Student ID |
|---|---|---|
| Member 1 | Koushik | 9087547 | 
| Member 2 | Rangeetha | 9081357 |
| Member 3 | Ubaid | 9110715 | 



## Aim and scope

Use all analysis sections from `assignment 1.ipynb` as the foundation for the new lab. Retain the object-oriented `CropAnalyzer` approach, statistical profiling, box-whisker plots, rainfall histogram/KDE, temperature–humidity scatter plot, three-set Venn diagram, and analytical discussion. Add the current lab's distributions, normality, variance, and mean comparisons. The discontinued Z-score task remains removed.

**Audience:** A proposed regional agricultural planning committee, agricultural extension officers, public-sector analysts, and farmer-association representatives.

**Expected outcome:** Identify dataset patterns that motivate local agricultural water-planning investigations. 

**Broad question from the assignment:** Which soil and environmental factors are associated with crop labels? The inherited exploratory sections display patterns but do not rank the strongest predictors.

**Focused question for the new lab:** For the statistical testing required in this lab, we compare rainfall values for rice and maize records. Use the same variable and groups throughout Sections 11–14.

## Mapping the reference notebook to the new notebook

| Reference section | New section | What is reused or improved |
|---|---|---|
| Project Overview & Use Case Summary | 1 | Crop-analysis context, updated public-sector audience and limitations |
| Research Question | 2 | Broad question plus the focused rainfall question; all four planning questions retained |
| Methodology & Notebook Structure | 3 | Original analysis sequence extended with the new lab requirements |
| Imports & Global Configurations | 4 | NumPy, pandas, SciPy, plotting, Venn support, reproducibility settings |
| Data Ingestion & Cleansing | 5–7 | Source, loading, quality checks, descriptive names; rounding only for display |
| Statistical Profiling & Object-Oriented Analysis | 7 | CropAnalyzer, mean, median, mode, sample variance/SD, quartiles, summary table |
| Visual Analytics & Graphical Presentations | 8 | All four original visual types and the same six selected crops |
| Key Analytical Insights & Discussion | 9 | Four original discussion topics, with corrected and recomputed statements |
| New lab requirements | 10–18 | Expanded histograms, QQ/Shapiro, F/Levene, Welch t, interpretations, normalization discussion, Whiteboard, presentation, references |

## Three-member work allocation

| Member | Ownership | Concrete responsibilities | Peer reviewer |
|---|---|---|---|
| 1 | Sections 1–7 | Finalize framing; verify source and setup; inspect cleansing; explain descriptive renaming and full precision; review CropAnalyzer and all descriptive measures | Member 2 |
| 2 | Sections 8–11 | Review all four inherited visualizations and their discussion; check Venn set logic; explain seven-variable histograms and rice/maize plots; interpret QQ plots and Shapiro–Wilk | Member 3 |
| 3 | Sections 12–18 | Review F and Levene assumptions; verify Welch calculations and confidence interval; explain p-values and normalization; align conclusions, Whiteboard and presentation | Member 1 |

Member 1 leads reproducibility checks, Member 2 checks figure readability, and Member 3 combines the final notebook. Everyone reviews the complete work and can present any section. Ownership is not an exemption from understanding another member's code.

## Required deliverables by member

### Member 1: Data and statistical foundation

- Replace team placeholders in the opening Markdown cell and this plan.
- Explain why this dataset is suitable for an exploratory classroom lab and why it cannot support the original food-price timeframe.
- Verify package setup, relative file paths, checksum, and optional source-download comparison.
- Confirm 2,200 records, 22 crop labels, 100 observations per crop, and no missing entries or exact duplicates.
- Explain `df` (original column names) and `analysis_df` (descriptive names); both retain identical full-precision values.
- Explain sample variance and standard deviation (`ddof=1`), the handling of tied modes and continuous values without repeats, and the quartile convention.

### Member 2: Visual evidence and normality

- Review the nitrogen box plots for the same six crops used in the reference.
- Explain the rainfall histogram/KDE without calling the period annual.
- Explain temperature–humidity clusters without treating them as strict biological limits.
- Review the Venn diagram's strict above-median record sets and exact intersection counts. The full-precision three-way overlap is 255, whereas rounding first reproduces 254.
- Review histograms of all seven numerical variables and matching-axis rice/maize rainfall histograms.
- Explain Shapiro–Wilk hypotheses and the QQ plot departures.
- Review the **100-word normality interpretation** in Section 11. A small p-value rejects the normality model; a large one would not prove it.

### Member 3: Statistical comparisons and communication

- Verify the two-sided variance-ratio F calculation, degrees of freedom, and **50-word F-test interpretation** in Section 12.
- Explain that both crop groups reject normality, weakening the classical F-test. Identify median-centered Levene as a separate robust check.
- Verify the manual Welch t-statistic against SciPy, its degrees of freedom, p-value, and 95% confidence interval.
- Review the **100-word t-statistic interpretation** and **50-word concise t summary** in Section 13. Both retained rubric word limits are covered.
- Review the **100-word p-value assessment** in Section 14.
- Explain that numerical scaling does not produce normality and is unnecessary for a same-unit rainfall comparison.
- Align the executive result, Whiteboard, limitations, and five-minute presentation.

All word counts exclude headings and use whitespace-separated words. If text is edited, check the counts again.

## Shared statistical decisions

- Alpha = 0.05; use two-sided mean and variance alternatives.
- Fix rice and maize as the teaching comparison; do not search across crop pairs for the smallest p-value.
- Keep full precision and original observations. Do not delete observations to improve normality.
- Use rainfall in mm, with accumulation period explicitly unspecified.
- Test within-group normality; pooled normality is descriptive context.
- Keep the classical F-test for the lab, qualify its failed normality assumption, and report Levene separately.
- Use Welch's mean comparison rather than assuming equal variances. A t-statistic measures a mean difference in standard-error units.
- Interpret inferential results conditionally: independence and representative field sampling are unverified.
- Discuss differences and confidence intervals, not only p-values. The data show associations, not causal effects or crop requirements.

## Corrections from the reference to explain

1. Early rounding changes set membership and can create ties. Only presentation tables are rounded in the new analysis.
2. The first mode returned by software is not a useful unique mode when every observation occurs once. The adapted class reports this explicitly.
3. The source does not establish an annual rainfall period.
4. The six visualized crops are selected categories, not ranked top crops.
5. Above-median thresholds are relative to this dataset, not agricultural high/low standards.
6. Visual group differences do not establish optimized fertilizer, maximum yields, strict humidity requirements, or validated crop recommendations.

## Integration and review sequence

1. All three members read the notebook and agree on the scope and crop comparison.
2. Member 1 checks Sections 1–7 and hands the validated tables and class explanation to Member 2.
3. Member 2 checks visual interpretations and normality, then hands the assumption assessment to Member 3.
4. Member 3 checks comparisons and communication, then combines proposed edits.
5. Review in a cycle: Member 2 reviews Member 1, Member 3 reviews Member 2, and Member 1 reviews Member 3.
6. Run from a clean kernel on each laptop. If the dataset or group selection changes, revise the static Markdown summaries and Whiteboard after rerunning.
7. Each member explains one section they did not author and practices a small code change. Rehearse the complete presentation together.

## Five-minute presentation using the notebook

| Time | Speaker | Show | Main message |
|---|---|---|---|
| 0:00–1:30 | Member 1 | Overview, quality assessment, CropAnalyzer summary | Dataset and audience; what the measurements can and cannot support |
| 1:30–3:00 | Member 2 | Four-view visual dashboard, then group QQ plots | Inherited analysis patterns; 255-record overlap; both rainfall groups reject normality |
| 3:00–4:30 | Member 3 | F/Levene table, Welch difference plot, assessment | Variability and mean differences; limitations of inference |
| 4:30–5:00 | Any member | Whiteboard and next step | Obtain local, dated field data before policy action |

Do not narrate every code line. Keep all sections available for questions. Everyone must be ready to present the entire notebook and explain changes. Test the projector connection, required adapters, display scaling, and chart readability on all three laptops.

## Whiteboard and files

The Whiteboard draft is a local PNG ready to import into the team's chosen Teams Whiteboard. It has not been posted. Its rainfall-focused story summarizes the new lab; the inherited four-view dashboard is also available in `figures/06_reference_visual_analytics.png` for insertion or discussion.

- `Crop_Recommendation_New_Lab.ipynb`: new executed notebook, including every inherited analysis section.
- `team plan.md`: this shareable plan.
- `Teams_whiteboard_draft.png`: first report draft for Teams.
- `data/Crop_recommendation.csv`: unchanged supplied data.
- `figures/`: individual charts and the inherited-analysis dashboard.
- `requirements.txt`: tested package versions, including matplotlib-venn.

Extract the ZIP before opening the notebook. Keep its folders together. Use Python 3.12 and install `requirements.txt` into the active Jupyter environment. Restart Kernel and Run All. The source download check is optional for offline reruns and is enabled by setting `VERIFY_SOURCE_ONLINE = True`.

## Final checklist

- [ ] Team names and IDs entered in both files.
- [ ] Every inherited analysis section reviewed and understood.
- [ ] All cells execute in order on each laptop.
- [ ] Required 100-word and 50-word summaries checked after edits.
- [ ] F-test limitation, robust check, and Welch interpretation understood.
- [ ] Z-score work remains excluded.
- [ ] Notebook, Whiteboard, and oral findings agree.
- [ ] Everyone can modify the code and present any section.
- [ ] Projector connections and five-minute timing tested.

Statistical and dataset references appear in Section 18 of the notebook. The original notebook is used as analysis material; the latest lab instructions govern the deliverables.
