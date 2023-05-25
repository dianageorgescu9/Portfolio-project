Model Card

**Model description**

The first half of this notebook explores predicting disease activity (expressed as high or low) using transcriptomic data. Shap plots are used to describe which genes are driving the model. The second part of this notebook, drills down to the genes making up IFN A and IFN B and uses these to predict Responders and Non-Responders (response is based on Remission column in the file Clusters.txt

_Input:_

**First part:**

The input of the model consists of transcriptomic data, specifically gene expression levels. Here's a breakdown of the input components:

1. **data** : This variable represents the gene expression data, which is a pandas DataFrame. Each row in the DataFrame corresponds to a sample (e.g., a patient) and each column corresponds to a gene. The values in the DataFrame indicate the expression levels of the genes for each sample.
2. **X\_train** and **X\_test** : These variables represent the training and testing sets of the gene expression data, respectively. They are subsets of the **data** DataFrame and are used to train and evaluate the model.
3. **y\_train** and **y\_test** : These variables represent the target variable (disease activity) for the training and testing sets, respectively. They are pandas Series or arrays that contain the disease activity labels (e.g., high or low) corresponding to each sample in the training and testing sets.

**Second part:**

The input of the model consists of gene expression data for interferon genes. The gene expression data is represented as a pandas DataFrame called **IFNdata** , where each row corresponds to a sample and each column represents a gene. The shape of **IFNdata** is **(n\_samples, n\_genes)**, where **n\_samples** is the number of samples and **n\_genes** is the number of genes.

_Output:_

**First part:**

The output of the model is the predicted disease activity labels. Here's a breakdown of the output components:

**prediction** : This variable is a list or array that contains the predicted disease activity labels for the testing set. Each predicted label corresponds to a sample in the testing set.

The model uses the gene expression data as input and learns patterns and relationships between gene expression levels and disease activity. It then predicts the disease activity labels for the testing set based on the learned patterns. The output provides the predicted disease activity labels, which can be compared to the true labels ( **y\_test** ) for evaluation and analysis.

**Second part:**

The output of the model is a binary prediction indicating the response to treatment in rheumatoid arthritis. The model predicts whether a given sample is a responder or a non-responder. The predictions are based on the trained XGBoost model, and they are stored in the variable **predictionIFN**. The predictions are represented as a list or array of binary values, where 1 indicates a responder and 0 indicates a non-responder. The length of **predictionIFN** is equal to the number of samples in the test set.

Additionally, the code also computes and displays various evaluation metrics and visualizations related to the model's performance, such as a confusion matrix, precision, recall, accuracy, F1 score, SHAP values, and force plots. These outputs provide insights into the model's predictive accuracy and the importance of features (genes) in making the predictions.

_Model Architecture_

The model architecture is an XGBoost. The model also utilizes SHAP (SHapley Additive exPlanations) values to interpret the predictions. SHAP values provide an explanation for each feature (gene) in the dataset, indicating their contribution to the model's prediction. The SHAP values are calculated using the **shap. TreeExplainer** class, and various visualizations, such as the summary plot and force plots, are created to visualize the impact of features on individual predictions.

_Limitations_

The main limitation of the work carried out in this study is the size of the training dataset used, as it is likely that a larger dataset would have improved the performance of the ML- based model both in the case of predicting the disease activity and response to methotrexate therapy in RA. Furthermore, the use of additional explanatory variables might have enhanced the accuracy of predictions as well as the generalizability of the findings in a clinical setting that is not fully understood.

_Performance_

The performance of the model was assessed based on precision, recall, accuracy, and F1 score. The learning rate (eta) and max depth parameters were modified to optimize the model by introducing different values to see how they affect the performance of both parts of the notebook.

_Trade-offs_

A few trade-offs associated with the model:

1. Complexity vs. Interpretability: XGBoost models, including the one used in the code, are known for their high predictive accuracy. However, they can be complex and have a black-box nature, making it challenging to interpret and understand the underlying decision-making process. While SHAP plots provide some insights into feature importance, the overall interpretability of the model may still be limited.
2. Computational Resources: XGBoost models can be computationally expensive, especially when dealing with large datasets and a large number of features. Training the model and generating SHAP values can require substantial computational resources and time.
3. Feature Selection and Dimensionality: Dealing with transcriptomic data often involves a large number of genes, resulting in a high-dimensional feature space. While the model can handle high-dimensional data, it may lead to increased computational complexity, potential overfitting, and challenges in feature selection. It is important to carefully select relevant features or apply dimensionality reduction techniques to improve model performance and efficiency.
4. Data Requirements: The model relies on having sufficient and high-quality transcriptomic data, along with corresponding clinical information. Obtaining such data can be costly, time-consuming, and require expertise. Additionally, the model's performance heavily depends on the representativeness and generalizability of the training data.
5. Balancing Predictive Accuracy and False Positives/Negatives: The model aims to predict disease activity in rheumatoid arthritis based on transcriptomic data. While high predictive accuracy is desirable, it is important to consider the trade-off between correctly identifying disease activity (true positives) and potential false positives or false negatives. Depending on the specific application and context, different emphasis may be placed on sensitivity (recall) or specificity (precision) of the model.
6. Model Generalization: The model's performance and generalizability to new and unseen data should be carefully evaluated. It is essential to assess how well the model can predict disease activity in different populations, settings, or when applied to external datasets. Adequate external validation is crucial to understanding the model's robustness and reliability.
7. Practical Applicability: While the model may provide insights into the relationship between gene expression and disease activity, it is important to consider its practical applicability in real-world clinical settings. Factors such as cost-effectiveness, feasibility, and integration with existing diagnostic or treatment protocols need to be taken into account.

