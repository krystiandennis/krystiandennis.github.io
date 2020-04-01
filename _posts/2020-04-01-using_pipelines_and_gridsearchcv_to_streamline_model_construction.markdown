---
layout: post
title:      "Using Pipelines and GridSearchCV to streamline model construction"
date:       2020-04-01 15:54:18 -0400
permalink:  using_pipelines_and_gridsearchcv_to_streamline_model_construction
---

![](https://imgur.com/NKKCxvp.jpg)

For my 5th project for Flatiron School's Online Data Science Boot camp, I chose to build classification models that will predict whether or not a flight will be delayed During the Holiday Travel Season, which is considered December 21-January 2 every year.

I used a Kaggle dataset containing the 2018 on-time flight statistics for 2018 gathered from the Bureau of Transportation Statistics. The dataset is vast, with 7 million records. To make the dataset manageable, I selected only the top three US domestic airlines by revenue passenger-kilometers, which are Delta, United and American Airlines.
Once the dataset was cleaned and explored, I constructed a Pipeline with GridSearchCV for K Nearest Neighbors, Random Forest, XGBoost and Support Vector Machines.

I used make_pipeline(), instead of just Pipeline(), because I was able to add a scaler, GridSearchCV, param_grid, and refit the model with best parameters inside make_pipeline. Now they don't have to be done individually.

```
pipe_knn = make_pipeline(StandardScaler(), GridSearchCV(KNeighborsClassifier(), param_grid = {'n_neighbors':[5,10,20,40,50],
 'metric': ['manhattan', 'euclidean','minkowski'],
 'weights': ['uniform', 'distance']}, scoring='accuracy', cv=5, verbose = False, refit = True, return_train_score = True))
 
pipe_rf = make_pipeline(StandardScaler(), GridSearchCV(RandomForestClassifier(random_state=42), param_grid= {'n_estimators': [4,10,20,50],
 'criterion': ['gini', 'entropy'], 'max_depth': [None, 2, 5, 10, 15],'class_weight': ['balanced', None]},
 scoring= 'accuracy',cv=5, verbose = False, refit = True, return_train_score = True))
 
pipe_xgb = make_pipeline(StandardScaler(), GridSearchCV(xgb.XGBClassifier(), param_grid= {'colsample_bytree': [0.3, 0.7, 1],
 'n_estimators': [5,10,20,40,50],
 'max_depth': [3, 5, 10]}, scoring= 'accuracy', cv=5, verbose = False, refit = True, return_train_score = True))
 
pipe_svm = make_pipeline(StandardScaler(), GridSearchCV(svm.SVC(gamma = 'auto', random_state=42),
 param_grid = {'C': [0.1, 1,5, 10], 'kernel': ('linear','rbf')},
 scoring= 'accuracy', cv=5, verbose = False, refit = True, return_train_score = True))
```
 
Next, I created a list of pipelines and pipeline names.

```
pipelines = [pipe_knn,pipe_rf, pipe_xgb,pipe_svm]
pipeline_names = ['K Nearest Neighbors','Random Forest','XGBoost','Support Vector Machine']
```

Then, I created a for loop to fit each pipeline and run all models in one step.

```
for pipe in pipelines:
 print(pipe)
 pipe.fit(X_train, y_train)
```

I used the following function to determine which model in the pipeline had the best accuracy:

```
best_acc = 0.0
best_clf = 0
best_pipe = ''
for index, val in enumerate(pipelines):
 if val.score(X_test, y_test) > best_acc:
 best_acc = val.score(X_test, y_test)
 best_pipe = val
 best_clf = index
print('Classifier with best accuracy: %s' % pipeline_names[best_clf])
```

XGBoost was the most accurate model, with 93.7% accuracy.
