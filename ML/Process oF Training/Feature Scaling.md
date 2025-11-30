#MLprocess #leakage

 ## What is feature scaling?

It is basically the process of scaling all your features so that all the features take the values in the same scale

## why do we need to do it?

It is done to prevent one feature from dominating other ; which therefore would be neglected by the ML model.

## so do we do it before or after splitting the data into train test set ?
We do it after . It is for the simple reason that the test set is supposed to be a brand new set that you need to evaluate on your machine learning model. The test is not sth you are supposed to work on for the training. Feature scaling gets the mean and standard deviation of your feature in order to perform the scaling .
So if we apply it before splitting , it will get the mean and SD of all the values including the one in the test . And a test set is not sth you are supposed to have in the production.

It would cause sth like information leakage.