


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
