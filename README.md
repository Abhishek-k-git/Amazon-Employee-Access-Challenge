![Banner](https://github.com/Abhishek-k-git/Amazon-Employee-Access-Challenge/blob/main/images/chatboost.png)

# Amazon Employee Access Challenge
#### Amazon employee access grant using catboost

![GitHub release (latest by date including pre-releases)](https://img.shields.io/github/v/release/navendu-pottekkat/awesome-readme?include_prereleases)
![GitHub last commit](https://img.shields.io/github/last-commit/navendu-pottekkat/awesome-readme)
![GitHub issues](https://img.shields.io/github/issues-raw/navendu-pottekkat/awesome-readme)
![GitHub pull requests](https://img.shields.io/github/issues-pr/navendu-pottekkat/awesome-readme)
![GitHub](https://img.shields.io/github/license/navendu-pottekkat/awesome-readme)

When an employee at any company starts work, they first need to obtain the computer access necessary to fulfill their role. This access may allow an employee to read/manipulate resources through various applications or web portals.

> Objective

The objective of this challenge is to build a model, learned using historical data, that will determine an employee's access needs, such that manual access transactions (grants and revokes) are minimized as the employee's attributes change over time. The model will take an employee's role information and a resource code and will return whether or not access should be granted.

> Data Set Information

Number of instances 1030
This is a sparse data set, less than 10% of the attributes are used for each sample. This file contains the access for users

| Column Name |	Description |
| -- | -- |
| ACTION |	ACTION is 1 if the resource was approved, 0 if the resource was not |
|RESOURCE |	An ID for each resource |
|MGR_ID |	The EMPLOYEE ID of the manager of the current EMPLOYEE ID record; an employee may have only one manager at a time |
|ROLE_ROLLUP_1 |	Company role grouping category id 1 (e.g. US Engineering) |
|ROLE_ROLLUP_2 |	Company role grouping category id 2 (e.g. US Retail) |
|ROLE_DEPTNAME |	Company role department description (e.g. Retail) |
|ROLE_TITLE |	Company role business title description (e.g. Senior Engineering Retail Manager) |
|ROLE_FAMILY_DESC |	Company role family extended description (e.g. Retail Manager, Software Engineering) |
|ROLE_FAMILY |	Company role family description (e.g. Retail Manager) |
|ROLE_CODE |	Company role code; this code is unique to each role (e.g. Manager) |

> Algorithm used

**CatBoost** is a high-performance open source library for gradient boosting on decision trees. It is developed by Yandex researchers and engineers, and is used for search, recommendation systems, personal assistant, self-driving cars, weather prediction and many other tasks at Yandex and in other companies, including CERN, Cloudflare, Careem taxi. It is in open-source and can be used by anyone.


> Model Building

```python
y = train_df['ACTION']
x = train_df.drop('ACTION', axis = 1)
x_test = test_df.drop('id', axis = 1)
```
```python
from sklearn.model_selection import train_test_split
x_train, x_valid, y_train, y_valid = train_test_split(x, y, test_size = 0.25, random_state = 1)
```
```python
#from catboost import CatBoostClassifier
%%time
params = {'loss_function': 'Logloss',
          'eval_metric':'AUC:hints=skip_train~false',
          'verbose': 200,
          'random_seed': 1}
catmodel_1 = CatBoostClassifier(**params)
catmodel_1.fit(x_train, y_train, eval_set = (x_valid, y_valid), use_best_model = True)
```
```
Learning rate set to 0.069882
0:	learn: 0.5389210	test: 0.5400959	best: 0.5400959 (0)	total: 191ms	remaining: 3m 10s
200:	learn: 0.8792570	test: 0.8016667	best: 0.8017826 (196)	total: 6.1s	remaining: 24.2s
400:	learn: 0.9225218	test: 0.8234442	best: 0.8234442 (400)	total: 12.1s	remaining: 18s
600:	learn: 0.9441294	test: 0.8323016	best: 0.8323806 (596)	total: 18s	remaining: 12s
800:	learn: 0.9599636	test: 0.8358281	best: 0.8361190 (795)	total: 24s	remaining: 5.95s
999:	learn: 0.9711849	test: 0.8391131	best: 0.8393621 (997)	total: 29.8s	remaining: 0us

bestTest = 0.8393620826
bestIteration = 997

Shrink model to first 998 iterations.
Wall time: 30.9 s
<catboost.core.CatBoostClassifier at 0x15799a34b20>
```
```python
categorical_features = list(range(x.shape[1]))
categorical_features
```
```python
%%time
params = {'loss_function': 'Logloss',
          'eval_metric':'AUC:hints=skip_train~false',
          'cat_features': categorical_features,
          'verbose': 200,
          'random_seed': 1}
catmodel_2 = CatBoostClassifier(**params)
catmodel_2.fit(x_train, y_train, eval_set = (x_valid, y_valid), use_best_model = True)
```
```
Learning rate set to 0.069882
0:	learn: 0.5616960	test: 0.5637606	best: 0.5637606 (0)	total: 119ms	remaining: 1m 58s
200:	learn: 0.8697068	test: 0.8955617	best: 0.8955872 (198)	total: 26.3s	remaining: 1m 44s
400:	learn: 0.8896195	test: 0.8973364	best: 0.8979162 (365)	total: 56.8s	remaining: 1m 24s
600:	learn: 0.9093650	test: 0.8972380	best: 0.8979162 (365)	total: 1m 27s	remaining: 58.4s
800:	learn: 0.9252708	test: 0.8958290	best: 0.8979581 (706)	total: 1m 54s	remaining: 28.5s
999:	learn: 0.9391837	test: 0.8933696	best: 0.8979581 (706)	total: 2m 22s	remaining: 0us

bestTest = 0.8979580831
bestIteration = 706

Shrink model to first 707 iterations.
Wall time: 2min 23s
<catboost.core.CatBoostClassifier at 0x15783eb98e0>
```
