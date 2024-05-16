
```r
knitr::knit_child("11-modeling.Rmd")
#> 
#> 
#> processing file: ./11-modeling.Rmd
#>   |                                        |                                |   0%  |                                        |....                            |  12% [unnamed-chunk-4]  |                                        |........                        |  25%                    |                                        |............                    |  38% [unnamed-chunk-5]  |                                        |................                |  50%                    |                                        |....................            |  62% [unnamed-chunk-6]  |                                        |........................        |  75%                    |                                        |............................    |  88% [unnamed-chunk-7]  |                                        |................................| 100%                  
```

````
#> [1] "\n\n\n# Model training and hyperparameter tuning\n\n## Concept of train set, test set, validation set and cross validation\n\n- The training set is the dataset that we employ to train our model. It is this dataset that our model uses to learn any underlying patterns or relationships that will enable making predictions later on.\n- The test set is used to approximate the models's true performance in the reality. It is the final step in evaluating our model's performance on unseen data.\n- The validation set uses a subset of the training data to provide an unbiased evaluation of a model. The validation data set contrasts with training and test sets in that it is an intermediate phase used for choosing the best model and optimizing it. It is in this phase that hyperparameter tuning occurs.\n- Cross-validation is a statistical method used to estimate the performance (or accuracy) of machine learning models. In cross-validation, you make a fixed number of folds (or partitions) of the data, run the modelling process on each fold, and then average the overall error estimate.\n\n## Model training\n\nModel training is the process of teaching a machine learning algorithm to learn patterns and relationships in data by adjusting its parameters based on the provided training dataset.\\\nTo train the model we will use the package **caret**.\n\n\n```r\n#import libraries\nlibrary(tidymodels)\nlibrary(caTools)\nlibrary(caret)\n\n#load the data\n#breast_cancer <- read.csv(\"data/Breast_cancer_data.csv\")\n\n#transform the target variable to factor\nbreast_cancer$diagnosis <- as.factor(breast_cancer$diagnosis)\n\n# fixing the observations in training set and test set\nset.seed(123)\n# splitting the data set into ratio 0.80:0.20\nsplit <- caTools::sample.split(breast_cancer$diagnosis, SplitRatio = 0.80)\n\n# creating training dataset\ntrainingSet <- subset(breast_cancer, split == TRUE)\n\n# creating test data set\ntestSet <- subset(breast_cancer, split == FALSE)\n\n#train the KNN model\ndefault_knn_mod = train(\n  diagnosis ~ .,\n  data = trainingSet,\n  method = \"knn\",\n  trControl = trainControl(method = \"cv\", number = 5)\n)\n```\n\n\n## Hyperparameter tuning\nHyperparameter tuning is the process of selecting the optimal set of hyperparameters for a machine learning model.\n\n\n```r\n#tuning hyperparameters of the KNN model\ntune_knn_mod = train(\n  diagnosis ~ .,\n  data = trainingSet,\n  method = \"knn\",\n  trControl = trainControl(method = \"cv\", number = 5),\n  preProcess = c(\"center\", \"scale\"),\n  tuneGrid = expand.grid(k = seq(1, 101, by = 2))\n)\n```\n\n\n## Model evaluation\\\nModel evaluation is the process of assessing the performance and effectiveness of a machine learning model on unseen data. It involves various techniques and metrics to measure how well the model generalizes to new observations.\n\n\n```r\n#predictions on the test set for the first model\nmodel_pred <- predict(default_knn_mod, newdata = testSet)\n\n#confusion matrix for the fist model\ncm <- table(model_pred,testSet$diagnosis)\ncm\n#>           \n#> model_pred  0  1\n#>          0 26  1\n#>          1 16 70\n\n#predictions on the test set for the second model\nmodel_pred_tune <- predict(tune_knn_mod, newdata = testSet)\n\nconfusion_matrix <- table(model_pred_tune,testSet$diagnosis)\nconfusion_matrix\n#>                \n#> model_pred_tune  0  1\n#>               0 31  0\n#>               1 11 71\n\n#Calculate the accuracy\ncalc_acc <- function(data) {\n  data <- as.data.frame(data)\n  max_accuracy_index <- which.max(data$Accuracy)\n  row_with_max_accuracy <- data[max_accuracy_index, ]\n  return(row_with_max_accuracy$Accuracy)\n}\n\nprint(paste(\"The accuracy of the simple model is:\", calc_acc(default_knn_mod$results)))\n#> [1] \"The accuracy of the simple model is: 0.899044433827042\"\nprint(paste(\"The accuracy of the tuned model is:\", calc_acc(tune_knn_mod$results)))\n#> [1] \"The accuracy of the tuned model is: 0.936359292881032\"\n```\n\n"
````


# Model deployment

Model deployment in machine learning is the process of integrating your model into an existing production environment where it can take in an input and return an output. The objective is to enable others to access and utilize the predictive capabilities of your trained machine learning model.

## Model serialization
After achieving satisfactory performance with your model, it's essential to serialize and store it for future utilization. Serialization transforms the model into a binary format suitable for storage on disk.

```r
#save the model
saveRDS(tune_knn_mod,"./knn_model.rds")
```

**Use serialized model for predictions:**

```r
#load the model
knn_model <- readRDS("./knn_model.rds")

#use the model for predictions
predict(knn_model, testSet)
#>   [1] 1 0 0 0 0 1 0 0 0 0 0 1 1 1 0 1 1 1 0 1 1 1 1 1 0 1 1
#>  [28] 1 1 1 1 1 0 0 0 1 1 1 1 0 0 0 1 1 1 1 1 1 1 1 1 0 0 1
#>  [55] 0 1 1 0 1 1 1 1 1 1 1 0 1 1 1 1 1 1 1 1 1 1 0 1 1 1 1
#>  [82] 1 0 1 1 1 1 1 1 1 0 1 0 1 0 1 0 1 1 0 1 1 1 1 1 1 0 1
#> [109] 1 1 1 1 1
#> Levels: 0 1
```


## Model Deployment Criteria
Before you deploy a model, there are a couple of criteria that your machine learning model needs to achieve before it’s ready for deployment:

1. Portability: A portable model is one that can run efficiently on various hardware configurations and operating systems, with minimal adjustments required. 
2. Scalability: A scalable model is one that can handle increasing demands and data volumes without compromising performance. 

##  Model Deployment Methods
There exist three general methods for deploying your machine learning model:

1. One-off:\
Sometimes a model is only needed once or periodically. In this case, the model can simply be trained ad-hoc when it's needed and pushed to production until it deteriorates enough to require fixing.
2. Batch:\
Batch training involves updating a machine learning model using subsets of data at a time, ensuring scalability and up-to-date performance without requiring real-time predictions.
3. Real time:\
Model deployment in real-time refers to the process of integrating a trained machine learning model into a production environment where it can make predictions or classifications on new data instantaneously as it arrives. 

Once a model is deployed, it's common to monitor its performance and consider retraining it with updated training data. Monitoring and maintaining the deployment through continuous delivery ensures that your model provides accurate and reliable predictions in real-world scenarios.
