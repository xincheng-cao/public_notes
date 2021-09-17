# Confusion matrix
[link](https://machinelearningmastery.com/confusion-matrix-machine-learning/)
## About

A confusion matrix is a technique for summarizing the performance of a classification algorithm.

## Classification accurary and limitations

Classification accuracy is the ratio of correct predictions to total predictions made.

`classification accuracy = correct predictions / total predictions * 100`

Classification accuracy can also easily be turned into a misclassification rate or error rate by inverting the value, such as:

`error rate = (1 - (correct predictions / total predictions)) * 100`

problem:
- When your data has more than 2 classes. With 3 or more classes you may get a classification accuracy of 80%, but you don’t know if that is because all classes are being predicted equally well or whether one or two classes are being neglected by the model.
- When your data does not have an even number of classes. You may achieve accuracy of 90% or more, but this is not a good score if 90 records for every 100 belong to one class and you can achieve this score by always predicting the most common class value.

sum Classification accuracy can hide the detail you need to diagnose the performance of your model

## Definition

