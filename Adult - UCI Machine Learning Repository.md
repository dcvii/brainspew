---
title: "Adult - UCI Machine Learning Repository"
source: "https://archive.ics.uci.edu/dataset/2/adult"
author:
published:
created: 2026-06-26
description: "Discover datasets around the world!"
tags:
  - "brain_spew"
---
![](https://archive.ics.uci.edu/static/public/default/Large.jpg?10)

## Adult

## Donated on 4/30/1996

Predict whether annual income of an individual exceeds $50K/yr based on census data. Also known as "Census Income" dataset.

## Dataset Information

Additional Information

Extraction was done by Barry Becker from the 1994 Census database. A set of reasonably clean records was extracted using the following conditions: ((AAGE>16) && (AGI>100) && (AFNLWGT>1)&& (HRSWK>0)) Prediction task is to determine whether a person's income is over $50,000 a year.

Has Missing Values?

Yes

## Variables Table

| Variable Name | Role | Type | Demographic | Description | Units | Missing Values |
| --- | --- | --- | --- | --- | --- | --- |
| age | Feature | Integer | Age | N/A |  | no |
| workclass | Feature | Categorical | Income | Private, Self-emp-not-inc, Self-emp-inc, Federal-gov, Local-gov, State-gov, Without-pay, Never-worked. |  | yes |
| fnlwgt | Feature | Integer |  |  |  | no |
| education | Feature | Categorical | Education Level | Bachelors, Some-college, 11th, HS-grad, Prof-school, Assoc-acdm, Assoc-voc, 9th, 7th-8th, 12th, Masters, 1st-4th, 10th, Doctorate, 5th-6th, Preschool. |  | no |
| education-num | Feature | Integer | Education Level |  |  | no |
| marital-status | Feature | Categorical | Other | Married-civ-spouse, Divorced, Never-married, Separated, Widowed, Married-spouse-absent, Married-AF-spouse. |  | no |
| occupation | Feature | Categorical | Other | Tech-support, Craft-repair, Other-service, Sales, Exec-managerial, Prof-specialty, Handlers-cleaners, Machine-op-inspct, Adm-clerical, Farming-fishing, Transport-moving, Priv-house-serv, Protective-serv, Armed-Forces. |  | yes |
| relationship | Feature | Categorical | Other | Wife, Own-child, Husband, Not-in-family, Other-relative, Unmarried. |  | no |
| race | Feature | Categorical | Race | White, Asian-Pac-Islander, Amer-Indian-Eskimo, Other, Black. |  | no |
| sex | Feature | Binary | Sex | Female, Male. |  | no |

0 to 10 of 15

## Additional Variable Information

Listing of attributes: >50K, <=50K. age: continuous. workclass: Private, Self-emp-not-inc, Self-emp-inc, Federal-gov, Local-gov, State-gov, Without-pay, Never-worked. fnlwgt: continuous. education: Bachelors, Some-college, 11th, HS-grad, Prof-school, Assoc-acdm, Assoc-voc, 9th, 7th-8th, 12th, Masters, 1st-4th, 10th, Doctorate, 5th-6th, Preschool. education-num: continuous. marital-status: Married-civ-spouse, Divorced, Never-married, Separated, Widowed, Married-spouse-absent, Married-AF-spouse. occupation: Tech-support, Craft-repair, Other-service, Sales, Exec-managerial, Prof-specialty, Handlers-cleaners, Machine-op-inspct, Adm-clerical, Farming-fishing, Transport-moving, Priv-house-serv, Protective-serv, Armed-Forces. relationship: Wife, Own-child, Husband, Not-in-family, Other-relative, Unmarried. race: White, Asian-Pac-Islander, Amer-Indian-Eskimo, Other, Black. sex: Female, Male. capital-gain: continuous. capital-loss: continuous. hours-per-week: continuous. native-country: United-States, Cambodia, England, Puerto-Rico, Canada, Germany, Outlying-US(Guam-USVI-etc), India, Japan, Greece, South, China, Cuba, Iran, Honduras, Philippines, Italy, Poland, Jamaica, Vietnam, Mexico, Portugal, Ireland, France, Dominican-Republic, Laos, Ecuador, Taiwan, Haiti, Columbia, Hungary, Guatemala, Nicaragua, Scotland, Thailand, Yugoslavia, El-Salvador, Trinadad&Tobago, Peru, Hong, Holand-Netherlands.

## Baseline Model Performance

## Dataset Files

| File | Size |
| --- | --- |
| adult.data | 3.8 MB |
| adult.test | 1.9 MB |
| adult.names | 5.1 KB |
| old.adult.names | 4.2 KB |
| Index | 140 Bytes |

## Papers Citing this Dataset

[Integrating Association Rules with Decision Trees in Object-Relational Databases](https://api.semanticscholar.org/CorpusID:127985102)

By Maruthi Ayyagari. 2019

Published in International Journal of Engineering Trends and Technology 67.3 (2019): 102-108.

[Outis: Crypto-Assisted Differential Privacy on Untrusted Servers](https://api.semanticscholar.org/CorpusID:67789712)

By Amrita Chowdhury, Chenghong Wang, Xi He, Ashwin Machanavajjhala, Somesh Jha. 2019

Published in ArXiv.

[Refining the Structure of Neural Networks Using Matrix Conditioning](https://api.semanticscholar.org/CorpusID:199472855)

By Roozbeh Yousefzadeh, Dianne O'Leary. 2019

Published in ArXiv.

[Fair k-Center Clustering for Data Summarization](https://api.semanticscholar.org/CorpusID:59291919)

By Matthaus Kleindessner, Pranjal Awasthi, Jamie Morgenstern. 2019

Published in ArXiv.

[Effectiveness of Equalized Odds for Fair Classification under Imperfect Group Information](https://api.semanticscholar.org/CorpusID:182952909)

By Pranjal Awasthi, Matthaus Kleindessner, Jamie Morgenstern. 2019

Published in ArXiv.

0 to 5 of 257

```
pip install ucimlrepo
```

Import the dataset into your code
```
from ucimlrepo import fetch_ucirepo 
  
# fetch dataset 
adult = fetch_ucirepo(id=2) 
  
# data (as pandas dataframes) 
X = adult.data.features 
y = adult.data.targets 
  
# metadata 
print(adult.metadata) 
  
# variable information 
print(adult.variables)
```

257 citations

666440 views

```
Becker, B. & Kohavi, R. (1996). Adult [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5XW20.
```

## Keywords

[census](https://archive.ics.uci.edu/datasets?search=&Keywords=census)

## Creators

Barry Becker

Silicon Graphics

Ronny Kohavi

ronnyk@live.com

Consultant/Stanford

## DOI

[10.24432/C5XW20](https://doi.org/10.24432/C5XW20)

## License

This dataset is licensed under a [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/legalcode) (CC BY 4.0) license.

This allows for the sharing and adaptation of the datasets for any purpose, provided that the appropriate credit is given.