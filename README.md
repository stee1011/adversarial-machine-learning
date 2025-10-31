# 🧠 Model Robustness Under Structured Bias Injection  
### *A Gaussian + Chi-Square Mixture Experiment in Regression*

---

## Overview
This project investigates how machine learning regression models behave under **controlled bias injection**.  
By applying a **Gaussian–Chi² mixture distribution** to a single influential feature (`horsepower`) during inference, we observe how different models adapt or collapse under targeted data drift.  

The setup mirrors **real-world adversarial or distribution-shift attacks**, where small, structured perturbations can degrade an AI system’s reliability — especially in critical applications like **cybersecurity or malware analysis**.

---

## Objective
To evaluate and compare the **robustness of three regression algorithms** — Linear Regression, Random Forest, and Gradient Boosting — when one key feature undergoes statistical bias via a mixed Gaussian–Chi² distribution.

The purpose is not to improve accuracy, but to **understand fragility and resilience** under non-random data corruption.

---

## Methodology

1. **Data Preparation**
   - A clean automotive dataset is used with a mix of categorical and numerical predictors.
   - Preprocessing is handled via a `ColumnTransformer` and `Pipeline` setup with scaling, encoding, and dimensionality reduction.

2. **Model Training**
   - Each model is trained on unbiased data.
   - Evaluation metrics are recorded as a baseline.

3. **Bias Injection**
   - A composite distribution `Normal(μ=6, σ=0.1) + Chi²(k=6)` is applied **only to the `horsepower` feature** in the **test set**.
   - This ensures we simulate an **inference-time attack** — not data contamination.

4. **Re-Evaluation**
   - Post-bias predictions are generated.
   - Performance degradation is measured using **MAE**, **MSE**, and **R²** metrics.

---

## Results Summary

| Model                 | R² (Before Bias) | R² (After Bias) | ΔR² Change | Observations |
|------------------------|------------------|-----------------|-------------|---------------|
| **Linear Regression**  | 0.883            | 0.899           | +0.016      | Minimal impact, bias aligned partially with regression slope. |
| **Random Forest**      | 0.976            | 0.937           | −0.039      | Strong resilience; ensemble decorrelation dampened the noise. |
| **Gradient Boosting**  | 0.972            | 0.510           | −0.462      | Severe collapse due to compounded residual fitting. |

---

## Analytical Insights

- **Random Forests** remain stable under additive, feature-specific bias due to **bagging and randomness** that reduce dependency on any single corrupted feature.  
- **Linear Regression** performs better than expected — linear dependency sometimes neutralizes symmetric bias effects.  
- **Gradient Boosting** fails dramatically because its **sequential learners amplify systematic distortions** in the residuals, making it highly sensitive to structured noise.

---

## Theoretical Interpretation

1. **Gaussian + Chi² Mixture**
   - Represents a hybrid between symmetric (Gaussian) and asymmetric (Chi-square) noise.
   - Produces non-zero skewness and kurtosis, simulating *realistic sensor or logging distortions*.

2. **Residual Behavior**
   - After injection, the residual distribution becomes non-Gaussian.
   - Statistical checks (e.g., **Jarque-Bera test**, **Q–Q plot**) reveal **deviations from normality**, indicating bias-induced distortion.

3. **Implications in Security Systems**
   - In malware or anomaly detection, even subtle input bias can **shift decision boundaries**.
   - Models relying on high-variance sequential learning (like GBMs) become **attack vectors** via *data-level perturbations*, not traditional exploits.

---

## Key Takeaways

- **Noise ≠ harmless** — structured bias is a silent adversary.
- **Robustness testing** should be part of every model validation process, not just accuracy optimization.
- **Gradient Boosting models**, despite high baseline accuracy, can be brittle under adversarial drift.
- **Random Forests** and simpler models may act as **robust baselines** in adversarial or mission-critical environments.

---

## Research Relevance

This experiment aligns with topics in:
- **Adversarial Machine Learning**
- **Data Drift & Distribution Shift Detection**
- **AI Robustness in Cybersecurity**
- **Explainable Model Behavior Under Attack**

---

## Future Work

- Explore **drift-aware retraining** strategies.
- Quantify **feature sensitivity** using Shapley values before and after injection.
- Extend testing to **classification tasks** with simulated adversarial features.
- Develop a **robustness scoring index** that quantifies model stability under synthetic perturbations.

---

## Author

**Stephen Njoroge**  
*Data Science | Cybersecurity | AI Robustness Researcher*  
📫 [LinkedIn](https://www.linkedin.com/) | 💻 [GitHub](https://github.com/)

---

## Tags
`Machine Learning` • `Cybersecurity` • `Model Robustness` • `Adversarial ML` • `Gaussian Mixture` • `Chi-Square` • `Regression Analysis` • `Data Drift` • `Bias Injection`
