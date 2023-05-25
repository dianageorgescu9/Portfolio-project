# Portfolio-project
Portfolio project - Professional Certificate in Machine Learning &amp; Artificial Intelligence
**Non-technical explanation of your project**

This project aims to understand how a specific signalling pathway called interferon signalling is involved in rheumatoid arthritis (RA), which is a chronic inflammatory disease affecting the joints. We used artificial intelligence and machine learning techniques to analyse genetic data from RA patients and healthy individuals. By doing so, we identified the genes that are most relevant in predicting disease activity in RA and also explored which genes are related to the response to a commonly used therapy called methotrexate. This study provides valuable insights into the role of interferon signalling in RA and may help in improving treatment strategies for this disease.

**Data**

The data used in this study for analysis was obtained from RA-MAP that was created by RA-MAP Consortium. This contains a total number of 242 early RA patients that received only first-line treatment according to the UK-NHS standard of care, consisting of disease- modifying anti-rheumatic drugs (csDMARD) and 37 healthy vaccines. This was carried out using the whole blood, PBMCs, and CD8+, CD14+, and CD4+ leukocyte subsets collected when the patients first visited the clinic and after 6 months. The patients were followed up after 18 months and a wide range of clinical and omic data was collected. The disease Activity Score using only 28-joint counts (DAS28) and the Simplified Disease Activity Index (SDAI) were calculated at the beginning of the study, 3-, 6-, 9-, and 12- months. Transcriptomic data will be used in this study to explore the prediction of disease activity expressed as high or low as well as the genes making up IFN A and IFN B and use these to predict responders and non-responders following methotrexate

_Model_

The code is using the XGBoost (eXtreme Gradient Boosting) model for predicting disease activity based on transcriptomic data. XGBoost is a popular gradient boosting framework known for its high performance and ability to handle complex datasets.

The choice of XGBoost model might be due to its effectiveness in handling tabular data and its ability to capture nonlinear relationships between features and the target variable. Additionally, XGBoost provides feature importance rankings, which can be useful in identifying the genes that are driving the model's predictions.

The model is trained using the **xgb.train()** function, where various parameters are set, such as **max\_depth** (maximum depth of a tree), **eta** (learning rate), and **objective** (binary logistic regression in this case). The evaluation metric is set to "auc" (Area Under the ROC Curve), indicating the model's performance in classification tasks.

The XGBoost model is trained on the training data ( **X\_train** and **y\_train** ) and evaluated on the test data ( **X\_test** and **y\_test** ). The model's predictions are thresholded at 0.5 to determine the predicted disease activity level (high or low).

The model's performance is assessed using various metrics such as precision, recall, accuracy, and F1 score. The confusion matrix is visualized using Matplotlib to provide an overview of the model's classification results.

After training the model, SHAP (SHapley Additive exPlanations) values are calculated to explain the model's predictions. SHAP values provide insights into the contribution of each gene (feature) towards a particular prediction. The SHAP summary plot and force plots are generated to visualize the feature importances and the impact of individual genes on specific predictions.

The same modeling process is repeated for a second dataset related to interferon (IFN) and its association with disease activity. The IFN dataset is loaded, pre-processed, and used to train another XGBoost model. The model's performance and SHAP values are evaluated and visualized, similar to the first dataset.

Overall, XGBoost is chosen for its ability to handle tabular data, capture complex relationships, and provide interpretable feature importances through SHAP values

**Hyperparameter optimisation**

1. **max\_depth** : It defines the maximum depth of a tree. The default value is set to 3. The **max\_depth** hyperparameter controls the complexity of the trees in the ensemble. A higher value can lead to overfitting, while a lower value can result in underfitting. To optimize this hyperparameter I performed a grid search.
2. **eta** : It represents the learning rate, or the step size shrinkage used in each boosting iteration. The default value is 0.3. A lower learning rate can make the model converge slower but potentially yield better performance by allowing more fine-grained adjustments. I optimized this hyperparameter through techniques like grid search or cross-validation.
3. **objective** : This defines the loss function to be minimized during training. In the provided code, "binary:logistic" is used for binary logistic regression. There are other objectives available for different types of problems such as regression or multi-class classification.
4. **eval\_metric** : It specifies the evaluation metric to be used during training. In the code, "auc" (Area Under the ROC Curve) is used to evaluate the model's performance. I chose different evaluation metrics such as accuracy, precision, recall, or F1 score.
5. **num\_round** : It represents the number of boosting rounds (iterations) to perform. In the code, it is set to 10, which means the model will go through 10 iterations of boosting. The optimal number of rounds can be determined through techniques like early stopping, where the training is stopped if the evaluation metric on a validation set stops improving.

_Results_

ML methods enabled the identification of the top 20 genes that are highly relevant for predicting disease activity in RA. The strongest correlations revealed that elevated expression of MRPS9, TNRC15, FCER1A, and LOC727963 had a detrimental effect on the model's performance, while reduced expression of NKX3-1, C20orf127, LOC100130166, and LOC553137 were also associated with negative impact. Moreover, for predicting the response to methotrexate therapy, the top 20 interferon genes with the most significance were determined. Notably, lower expression levels of IFH1, UNC93B1, CXCL10, CEACAM1, and IFI44 were found to have an adverse effect on the model's performance. Conversely, the expression of TAP1 and SERPING1 genes demonstrated a notable positive correlation with the model's performance. On the other hand, increased expression of BST2, TAP1, SERPING1, and UBE2L6 genes was observed to have a negative impact on the model.

In summary, ML techniques facilitated the identification of key genes associated with disease activity in RA and response to methotrexate therapy. These findings provide valuable insights into the molecular mechanisms underlying the disease and can contribute to improved diagnostics and personalized treatment approaches.
