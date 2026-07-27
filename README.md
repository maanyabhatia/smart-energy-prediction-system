# Smart Energy Prediction System

Component-wise machine learning system for building energy analytics: predicts energy consumption and classifies overall efficiency across HVAC, lighting, and IT systems in a corporate building.

## Problem

Building managers usually get either raw meter data or a single vague "efficiency score," neither of which says where energy is actually being wasted or what to do about it. This project builds component-level models (HVAC, lighting, IT) and rolls them up into one decision-ready metric a non-technical manager can act on.

## Method

Two supervised models work together: a Random Forest regression model predicts energy consumption per component from operating and environmental features, and a classification model labels overall system efficiency. Outputs are combined into a single Avoidable Energy Index (AEI) rather than leaving a manager to interpret several disconnected numbers. Robustness was checked with confusion-matrix and feature-importance analysis under noisy conditions.

## Results

The regression models produced reasonable consumption estimates per component. The efficiency classifier reached 1.0 (perfect) accuracy on the evaluation split.

Methodology note: a perfect score on real-world data is a warning sign, not a win, and I am flagging it rather than hiding it. The most likely explanation is feature leakage: the Avoidable Energy Index is engineered from the same underlying consumption data used to build the efficiency label, so the classifier may be finding a shortcut rather than learning a genuine efficiency signal. The fix is to audit the feature set, remove anything derived from the label, and re-evaluate before this number should be trusted.

## Limitations and next steps

Audit and fix the likely AEI leakage in the efficiency classifier described above. Validate on a separate building or time period rather than a random split of the same dataset, since energy data is often autocorrelated across time. Report per-component regression error (MAE, RMSE) alongside classification accuracy, not accuracy alone.

## Stack

Python, scikit-learn (Random Forest, ColumnTransformer, Pipeline), pandas, NumPy.

## Files

`Machine_Learning_driven_intelligence.ipynb` contains the full regression and classification pipeline, feature engineering, and evaluation. `Machine Learning-Driven Energy Intelligence for Corporate Buildings.pdf` is the accompanying written report.
