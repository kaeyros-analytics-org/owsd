# Model training and hyperparameter tuning

## Concept of train set, test set, validation set and cross validation

- The training set is the dataset that we employ to train our model. It is this dataset that our model uses to learn any underlying patterns or relationships that will enable making predictions later on.
- The test set is used to approximate the models's true performance in the reality. It is the final step in evaluating our model's performance on unseen data.
- The validation set uses a subset of the training data to provide an unbiased evaluation of a model. The validation data set contrasts with training and test sets in that it is an intermediate phase used for choosing the best model and optimizing it. It is in this phase that hyperparameter tuning occurs.
- Cross-validation is a statistical method used to estimate the performance (or accuracy) of machine learning models. In cross-validation, you make a fixed number of folds (or partitions) of the data, run the modelling process on each fold, and then average the overall error estimate.

## Model training

Model training is the process of teaching a machine learning algorithm to learn patterns and relationships in data by adjusting its parameters based on the provided training dataset.\
To train the model we will use the package **caret**.

## Hyperparameter tuning

