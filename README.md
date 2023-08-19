# SVM-Anuran
SVM on 'Frogs_MFCCs' dataset  
Overall steps:  
1- First, we add the required libraries at the beginning of the work so that the reader can get an overview of the code content at the first glance.
2- The data are read by the read_csv tab from the pandas library.
3- Now the Family column is considered as the desired column as a data label and for data classification. (According to the type of existing data, it was also possible to work with multiple classes, which was not the question, and for this reason, the Genus and Species columns were removed from the data.)
4- The RecordTD column, which was neither used for the label nor as a feature, was removed from the data.

a)
1- With the help of the train_test_split function, we separate the training and test sections in the same proportion as requested and randomly.
2- From the scikit learn library and the svm module, we call the LinearSVC class and create a model from it. (We will see later that we will have to use the linear kernel from SVC to count the number of support vectors)
3- We fit the built model on the training data.
4- Finally, with the help of the score method, we check the validity of this model on the training and test data.

A) (Using a linear model that has the ability to count the number of support vectors)
1- Instead of selecting LinearSVC directly, we call SVC and consider its linear kernel.
2- Perform the same steps mentioned above for this model and finally, with the help of an attribute of this model called n_support_, the number of support vectors for each of the 4 different values of the Family column, which are the same 4 classes where the data is supposed to be the same From that we calculate the labels to eat.

b)
1- First, we divide the data into three parts: training, evaluation and testing.
2- Now, according to the demand of the problem of choosing non-linear SVM, we choose one of the SVM modes. (We chose Sigmoid here as a kernel of SVC)
3- We increase the cache size to improve the execution time.
4- We also do not touch the default value of C as the SoftSVM parameter at this stage and leave it as 1.
5- We perform the same steps of fit, prediction, accuracy and calculation of the number of support vectors with the same methods and functions as in the previous section.
6- Now we perform the request of the problem to change the parameter C in order to find the best model according to the changes in the accuracy of the model on the evaluation data.
For this purpose, we create empty lists to store the predicted label values on the evaluation data as well as the accuracy values of each model on this evaluation data.
Now, we choose the parameter C in a reasonable range (increasing or decreasing C too much as we examine different models according to the definition of this parameter has no effect on our goal) and a loop to apply it to the model and create models. We form with different C parameters. It is clear that every time inside the loop we complete the steps of fit and prediction and accuracy calculation and we add those values to the end of the created lists being filled in the loop.
7- In this step, with the help of argmax index, we find the highest accuracy and save and print the accuracy and C values in variables.
8- We draw the required curve in the case of a problem with the help of the range C that we have determined and also the list of stored truths.
9- Finally, we fit this best model on the training data and measure its accuracy on the training and test data. (On the evaluation data that we had obtained before and we had set the model from there)
10- At the end, we obtain the values of the support vectors for the new model and compare them with the previous model. According to the table obtained in the notebook, the result was that, except for the first class, which required a slightly larger number of support vectors in the linear mode, the rest of the classes needed about twice as many support vectors as the linear mode.
                 
1- We repeat exactly all the steps of the previous section for poly and rbf kernels. (First, like sigmoid, only these kernels are checked and then they are checked by changing the parameters of SoftSVM, the first one is equivalent to the "p" section and the second one is equivalent to the "t" section for these two kernels.

c)
1- With the help of the GridSearchCV class from the Model_Selection module from the ScikitLearn library, we can easily solve the problem by specifying parameters and cv parameters.
In parameters, we specify the type of kernel and the range of SoftSVM parameters, which is C, and in cv, we specify the number of folds, which is equal to 4 according to the question.
Finally, by specifying the estimator in question, which here is the rbf kernel from svm.SVC, we fully initialize GridSearchCV and this class returns us the best model.
2- We fit the training data on the model obtained in the previous issue.
3- Now we print the parameters of the model, which means the best C and kernel type, as soon as we know.
4- Finally, with the help of the model, we predict the label of the test data and measure the accuracy of the model on the training and test data, and we also calculate the number of support vectors for each of the 4 Family classes.
5- We do the same steps above (1-4) for the poly kernel.


At the end, we used a table with rows of Best_C (for the best SoftSVM parameter determined in the final model of each kernel), the number of support vectors and accuracy on different parts of the data (training, evaluation and testing) to check and compare the results of different models. ) we formed

Difference analysis of linear and non-linear SVMs:
Except for the non-linear sigmoid kernel, which we chose arbitrarily for part "b" in order to be different from the following parts, the rest of the non-linear kernels performed better than the linear kernel, which is based on moving the data to the upper spaces and their easier separation in those spaces is logical.
