# Capstone Report

**Author:** Mahin Attar
**Lane:** Content Refresh Prioritization
**Repo:** `<MA-1305/Project_Mahin-1305>`
**Date:** 01 August 2026

---

# 0. Abstract

This project focuses on predicting which existing web pages should be prioritized for content updates to improve search performance. The analysis was performed using the FlyRank Machine Learning Internship dataset containing approximately 79 million rows of production search data. A rule-based baseline was first created and then compared with a supervised Machine Learning model trained on carefully selected features while avoiding data leakage. The Machine Learning model achieved better predictive performance than the baseline and identified the most important factors affecting page refresh priority. The final output is a ranked list of pages that helps FlyRank editors and SEO teams decide which pages should be refreshed first.

---

# 1. Problem Framing

The objective of this project is to support content refresh decisions using Machine Learning.

**Decision Supported:** Determine which existing web pages should be updated first.

**Unit of Analysis:** Individual web page.

**Output:** A priority score or ranking indicating the likelihood that a page should be refreshed.

**Human Action:** Editors review the highest-ranked pages and update content, headings, metadata, keywords, images, or internal links.

**Cost of a Wrong Decision:** If a page is incorrectly identified as high priority, valuable editing time is wasted. If an important page is missed, the website may lose opportunities to improve search visibility and user engagement.

Machine Learning is suitable because many factors influence page performance simultaneously, making manual prioritization difficult. A trained model can learn patterns from historical data and produce consistent, data-driven recommendations.

---

# 2. Data Safety

The project uses the FlyRank ML Internship dataset for research and educational purposes.

To ensure fair model training, only relevant predictive features were used.

The following information was deliberately excluded:

* Label-derived columns such as `trend_direction` and `trend_pct` because they directly contain target information.
* Client identifiers and pseudonymous IDs, which were used only for grouping during validation and never as input features.
* Any feature that could reveal future information unavailable at prediction time.

No client-identifying information is stored or published in the `work/` directory or anywhere in the repository.

---

# 3. Baseline

Before building the Machine Learning model, a simple baseline approach was developed.

The baseline assigns page priority using transparent rules based on existing page metrics. This provides an easy-to-understand benchmark for comparison.

Both the baseline and the Machine Learning model were evaluated using the same train-test split and identical evaluation metrics.

The Machine Learning model demonstrated better predictive performance than the baseline, showing that learning patterns from multiple variables provides more accurate prioritization than simple rule-based methods.

---

# 4. Model / Analysis

A supervised Machine Learning model was trained to predict content refresh priority.

The model used features describing page performance and search behaviour while excluding information that could introduce data leakage.

Example features include:

* Clicks
* Impressions
* Click-Through Rate (CTR)
* Average Position
* Search Volume
* Content Freshness Indicators
* Historical Performance Metrics

Excluded features include:

* `trend_direction`
* `trend_pct`
* Client identifiers
* Any target-derived information

**Target Definition:** The model predicts whether a page should receive higher priority for content refresh based on historical search performance.

---

# 5. Evaluation

The dataset was divided into separate training and testing datasets using an appropriate validation strategy that prevented information leakage.

The following evaluation metrics were used:

* Accuracy
* Precision
* Recall
* F1 Score
The Machine Learning model consistently outperformed the baseline using the same evaluation split.

Error analysis showed that most incorrect predictions occurred for pages with performance values close to the decision boundary, where distinguishing between medium- and high-priority pages is naturally more difficult.

These results indicate that the model provides useful decision support while still requiring human review for uncertain cases.

---

# 6. Interpretation

Feature importance analysis showed that search performance metrics contributed most strongly to the predictions.

The model learned several useful patterns:

* Pages showing declining search performance often received higher refresh priority.
* Pages with low click-through rates despite strong visibility frequently benefited from content updates.
* Historical engagement metrics were important indicators of refresh opportunity.
* Some variables expected to influence performance contributed very little, showing that not every commonly assumed SEO factor has measurable predictive value.

These findings help explain why the model recommends certain pages and improve confidence in its predictions.

---

# 7. Recommendation

The model should be used as a decision-support system for content editors.

Recommended workflow:

1. Generate page priority scores.
2. Review the highest-ranked pages.
3. Update page content, titles, metadata, and internal links.
4. Republish updated pages.
5. Monitor search performance after the refresh.

Editors should prioritize pages receiving the highest model scores while also considering business goals and editorial judgement.

Confidence in these recommendations is moderate because they are based on historical observational data rather than controlled experiments.

The model should assist human decision-making rather than replace it.

---

# 8. Reproducibility

The complete project can be reproduced using the following steps.

```bash
git clone <Project_Mahin-1305>

cd <Project_Mahin-1305>

pip install -r requirements.txt

jupyter notebook
```

Run all notebooks in numerical order until the final evaluation notebook completes.

Random seeds were fixed during model training to ensure reproducibility.

The software environment is documented through the included `requirements.txt` file.

If a sealed or holdout evaluation is included, both the script that creates the evaluation dataset and the generated metrics file are committed to the repository so that the evaluation process can be independently verified.

---

# 9. Acknowledgments & Data Credit

This project was built using the **FlyRank ML Internship Dataset**.

Data source: **[https://flyrank.ai](https://huggingface.co/datasets/FlyRank/internship-warehouse)**

The FlyRank dataset was used solely for educational and research purposes during this Machine Learning internship. Credit is given to FlyRank for providing the dataset used throughout this capstone project.

---


