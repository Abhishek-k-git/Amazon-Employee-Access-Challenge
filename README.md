> When an employee at any company starts work, they first need to obtain the computer access necessary to fulfill their role. This access may allow an employee to read/manipulate resources through various applications or web portals.

> Predicting compressive strength of concrete using various M.L classifications.
> Given are the variable name, variable type, the measurement unit and a brief description. The concrete compressive strength is the regression problem. The order of this listing corresponds to the order of numerals along the rows of the database.

![compressive strength of concrete](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQeR7DWGl6KmCEPycTAn6RhJeZIkf-x5blObw&usqp=CAU)

**Data Set Information:**

Number of instances 1030
This is a sparse data set, less than 10% of the attributes are used for each sample. This file contains the access for users

**Attribute Information:**
> The [PERSON_ID] column is the primary key column for the file. There is one row per user.

1. [PERSON_{ATTRIBUTE}]: This category describes the 'user' who was given access. 

|PERSON_ID | id of the user|
|--|--|
|PERSON_MGR_ID | id of the user's manager|
|--|--|
|PERSON_ROLLUP_1 | user grouping id|
|--|--|
|PERSON_ROLLUP_2 | user grouping id|
|--|--|
|PERSON_ROLLUP_3 | user grouping id|
|--|--|
|PERSON_DEPTNAME | department desciption id|
|--|--|
|PERSON_LOCATION | region id|
|--|--|
|PERSON_BUSINESS_TITLE | title id|
|--|--|
|PERSON_BUSINESS_TITLE_DETAIL | description id|
|--|--|
|PERSON_JOB_CODE | job code id|
|--|--|
|PERSON_COMPANY | company id|
|--|--|
|PERSON_JOB_FAMILY | job family id|
|--|--|

2. [RESOURCE_{ID}] This category of attributes are the resources that a users can possibly have access to. A user will have a 1 in this column if the have access to it otherwise it will be 0.

3. [GROUP_{ID}] - This category of attributes are the groups that a users can possibly have access to. A user will have a 1 in this column if the have access to it otherwise it will be 0.

4. [SYSTEM_SUPPORT_{ID}] - This category of attributes are the system that a user can possibly be supporting. A user will have a 1 in this column if the have can possibly be supporting it, otherwise it will be 0.


|Data Set Characteristics: | Time-Series, Domain-Theory | 
|--|--|
|Number of Instances: | 30000 |
|Area: | Business |
|Attribute Characteristics: | N/A|
|Number of Attributes: | 20000 |
|Date Donated | 2011-09-13 |
|Associated Tasks: | Regression, Clustering, Causal-Discovery|
|Missing Values? | No|
|Number of Web Hits: | 226095|
