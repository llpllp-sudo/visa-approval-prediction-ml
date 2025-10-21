# Visa Approval Prediction — EasyVisa ML Project

## 🏢 **Business Context**

U.S. companies face increasing demand for skilled workers but often struggle to identify and sponsor the right foreign talent.
The **Office of Foreign Labor Certification (OFLC)** reviews hundreds of thousands of visa applications yearly, ensuring compliance with fair wage and labor laws.
Due to growing application volumes, OFLC partnered with **EasyVisa** to develop a **Machine Learning model** to assist in identifying visa applications with a higher probability of approval.

---

## 🎯 **Objective**

Build a classification model that predicts whether a visa application will be **Certified (1)** or **Denied (0)**.
The goal is to:

* Streamline the review process.
* Identify key factors influencing visa approval.
* Recommend applicants and employers most likely to be certified.

---

## 📊 **Data Description**

Each record represents a visa application, containing:

* **Employee attributes:** continent, education, job experience, training requirement.
* **Employer attributes:** number of employees, establishment year, region of employment.
* **Job details:** prevailing wage, wage unit, full-time status.
* **Target:** `case_status` (Certified / Denied).

---

## ⚙️ **Model Development**

### **Baseline Models**

| Model                   | Train F1 | Validation F1 | Key Notes          |
| ----------------------- | -------- | ------------- | ------------------ |
| Decision Tree           | 0.74     | 0.75          | Overfits easily    |
| Random Forest           | 0.80     | 0.81          | Strong baseline    |
| AdaBoost                | 0.82     | 0.82          | High recall        |
| Gradient Boosting (GBM) | **0.83** | **0.83**      | Best performing    |
| XGBoost                 | 0.81     | 0.81          | Stable performance |

**Evaluation Metric:**
📈 **F1 Score** – chosen to balance **Precision** and **Recall**, since both false approvals and false denials are costly.

---

### **Resampling Strategies**

* **Oversampling:** Improved model balance, with **XGBoost** and **GBM** performing best (Val F1 ≈ 0.82).
* **Undersampling:** Increased overfitting and lower F1; not preferred.

---

### **Hyperparameter Tuning**

**Models tuned using RandomizedSearchCV:**

* **GBM:** Tuned `n_estimators`, `learning_rate`, `max_depth`, etc.
* **AdaBoost:** Tuned base estimator depth and learning rate.
* **Random Forest:** Tuned `n_estimators`, `max_samples`, and `max_features`.

**Best Final Model:**
✅ **Gradient Boosting (GBM)** — strong F1 and Recall with minimal overfitting.

---

## 💡 **Key Insights**

1. **Prevailing Wage** – Most critical predictor; higher wages correlate strongly with approvals.
2. **Education Level** – Higher education (Master’s/Doctorate) increases chances of certification.
3. **Employer Strength** – Larger and more established companies have higher approval rates.
4. **Experience & Full-Time Jobs** – Applicants with prior experience and full-time positions are favored.
5. **Geographic Influence** – Employment in **Midwest/West** regions and **Europe-based applicants** have slightly better outcomes.
6. **Wage Unit** – Applications quoting **annual wages** perform better than those listing hourly/weekly rates.

---

## 🧭 **Business Recommendations**

* **Prioritize candidates** with higher wages and education levels.
* **Encourage employers** with larger, older firms to apply — their history boosts credibility.
* **Promote full-time roles** and experienced candidates for higher success.
* **Standardize wage reporting** to yearly terms for better clarity.
* **Target campaigns** toward regions and profiles historically showing higher certification rates.

---

## 🧠 **Technologies Used**

* Python (Pandas, NumPy, Scikit-learn, XGBoost)
* Data visualization (Matplotlib, Seaborn)
* Model tuning (RandomizedSearchCV)
* Class balancing (SMOTE / Oversampling)

---

## 🏁 **Result**

* Achieved **Validation F1 = 0.83** with GBM
* Balanced recall and precision → improved generalization
* Enabled OFLC to **prioritize high-likelihood approvals**, saving time and resources in the visa screening process.
