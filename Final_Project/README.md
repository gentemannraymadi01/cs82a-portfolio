### After controlling for age, marital status, and group affiliation, does the probability and velocity of primary online radicalization among lone-actor terrorists increase significantly in the post-algorithmic era (2011-2022) compared to the pre-algorithmic era (1999-2010)?

# Background:

Algorithms became more commonly used to rank and recommend content on major social media platforms in the early 2010s. For example, Facebook changed its ranking system around 2011 (source: https://www.newamerica.org/oti/reports/rising-through-ranks/news-feed-ranking/) and YouTube changed its recommendation system in 2012 (source: https://www.newamerica.org/oti/reports/why-am-i-seeing-this/case-study-youtube). This notebook uses 2011 as a rough dividing line.

This notebook does not show that algorithms caused any change. It compares the percent of lone offenders primarily radicalized online and speed of radicalization across two groups, 1999-2010 and 2011-2022.

# Data source

Dataset: Profiles of Individual Radicalization in the United States (PIRUS), Version 5, accessed October 2026

Citation: National Consortium for the Study of Terrorism and Responses to Terrorism (START), University of Maryland. (2023). Profiles of Individual Radicalization in the United States (PIRUS) [Data file]. Retrieved from http://www.start.umd.edu/data-tools/profiles-individual-radicalization-united-states-pirus Copyright University of Maryland 2023

License: Used in accordance with START's End User License Agreement under non-commercial academic research use. The raw data and codebook are not in this notebook. Any changes to the data are documented in the cleaning log.

# Cleaning log

| Step | Rows | Detail |
|---|---|---|
| Load raw PIRUS V5 | 3,528 | one row per individual |
| Keep lone offenders | 1,165 | `Lone_Offender == 1` |
| Keep exposure year >= 1999 | 1,091 | dropped 74; the internet variable is not applicable before 1999 |
| Define era | 1,091 | pre (1999-2010) n = 107, post (2011-2022) n = 984 |
| Recode -99 (unknown) to missing | 1,091 | Age = 14, Marital_Status = 248, Group_Membership = 11, Internet_Radicalization = 384, Rad_duration = 493 |
| Build outcomes and controls | 1,091 | `prim_online`, `fast` (< 1 year), marital status (widowed merged into divorced/separated, n = 9), group labels |
| Complete cases, main model | 607 | primary-online events = 140 |

**Variable definitions**
- `prim_online` = 1 if the internet was the primary means of radicalization (`Internet_Radicalization == 2`).
- `fast` = 1 if radicalization took under one year (`Rad_duration == 1`).
- Controls: age, marital status, and group affiliation

# Findings

Primary online radicalization was more common in 2011-2022 (22.3% vs 11.9%). After controlling for age, marital status, and group affiliation, the odds were roughly 3.3 times higher (p = 0.049). Because of the small early group and close p-value, these results are suggestive not conclusive. In regards to velocity, the proportion of people radicalized in under a year rose from 24% to 43%. Adjusted odds were about 2.3 times higher (p = 0.017). Again because people in that group have had less time to offend, people who radicalize slowly may have not offended yet and that data bias could make the later era look faster. The rates of primarily online radicalization and the proportion of people who radicalized in under a year both increased in the later group. This does not prove causation.

# Limitations

This notebook does not prove causation. It is not proof that algorithms caused a change in radicalization method or velocity. It compares two time periods meant to represent the before and after of widespread algorithm use in media recommendation and platforms changed at different times (Facebook around 2011, YouTube 2012), so the 2011 cutoff is rough. In the earlier group 60.7% of cases have an unknown internet role vs 32.4% later, while error bars and p-values do represent the uncertainty caused by this the direction of any bias is not known. After controlling for other factors the early group is small, with only 3 primary-online cases in the 1999-2010 group, while the p = 0.049 is still technically statistically significant the result is borderline and should be read as suggestive. Also the velocity result could be biased. Because people in the later group have had less time to offend(2011-2022 < 1999-2022), people who radicalize slowly may have not offended yet. That data bias could contribute to the later era looking faster.

# Ethics

No names or identifying information were used in this notebook. The dataset is built from public open source records and has no direct identifiers. The raw data and codebook are not redistributed. The repo has instructions for downloading them.

# How to run

1. Download PIRUS V5 from [START](http://www.start.umd.edu/data-tools/profiles-individual-radicalization-united-states-pirus) and save it as `PIRUS V5.xlsx` in the repo root.
2. Install dependencies: `pip install numpy pandas matplotlib statsmodels openpyxl jupyter`
3. Open `Final_Project.ipynb` and run all cells. Figures are saved to `figures/`.
