## Two models we can choose from 
- DNNclassifier (Deep Neural Network)
- LinearClassifier (Just probability of what it can become not pure numeric value)
---
# Build a DNN with 2 hidden layers with 30 and 10 hidden nodes

```
classifier = td.estimator.DNNClassifier(
feature_columns = my_feature_columns ,
#two hidden layers of 30 and 10 nodes respectively
hidden_units = [30, 20],

n_classes = 3
)
```