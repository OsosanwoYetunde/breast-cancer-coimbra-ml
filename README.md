BREAST CANCER DETECTION USING ADVANCED MACHINE LEARNING TECHNIQUES
A comparative evaluation and interpretation of five supervised machine learning classifiers for the detection of breast cancer, using anthropometric and serological biomarkers from the Breast Cancer Coimbra Dataset (BCCD).
This repository accompanies a Higher Diploma in Science in Data Analytics dissertation at Dublin Business School.
---
Project Overview
Breast cancer is the most frequently diagnosed cancer in women worldwide. In resource-constrained settings, conventional diagnostics such as mammography and biopsy are often inaccessible. This project investigates whether a low-cost, non-invasive model built on routine blood biomarkers can serve as an early screening adjunct.
The study does not develop novel algorithms. It applies, benchmarks, and interprets five established classifiers within a single reproducible pipeline, with emphasis on rigorous comparative evaluation and explainable feature interpretation.
---
Dataset
Property	Detail
Source	Breast Cancer Coimbra Dataset, UCI Machine Learning Repository (DOI: 10.24432/C52P59)
Origin	Centro Hospitalar e Universitário de Coimbra, Portugal
Observations	116 (64 patients, 52 healthy controls)
Features	9 predictors + 1 binary target
Missing values	None
Predictors: Age, BMI, Glucose, Insulin, HOMA, Leptin, Adiponectin, Resistin, MCP-1
Target: `Classification` (1 = healthy control, 2 = patient)
---
Objectives
Explore the state of the art in machine learning applications for breast cancer diagnosis and identify methodological gaps.
Implement and train five classifiers — Logistic Regression, Support Vector Machine (SVM), Decision Tree, Random Forest, and Multilayer Perceptron Artificial Neural Network (MLP-ANN) — within a reproducible scikit-learn pipeline.
Evaluate each classifier using accuracy, precision, recall (sensitivity), specificity, F1-score, the confusion matrix, and AUC-ROC, under 5-fold stratified cross-validation on an 80:20 train–test partition.
Interpret the best-performing model through feature-importance and SHAP analysis, assessing clinical plausibility against the biomedical literature.
---
Methodology
The pipeline follows a CRISP-DM workflow:
Data understanding — exploratory data analysis (distributions, skewness, correlations, class balance).
Data preparation — target re-encoding, median imputation, `StandardScaler`, stratified 80:20 split.
Modelling — five classifiers, each tuned via `GridSearchCV` within a unified `Pipeline` to prevent data leakage.
Evaluation — nested cross-validation (outer 5-fold for performance, inner 3-fold for tuning); seven-metric reporting; Wilcoxon signed-rank statistical comparison.
Interpretability — permutation importance + SHAP, triangulated against the biomedical literature.
All preprocessing is encapsulated inside the `Pipeline` object and refitted on each training fold, so no test-set information leaks into model fitting.
---
Repository Structure
```
breast-cancer-coimbra-ml/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── dataR2.csv                     # Breast Cancer Coimbra dataset
└── notebooks/
    └── breast_cancer_pipeline.ipynb   # End-to-end analysis pipeline
```
---
How to Run
```bash
# 1. Clone the repository
git clone https://github.com/YOUR-USERNAME/breast-cancer-coimbra-ml.git
cd breast-cancer-coimbra-ml

# 2. (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch the notebook
jupyter notebook notebooks/breast_cancer_pipeline.ipynb
```
Reproducibility is enforced with a fixed random seed (`random_state=42`) across all stochastic steps.
---
Key Results
The notebook trains, tunes, and evaluates all five classifiers and programmatically selects the best model by AUC-ROC. Indicative held-out test performance:
Classifier	Test AUC-ROC	Recall (Sensitivity)	Specificity
Random Forest	0.825	0.692	0.818
MLP-ANN	0.797	0.692	0.818
Logistic Regression	0.783	0.692	0.818

SVM (RBF)	0.755	0.692	0.818
Decision Tree	0.682	0.615	0.818
> Results are internal validation benchmarks on a 23-observation test fold. Given the small sample, figures should be read alongside the cross-validation estimates reported in the notebook.
---
Outputs Generated
Running the notebook produces:
Performance summary table across all five classifiers
Confusion matrices and ROC curves
Permutation importance ranking
SHAP summary plot (if `shap` is installed)
Clinical plausibility triangulation table
Serialised best-model file (`.pkl`)
---
Limitations
A small sample (n = 116) constrains statistical power and elevates performance variance.
Single-site Portuguese cohort limits generalisability to other populations.
Cross-sectional, single-time-point measurements preclude longitudinal modelling.
No external validation cohort; results are internal benchmarks.
---
Author
Ososanwo Yetunde Oluwabusolami
Higher Diploma in Science in Data Analytics
Dublin Business School
Student ID: 20066065
Supervisor: Dr Alexander Victor Okhuese
---
References
Patrício, M., Pereira, J., Crisóstomo, J., Matafome, P., Gomes, M., Seiça, R., & Caramelo, F. (2018). Using resistin, glucose, age and BMI to predict the presence of breast cancer. BMC Cancer, 18(1), 29. https://doi.org/10.1186/s12885-017-3877-1
UCI Machine Learning Repository. (2018). Breast Cancer Coimbra Dataset. https://doi.org/10.24432/C52P59
