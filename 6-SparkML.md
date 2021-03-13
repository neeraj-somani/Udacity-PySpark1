## Spark ML capabilities and limitations

Lesson Overview
- feature creation
- Model training
- Hyper parameter tuning
- capabilities and limitations
- Train model at scale

ML Lib guide -- https://spark.apache.org/docs/latest/ml-guide.html

Spark MLlib is very similar to SciKit-learn
It supports
- data cleaning
- feature engineering
- model training and prediction

It also supports
- Supervised learning
- Unsupervised learning
- feature computation
- hyperparameter tuning
- model evaluation

In spark, we also in parallelization, there are two types
- Data Parallelzation -- divide the data into sub-set, train the same model on these subsets, this is spark default behavious, 
    - the driver program run, act as a parameter server for most algorithms, where partial result of each iteration gets combined. and final model will be run on this combined result.
- Tasks Parallelization -- in this we run the model on individual task node and model result is analyzed individually and can be tuned accordingly.


## Some questions that can be asked with data?
- How many songs a user listen on our app per month?
- How many days since the user signup on app?

### There are various ways by which we need to normalize our data to make it more suitable to analysis, below are few techniques
You can find more information about the different scaler and indexer options through the links below.

### Scalers

Normalizer - https://spark.apache.org/docs/latest/ml-features.html#normalizer
StandardScaler - https://spark.apache.org/docs/latest/ml-features.html#standardscaler
MinMaxScaler - https://spark.apache.org/docs/latest/ml-features.html#minmaxscaler
MaxAbsScale - https://spark.apache.org/docs/latest/ml-features.html#maxabsscaler

### Indexers

StringIndexer - https://spark.apache.org/docs/latest/ml-features.html#stringindexer
IndexToString - https://spark.apache.org/docs/latest/ml-features.html#indextostring
VectorIndexer - https://spark.apache.org/docs/latest/ml-features.html#vectorindexer


### A stackoverflow dataset was used in the lesson
- https://stackoverflow.blog/2009/06/04/stack-overflow-creative-commons-data-dump/

## Dimensionality Reduction
- PCA


### ML Pipeline concepts
- Transformers  - an algo that transforms one df to another
    - Tokenization -- when we change text values to numerical values
    - train logistic regression model and predictions
    - 
- Estimators - mostly used to create df from untrained dataframe to trained dataframe

Let's continue exploring the parameter space for our question classification model.

As a first step break your data set into 90% of training data and set aside 10% to answer what's the accuracy of the best model you trained using unseen data.

On the first 90% of the data let's find the most accurate logistic regression model using 3-fold cross-validation with the following parameter grid:

CountVectorizer vocabulary size: [1000, 5000]
LogisticRegression regularization parameter: [0.0, 0.1]
LogisticRegression max Iteration number: [10]
Set the random seeds of all stages of the pipeline to 42.



To learn more about text processing you can read further in the documentation.


