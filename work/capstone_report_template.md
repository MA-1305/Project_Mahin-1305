# Capstone Report

**Author:** Mahin Attar  
**Lane:** Content Refresh Prioritization  
**Repo:** `MA-1305/Project_Mahin-1305`  
**Date:** 01 August 2026  

---

# 0. Abstract

This project focuses on prioritizing existing web pages for content-refresh review using observable search and content-performance signals.

The analysis uses the FlyRank Internship Starter Dataset, a public-safe anonymized 30,000-row slice containing page-level search and content-performance features across pseudonymized clients. The project first establishes a transparent rule-based baseline and then compares it with supervised Machine Learning models.

The main ranking metric is Precision@50 because the practical decision is to identify a small set of pages that content teams should review first. The verified starter-dataset reference result shows that the rule baseline achieves Precision@50 of 0.26, while the Random Forest reaches 0.74.

The final output is a ranked decision-support queue for content editors. The model is not treated as proof that refreshing a page will cause improved search performance. Human review remains necessary before any content changes are made.

---

# 1. Problem Framing

The objective of this project is to support content-refresh decisions using Machine Learning.

**Decision Supported:** Determine which existing web pages should be reviewed first for a possible content refresh.

**Unit of Analysis:** Individual web page.

**Output:** A priority score or ranking indicating which pages should receive earlier human review.

**Human Action:** Editors review the highest-ranked pages and consider changes to content, headings, metadata, keywords, images, internal links, or other page elements.

**Cost of a Wrong Decision:** If a page is incorrectly identified as high priority, valuable editing time may be wasted. If an important page is missed, an opportunity to investigate or improve search performance may be delayed.

Machine Learning is suitable because multiple search and content signals can interact. A model can identify patterns across these signals and produce a consistent prioritization ranking.

---

# 2. Data Safety

The project uses the FlyRank Internship Starter Dataset for educational and research purposes.

The starter dataset contains 30,000 anonymized content-performance rows across pseudonymized clients. It contains numeric and categorical search/content metrics and does not include titles, URLs, keywords, domains, or client names.

The following information was deliberately excluded from the model feature set:

* Target-derived fields such as `trend_direction` and `trend_pct`.
* Product decision flags such as `health_score`, `needs_ctr_fix`, `is_quick_win`, and related fields because they can leak information about the decline label.
* `client_id` as a predictive feature. It is used only for grouped validation.
* Any information that would not be available at the intended prediction point.

No client-identifying information is included in public outputs.

---

# 3. Baseline

Before building the Machine Learning model, a transparent rule-based baseline was developed.

The baseline combines observable signals related to visibility, freshness, search position, and content depth to produce a prioritization score.

The purpose of the baseline is to provide a simple and interpretable benchmark against which the learned model can be compared.

The verified starter-dataset reference result reports:

**Rule Baseline Precision@50: 0.26**

The baseline is therefore useful as a transparent starting point, while the Machine Learning model can be evaluated on whether it improves the ranking of high-priority pages.

---

# 4. Model / Analysis

The task is treated as a classification and ranking problem.

The proxy declining label is derived from the observed trend direction:

`is_declining_label = trend_direction == "down"`

The model uses observable search and content-performance features such as:

* Search volume
* Competition
* CPC
* Impressions
* Clicks
* Sessions
* Content age
* Days since last update
* CTR
* Engagement rate
* Scroll rate
* AI traffic percentage
* Relevant categorical content and search fields

Target-derived and leakage-prone fields are excluded from the feature matrix.

A Random Forest model is used because it can capture nonlinear relationships and interactions among multiple numeric and categorical signals.

The model output is converted into a ranking so that content teams can review the highest-priority pages first.

---

# 5. Evaluation

The primary evaluation metric is **Precision@50** because the practical objective is to prioritize a limited number of pages for human review.

The verified starter-dataset reference results are:

| Method | Precision@50 |
|---|---:|
| Rule Baseline | 0.26 |
| Random Forest | 0.74 |

The Random Forest therefore provides a substantially stronger top-50 ranking than the transparent baseline on the starter dataset.

The evaluation should be interpreted as measured performance on the available anonymized starter slice. It does not establish that refreshing a recommended page will cause improved search performance.

Client-holdout validation is used where applicable to reduce the risk of information overlap between training and testing clients.

---

# 6. Interpretation

The analysis indicates that observable search and content-performance signals can provide useful information for prioritizing pages for review.

Important signals include visibility, freshness, CTR, search performance, and engagement-related measurements.

The analysis also demonstrates that commonly assumed relationships should be tested rather than assumed. For example, the starter-dataset reference results show an approximately zero correlation between `search_volume` and `impressions_90d`, indicating that search volume should not automatically be treated as a direct proxy for impressions.

The model's predictions should therefore be interpreted as evidence for prioritization rather than causal explanations.

Feature importance can help explain which variables contributed most to model predictions, but feature importance alone does not establish that a variable causes page decline.

---

# 7. Recommendation

The model should be used as a decision-support system for content editors.

Recommended workflow:

1. Generate page priority scores.
2. Rank pages by model score.
3. Review the highest-ranked pages first.
4. Check current search performance and recent content changes.
5. Evaluate search intent and content quality.
6. Decide whether a refresh is appropriate.
7. Republish approved changes.
8. Monitor subsequent search performance.

Editors should consider model scores together with business goals and editorial judgment.

The model should **not** automatically publish content, delete pages, change metadata, or make business decisions.

Confidence in the recommendations is moderate because the analysis is based on observational data and a proxy target rather than a controlled experiment.

---

# 8. Reproducibility

The project can be reproduced from the GitHub repository:

`MA-1305/Project_Mahin-1305`

The notebooks should be executed in numerical order, beginning with the task-framing and feature/leakage work and continuing through modeling, validation, and the action playbook.

Random seeds should be fixed wherever stochastic model training or splitting is used.

The required Python packages should be documented in `requirements.txt`.

The analysis should produce the relevant model outputs, validation results, ranked recommendations, and action queue under the repository's `work/` directory.

The public repository should contain only anonymized and safe outputs. Raw or client-identifying data should not be published.

---

# 9. Acknowledgments & Data Credit

This project was completed as part of the FlyRank ML Internship.

The analysis uses the **FlyRank Internship Starter Dataset (Anonymized)**, which is provided as a public-safe 30,000-row starter dataset for the internship. The dataset contains pseudonymized client/content identifiers and numeric/categorical metrics without titles, URLs, keywords, domains, or client names.

Dataset: `FlyRank/internship-starter`

The dataset is used for educational and research purposes under the FlyRank data-use conditions.

Credit is given to FlyRank for providing the dataset and internship framework.
