HIV Protease Inhibitor Potency Prediction

Project Overview:
This project aims to develop a machine learning model to predict the potency of HIV-protease inhibitors. Using a dataset of known inhibitors and their bioactivity data, a regression model is trained to predict `pIC50` values based on molecular descriptors. The model's performance is then evaluated on a set of experimentally validated ligands to assess its predictive capabilities and consistency.

Methods:

1. Data Collection & Preprocessing
Training Data: A ChEMBL dataset containing 28 HIV-protease inhibitors with IC50 values was downloaded and preprocessed. The data was filtered to include only IC50 values in nanomolar units with a standard relation of =. pIC50 values were then calculated.

   Control ligands : 15 experimentally validated ligands (with known `Ki_nM` values) were used as a control set to compare predicted vs. experimental potency.

2. Feature Engineering
For ligand sets (training and real), RDKit molecular descriptors were calculated. These include:
-   MolWt: Molecular Weight
-   LogP: Octanol-water partition coefficient
-   TPSA: Topological Polar Surface Area
-   RotBonds: Number of Rotatable Bonds
-   HBD: Number of Hydrogen Bond Donors
-   HBA: Number of Hydrogen Bond Acceptors

3. Model Training
A Ridge Regression model was trained using the preprocessed ChEMBL dataset. The target variable for prediction was pIC50, and the RDKit descriptors served as features. A StandardScaler was applied to the features, and RidgeCV was used to find the optimal regularization parameter (`alpha`).

4. Prediction & Evaluation
-  The trained model was used to predict pIC50 values for the 15 ligands.
-  The predicted pIC50 values were compared against their experimentally derived pIC50 values (calculated from `Ki_nM`).
-   Model performance was assessed using R-squared, Mean Absolute Error (MAE), and Root Mean Squared Error (RMSE)

Results and Discussion:

Model Performance on control Ligands
-   R-squared (R²): 0.16
       This indicates that our model explains only 16% of the variability in the experimental `pIC50` values for the real ligands. This is a relatively low value, suggesting that while the model captures some aspects of potency, a large portion (84%) of the experimental variation is not explained by the current features or model. This is consistent with a visual inspection of the scatter plot, which showed a general trend but significant scatter around the ideal prediction line.

-   Mean Absolute Error (MAE): 0.89
       On average, the model's predictions are about 0.89 `pIC50` units away from the actual experimental `pIC50` values. This gives a direct sense of the typical magnitude of the errors.

-   Root Mean Squared Error (RMSE): 1.20
       The RMSE of 1.20 `pIC50` units, being higher than the MAE, suggests that there are likely some predictions with more significant deviations from the experimental values, pulling the average error up compared to MAE.

While the model showed a positive correlation, its predictive power for the real ligands is modest. It serves as a starting point, but there is substantial room for improvement in accurately predicting the `pIC50` values of experimentally validated compounds.

Future Work
Given the modest performance metrics, several areas can be explored to improve the model:
-   Expand Training Data: Utilize a larger and more diverse ChEMBL dataset.
-   Additional Features: Incorporate more advanced molecular descriptors (e.g., ECFP4 fingerprints, 3D descriptors).
-   Advanced Models: Experiment with other machine learning algorithms (e.g., Random Forest, Gradient Boosting, Neural Networks).
-   Ensemble Methods: Combine multiple models to improve robustness and accuracy.
-   Target-Specific Features: If structural information for the target protein is available, incorporate protein-ligand interaction fingerprints.
