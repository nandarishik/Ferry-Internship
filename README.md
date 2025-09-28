# Ferry-Internship
# The Adherence-AI Project: A Research Journal
**Lead Researcher:** Nanda  
**Project Start Date:** August 2025  
**Status:** Completed

---

## 1. Introduction & Background
**The Problem:**  
Medication non-adherence is a persistent challenge in healthcare. For patients managing chronic conditions like anemia, failing to follow a prescribed regimen can lead to severe health complications, hospital readmissions, and reduced quality of life. Non-adherence is deeply personal and multi-faceted, driven by clinical, social, and psychological factors that are difficult to untangle.

**Our Motivation:**  
This project explores how machine learning can look beyond surface-level clinical data to understand the human story behind non-adherence. The goal was to build a tool that predicts at-risk patients and provides actionable insights to help healthcare providers intervene effectively.

---

## 2. Project Objectives
- **Develop a Predictive Model:** Classify patients as 'Adherent' or 'Non-Adherent'.  
- **Achieve Realistic Performance:** Establish a reliable, real-world accuracy baseline.  
- **Identify Key Predictive Factors:** Uncover influential drivers of medication adherence.  
- **Generate Actionable Insights:** Translate findings into practical clinical strategies.

---

## 3. Methodology & Project Log

### Phase 1: Data Exploration and Cleaning
- Dataset: 500 anonymized anemia patients  
- Approach: Imputed missing numeric values with the median and categorical values with the mode to ensure a complete dataset for modeling.

### Phase 2: Baseline Modeling and the "69% Wall"
- Models: Random Forest and XGBoost  
- Observation: Both models plateaued at ~69% accuracy. Hyperparameter tuning did not improve results, indicating the limitation was in the raw features, not the algorithms.

### Phase 3: Feature Engineering Experiments

**Experiment A: General Features (False Start)**  
- Created features like `frailty_index` (age * comorbidities) and `financial_burden` score.  
- Result: Accuracy dropped to ~63–68%. Generic features added noise rather than signal.

**Experiment B: Targeted Features (Breakthrough)**  
- Identified key predictors: `health_literacy_score`, `provider_consistency`, `social_support_index`, `belief_in_medication`, `income_bracket`.  
- Created targeted features:  
  - `patient_readiness_score`: combines health literacy, social support, belief in medication, and provider consistency.  
  - `literacy_x_income`: interaction term capturing compounded risk of low literacy & low income.

### Phase 4: Final Model Selection
- Models re-run with targeted features.  
- Result: Both Random Forest and XGBoost improved; Random Forest selected for simplicity and interpretability.

---

## 4. Results and Observations

| Model Version         | Accuracy | Recall (Non-Adherent) | Key Takeaway                               |
|----------------------|----------|----------------------|-------------------------------------------|
| Baseline (Tuned RF)   | 69%      | 0.61                 | Solid, but hit a performance ceiling.     |
| General Features (RF) | 68%      | 0.54                 | Features added noise; performance dropped.|
| Targeted Features (RF)| 72%      | 0.61                 | Winner! Higher accuracy and balanced performance.|

**Final Model Classification Report (Random Forest with Targeted Features):**

          precision    recall  f1-score   support
       0       0.74      0.61      0.67        46
       1       0.71      0.81      0.76        54
accuracy                           0.72       100


---

## 5. Model in Action: Predictive Test Cases

| Name            | Prediction (1=Adherent) | Confidence (Adherent) | Confidence (Non-Adherent) |
|-----------------|------------------------|---------------------|--------------------------|
| Saanvi (High Risk)  | 0                      | 23.5%               | 76.5%                    |
| Rohan (Low Risk)    | 1                      | 77.6%               | 22.4%                    |
| Priya (Ambiguous)   | 1                      | 56.4%               | 43.6%                    |

**Analysis:**  
The model correctly identifies high- and low-risk patients. Ambiguous cases, like Priya, are flagged with low confidence, highlighting the need for additional monitoring.

---

## 6. Discussion
- Feature engineering was the key to improving performance.  
- Generic features added noise, while targeted, data-driven features amplified signal.  
- Lesson: Understanding the problem deeply and iteratively experimenting outperforms brute-force algorithm application.

---

## 7. Conclusion
- Developed a machine learning model predicting medication adherence with **72% accuracy**.  
- Insights highlight the human factors in adherence, including trust, understanding, and socioeconomic context.

**Recommendations for Future Work:**  
1. **Deployment:** Integrate model into clinical dashboards for real-time risk scoring.  
2. **Refinement:** Incorporate additional data like appointment attendance and pharmacy refill history.  
3. **Intervention Studies:** Use model predictions to design targeted support programs and measure real-world adherence impact.

---

## 8. Tools, Tech Stack, and Datasets
- **Technology:** Python  
- **Libraries:** Pandas, NumPy, Scikit-learn  
- **Dataset:** Synthetic but realistic dataset of 500 anonymized anemia patients  
  [Dataset Link](https://raw.githubusercontent.com/nandarishik/Ferry-Internship/main/realistic_medication_adherence_data.csv)
