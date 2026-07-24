
Machine Learning Results

Overview

This analysis investigates whether white matter tract profiles canpredict face memory performance in the Human Connectome Project (HCP).

The prediction target was the average accuracy across the 0-back and2-back face conditions of the Working Memory task.

A total of 1030 participants were included in the final analysis.

Input Features

AFQ provides measurements from 24 major white matter tracts for eachparticipant.

Each tract is characterized by four diffusion MRI metrics:

Fractional Anisotropy (FA)

Mean Diffusivity (MD)

Mean Kurtosis (MK)

Axonal Water Fraction (AWF)

Rather than combining all diffusion metrics into a single model, eachmetric was analyzed independently. Therefore, each model used 24 tractmeasurements from one diffusion metric as predictors.

For example, the FA model used 24 features such as ILF_L_FA, ILF_R_FA,ATR_L_FA, ATR_R_FA, and the remaining tract measurements. The sameprocedure was repeated for MD, MK, and AWF.

Machine Learning Pipeline

Each diffusion metric was evaluated using the same workflow:

Standardize tract features.

Train a Ridge Regression model using RidgeCV.

Evaluate prediction with Leave-One-Out Cross Validation (LOOCV).

Compute the Pearson correlation between predicted and observed faceaccuracy.

This produced four independent prediction models, one for each diffusionmetric.

Prediction Performance

Metric     Subjects   Features   Prediction r          p-value

FA             1030         24      0.146   2.5 × 10⁻⁶MD             1030         24      0.092        0.003MK             1030         24          0.029            0.359AWF            1030         24          0.000            0.991

FA produced the strongest prediction of face memory performance. MD alsoshowed statistically significant predictive ability, whereas MK and AWFdid not significantly predict behavioral performance.

Feature Weights

Ridge Regression coefficients were extracted after model training.

These coefficients describe the relative contribution of each tractwithin the multivariate prediction model. They should not be interpretedas independent tract--behavior correlations because all 24 tractfeatures were fitted simultaneously.

Output Files

The analysis generates:

ridge_loocv_metric_summary.csv

ridge_fa_loocv_predictions.csv

ridge_md_loocv_predictions.csv

ridge_mk_loocv_predictions.csv

ridge_awf_loocv_predictions.csv

tract weight tables for each diffusion metric

Summary

Using tract-level diffusion MRI measurements from 1030 HCP participants,Ridge Regression models were trained to predict face memory performance.

Among the four diffusion metrics, FA showed the strongest predictiveperformance, followed by MD. MK and AWF did not provide significantpredictive power in this dataset.
