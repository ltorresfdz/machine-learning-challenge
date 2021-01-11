# machine-learning-challenge
DATA ANALYTICS BOOT CAMP MONTERREY TECH Machine Learning Assignment

The purpose of this assignment is to create a machine learning model to analye the data base produced by the NASA Kepler space telescope and classify candidate exoplanets correctly. 
A detailed explanations of the data could be found in this link  [https://www.kaggle.com/nasa/kepler-exoplanet-search-results.]

**Features selected:** 
For a detailed explanation of each data, please refer to the selected parameters file.  All the error data columns from each feature were not selected. 
**Koi_disposition** and **Koi_Pdisposition**  were selected as the dependent variables, except on the SVM Model, where only Koi_disposition was selected as the dependent variable. (KOI =KEPLER OBJECT OF INTEREST) 

**Comparison of each model’s performance**
Linear regression and logistic regression model  does not apply to the dataset we are analyzing. 

  * _Multiple linear model_: First, with Pd get dummies I converted to categorical data the Y values, of koi_disposition and koi_pdisposition. 
  Training Score: 0.49985891257568993  
  Testing Score: 0.7790671330794682  
  When Quantifying this model:  
  MSE: 0.15896900289683424, R2: 0.7790671330794682  
  Grahp of residuals for this model:
  ![alt text](https://github.com/ltorresfdz/machine-learning-challenge/blob/main/Models/Residualplot.jpeg)  
  Working with other type of multiple linear models, there is no variation on MSE & R2.  
  LASSO model:  MSE: 0.14396945157108487, R2: 0.7845586956291211  
  Ridge model:  MSE: 0.15896709643255977, R2: 0.7790686306754261  
  ElasticNet model:  MSE: 0.14887715679336883, R2: 0.7833764098497668  
  
  RESULT: R2 should be close to 1, is this model is not that low, but not close to 1.  MSE should be close to ZERO. We need to continue looking for a better model.

  * _Decision tree and randmon forest_:  Working with same X & y structure: Pd get dummies converted to categorical data the Y values, of koi_disposition and koi_pdisposition, where possible values for Y are "CANDIDATE", "FALSE POSITIVE", "NOT DISPOSITIONED","CONFIRMED".  
  For decision tree we obtain a classifier score of  0.9982394366197183.  For random forest we obtain a Rf.score  0.9964788732394366.  
  With this model we can identify Features importances:  
  0.40490810727659166, 'koi_fpflag_nt'  
  0.13626959342783548, 'koi_fpflag_ss'  
  0.08946615045416538, 'koi_fpflag_co'  
  0.04166649645329832, 'koi_period'  
  0.03648210826652313, 'koi_duration'  
  0.030232924406832715, 'koi_prad'  
  0.028142279171006965, 'koi_depth'  
  0.025630983986380244, 'koi_insol'  
  0.023388945722059122, 'koi_srad'  
  0.020932313334681454, 'koi_slogg'  
  0.020785950819378497, 'koi_model_snr'  
  0.02026116218756867, 'koi_time0bk'  
  0.020221017909884002, 'koi_teq'  
  0.019378793911791058, 'koi_fpflag_ec'  
  0.018235582167039764, 'ra'  
  0.017031424493593388, 'koi_kepmag'  
  0.016046034162320397, 'koi_impact'  
  0.01557128511554301, 'koi_steff'  
  0.015348846733506753, 'dec'   
  
  RESULT: I identify those features with the higher importance for the result that are useful when doing adjustments in dataset slection of features for further model refinement.  Classifier score for randon forest is close to 1, seems to be a good model. Will continue looking for other models though.  
  
  * _KNN MODEL_:  Working with same X & y structure: Pd get dummies converted to categorical data the Y values, of koi_disposition and koi_pdisposition, where possible values for Y are "CANDIDATE", "FALSE POSITIVE", "NOT DISPOSITIONED","CONFIRMED".
After adjusting the dataset (Scalar or MinMaxScalar),the highest model accuracy was obtained at k=9 Test Acc: 0.989; with both type of adjustment when doing the data preprocessing:  
![alt text](https://github.com/ltorresfdz/machine-learning-challenge/blob/main/Models/testplot.png)![alt text](https://github.com/ltorresfdz/machine-learning-challenge/blob/main/Models/testplot2.png)

  * _SVM MODEL_:  When working with this model, the dataset was definied as y = koi_disposition only, and the koi_pdisposition was eliminated. Unfortunatelly the result was thas this model is overfitted due to the accuracy results obtained.  Test Acc: 0.998, Train Acc: 1.000.  
  Also, when doing the GridSearchCV model, it seems that on the train & test split of the data, there was only 1 class on the selected portion of the train/test, therefore the F1 score for the CONFIRMED class was 1, and 0 for the FALSE POSITIVE.  
  RESULT: need to review dataset again to redefined this model.

# Summary 
KNN model seems to be a good model to predict new exploplanets due to the score obtained.  Will need to work with dataset to improve model using SVM, selecting a dataset that has more classes or adding the error columns from the dataset. 
