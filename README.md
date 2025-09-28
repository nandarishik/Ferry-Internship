# The Adherence-AI Project: A Research Journal
**Lead Researcher:** Nanda  
**Project Start Date:** August 2025  
**Status:** Completed

---

## 1. Introduction & Background

**The Problem:**  
Medication non-adherence remains one of the silent, persistent challenges in modern healthcare. For patients managing chronic conditions like anemia, failing to follow a prescribed regimen can lead to severe health complications, hospital readmissions, and a diminished quality of life. The core challenge is that non-adherence is deeply personal and multi-faceted, driven by a complex web of clinical, social, and psychological factors that are difficult to untangle.

**Our Motivation:**  
This project was born from a simple but powerful idea: what if we could use machine learning to look beyond surface-level clinical data and understand the human story behind non-adherence? Our goal was to build a tool that could not only predict which patients were at risk but also provide actionable insights to help healthcare providers intervene effectively and compassionately. This journal documents our journey—our steps, our experiments, our stumbles, and our ultimate success.

---

## 2. Project Objectives

Our mission was guided by a clear set of goals:

- **Develop a Predictive Model:** Build a robust machine learning model to classify patients as 'Adherent' or 'Non-Adherent'.  
- **Achieve Realistic Performance:** Move beyond simplistic metrics to establish a reliable, real-world accuracy baseline.  
- **Identify Key Predictive Factors:** Uncover the most influential drivers of medication adherence within the dataset.  
- **Generate Actionable Insights:** Translate the model's findings into practical strategies implementable in a clinical setting.

---

## 3. Methodology & Steps Taken: The Project Log

This section details our end-to-end research process, documenting the experiments, observations, and decisions made along the way.

### Phase 1: Data Exploration and Cleaning

The project began with a dataset of 500 anonymized anemia patients. While rich in information, the dataset contained missing values across several columns. Our first step was foundational: create a clean, complete dataset. We implemented a standard imputation strategy: numeric values were filled with the median, and categorical values with the mode. This ensured that our subsequent models had a solid foundation to learn from.

---

### Phase 2: Baseline Modeling and the "69% Wall"

With clean data, we trained our first set of models—Random Forest and XGBoost—both recognized for strong performance in classification tasks. Both models performed admirably, but they quickly plateaued at an accuracy of ~69%.

**Observation:**  
Even after extensive hyperparameter tuning using GridSearchCV, neither model could break past this ceiling. This critical finding indicated that the limitation wasn't in the models’ ability to learn, but in the features themselves. The raw data contained signal, but not strong enough to surpass the barrier. To improve, we needed better, more insightful features.

---

### Phase 3: Feature Engineering Experiments

Feature engineering became the heart of the project, conducted in two distinct experiments.

#### Experiment A: General Feature Engineering (The False Start)

We first created logical, general features such as:

- `frailty_index = age * comorbidities`  
- `financial_burden score`  

**Hypothesis:** Composite features might provide a stronger predictive signal.  

**Result:** Accuracy dropped to ~63–68%.  

**Lesson Learned:** These features, while logical, were too generic and added noise. They did not capture the nuances of adherence behavior. This was a valuable lesson: not all good ideas on paper translate to improved model performance.

---

#### Experiment B: Targeted Feature Engineering (The Breakthrough)

Using the baseline model's feature importance, we identified top predictors:

- `health_literacy_score`  
- `provider_consistency`  
- `social_support_index`  
- `belief_in_medication`  
- `income_bracket`  

We hypothesized that **relationships between these features** mattered more than the features individually. This led to:

1. **`patient_readiness_score`** – a composite metric combining health literacy, social support, belief in medication, and provider consistency.  
2. **`literacy_x_income`** – an interaction term capturing compounded risk for patients with both low health literacy and low income.

These targeted features were highly domain-specific and directly aligned with our understanding of adherence behavior.

---

### Phase 4: Final Model Selection

With targeted features in place, we re-ran Random Forest and XGBoost. Results were immediate and conclusive: performance improved, validating our hypothesis. Random Forest was selected as the final model due to its simplicity, interpretability, and comparable performance to XGBoost.

---

## 4. Results and Observations

Targeted feature engineering was the key that unlocked the next performance tier.

| Model Version         | Accuracy | Recall (Non-Adherent) | Key Takeaway                               |
|----------------------|----------|----------------------|-------------------------------------------|
| Baseline (Tuned RF)   | 69%      | 0.61                 | Solid, but reached a performance ceiling. |
| General Features (RF) | 68%      | 0.54                 | Added noise; performance dropped.         |
| Targeted Features (RF)| 72%      | 0.61                 | Winner! Higher accuracy and balanced performance.|

**Final Model Classification Report (Random Forest with Targeted Features):**
          precision    recall  f1-score   support
       0       0.74      0.61      0.67        46
       1       0.71      0.81      0.76        54
accuracy                           0.72       100


---

## 5. Model in Action: Predictive Test Cases

| Name             | Prediction (1=Adherent) | Confidence (Adherent) | Confidence (Non-Adherent) |
|-----------------|------------------------|---------------------|--------------------------|
| Saanvi (High Risk) | 0                      | 23.5%               | 76.5%                    |
| Rohan (Low Risk)   | 1                      | 77.6%               | 22.4%                    |
| Priya (Ambiguous)  | 1                      | 56.4%               | 43.6%                    |

**Analysis:**  
- High-risk and low-risk cases were correctly identified with high confidence.  
- Ambiguous cases, like Priya, were predicted as 'Adherent' but with low confidence, highlighting patients who may need additional monitoring.

---

## 6. Discussion

- Feature engineering was the pivotal factor in breaking through the performance ceiling.  
- Generic features introduced noise; targeted, hypothesis-driven features amplified meaningful signal.  
- Key principle reinforced: a deep understanding of the problem and an iterative, experimental approach always outperforms brute-force algorithmic attempts.

---

## 7. Conclusion

- Developed a machine learning model predicting medication adherence with **72% accuracy**.  
- Findings confirm that medication adherence is a profoundly human issue, shaped by understanding, trust, and socioeconomic context.

**Recommendations for Future Work:**  
1. **Deployment:** Integrate model into clinical dashboards for real-time risk scoring.  
2. **Refinement:** Incorporate additional data like past appointment attendance or pharmacy refill history.  
3. **Intervention Studies:** Use predictions to design targeted educational and social support programs and measure real-world adherence impact.

---

## 8. Tools, Tech Stack, and Datasets

- **Technology:** Python  
- **Libraries:** Pandas, NumPy, Scikit-learn  
- **Dataset:** Synthetic but realistic dataset of 500 anonymized anemia patients  
  [Dataset Link](https://raw.githubusercontent.com/nandarishik/Ferry-Internship/main/realistic_medication_adherence_data.csv)


  <img width="943" height="511" alt="image" src="https://github.com/user-attachments/assets/c4fb1564-3f73-4a7a-abab-5b7805b9e881" />
  <img width="941" height="443" alt="image" src="https://github.com/user-attachments/assets/9056bb72-7d90-419b-b5ae-f2ab9e8b6e26" />
  <img width="934" height="536" alt="image" src="https://github.com/user-attachments/assets/fdc83df5-b4cf-45fd-80bd-5b10b64d97ab" />
  <img width="956" height="448" alt="image" src="https://github.com/user-attachments/assets/8ef422a4-54a0-4517-8eb5-87f5fbabbd7c" />




