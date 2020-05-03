Project description:

Two datasets were selected from the internet at random and 5 supervised learning techniques of decision tree, SVM, Boosting, Artifical Neural Networks(ANN), k-Nearest Neighbors(kNN) were experimented on the datasets to identify how to select a machine learning algorithm according to the characteristics and nuances of a given dataset. Model complexity curves and learning curves were plotted for hyperparameter tuning and to identify underfitting/overfitting (bias/variance) problems. 

The following methodology and steps were used for both datasets in Weka 3.8 GUI:

Preprocessing data

1. In Weka GUI, load dataset in Preprocess -> Open File.
2. In Preprocess -> Edit, the correct attribute was set as the class uisng "Attribute as Class" option. 
3. Use Filter -> Unsupervised -> Instance -> RemoveDuplicates filter to remove the duplicated rows from the dataset.
4. Use Filter -> Unsupervised -> Instance -> Randomize filter to randomize the data using default seed value. 
5. Using Filter -> Unsupervised -> Instance -> Resample, with no replacement, 30% of dataset is sampled and stored as testing dataset. This filter produces a random subsample of a dataset using sampling without replacement. (Used 1 as seed for car evaluation dataset and 324 as seed for Letter Recognition dataset)
6. Setting the Invertselection parameter of Resample filter to true gives the remaining 70% of the dataset, which is stored as training dataset.

Finding best hyperparameters:

1. For each of the 2 datasets and each of the 5 algorithms, the preprocessed training dataset was loaded in the Preprocessor tab.
2. In order to find the best fitting hyperparameters for each algorithm, Weka -> classifiers -> Meta -> CVParameterSelection was used. 
3. In the CVParameterSelection dialog box, appropriate algorithm was chosen as the classifier and hyperparameter's ranges were inputted as java.lang.string. 
4. For some algorithms, gridsearch was conducted using Weka -> classifiers -> Meta -> GridSearch. It gave same output as CVParameterSelection.

Model complexity curve:

1. After obtaining the correct hyperparameters using CVParameterSelection or GridSearch, a range of values were selected for one or two hyperparameters per algorithm around their best-fit values.
2. For each algorithm and each dataset, the appropriate classifier is selected in the Classify tab. 
3. For each of the values in the range selected for the hyperparameters, the training set accuracy and cross-validation accuracy were recorded.
4. To obtain the accuracy(percent_correct) on the training set, the test option "Use Training set" was used.  In the classifier output summary, the percentage of correctly classified instances (Accuracy) will be shown.
5. To obtain the cross-validation accuracy, the test option "Cross-validation" was used.
6. The training set accuracy and cross-validation accuracy were plotted against hyperparameter values to get the model-complexity curve.

Learning curve:

1. The training set data was loaded in the Preprocess tab using Open File option.
2. Using weka -> filters -> supervised -> instance -> StratifiedRemoveFolds filter, 10% of the dataset was saved as the cross-validation set for the learning curve.
3. Selecting the InvertSelection option in StratifiedRemoveFolds filter, the remaining 90% was saved as the training set for the learning curve.
4. Using weka -> filters -> supervised -> instance -> resample filter with no replacement, subsets of the learning-curve training-set data were obtained. For example, 10% of the data was saved as subset1.arff, 20% as subset2.arff etc., till 100%. 
5. For each subset of the learning-curve training-set data, the training-set accuracy and cross-validation accuracy were obtained using the best-fitting hyperparameters for each dataset-algorithm pair (deduced from model-complexity curve).
6. The training set accuracy was recorded using the test option "Use training set" under the test options in the Classify tab.
7. The cross-validation accuracy was obtained using the "Supplied test set" test option and setting the test-set path to learning-curve cross-validation subset.
8. The training-set accuracy and cross-validation accuracy were plotted against the percentage of training set samples used,to get the learning curve.


The following libraries were used for each of the datasets. The best-fitting hyperpaarmeters for each algorithm-dataset pair was found using CVParameterSelection or GridSearch and listed in the report. 

Decision tree:
J48 classifier

ANN
Multilayer perceptron classifier.
NB: For ANN, a SMO classifier with Multilayer perceptron as underlying clasifier was used to do regularization with default parameters. 

KNN
IBk classifier
Note: LibSVM and GridSearch classifiers were installed using Weka GUI Chooser -> Tools -> Package Manager.

SVM
LibSVM classifier

Boosting
AdaBoostM1 with J48 as underlying classifier.

This project emphasizes on understanding how to select a machine learning algorithm for a task, rather than coding an algorithm. Hence the whole procedure was done in Weka GUI, and there is no handwritten-code. 

The preprocessed test and train sets for both the datasets are available at:
1. Letter Recognition train dataset
https://drive.google.com/open?id=12-5OBndOWQtC-S5vhccH7dwkkM6wCc2v 
2. Letter Recognition test dataset
https://drive.google.com/open?id=1a4sIC8NmXRfluNChdPtuxHRoqsTx1OIc 
3. Car Evaluation train dataset
https://drive.google.com/open?id=1EX-caX__N4wsvbUCdxi_b7APn7xD1dbb
4. Car Evaluation test dataset
https://drive.google.com/open?id=1_lqwj9zs4P5FaqqfVzYZuPdBJeaJfRJY