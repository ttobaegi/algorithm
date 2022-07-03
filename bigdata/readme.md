## 1. 기본 라이브러리
```py
import pandas as pd
import numpy as np
```
- 경로 설정 
```py
import os
```
## 2. 전처리
```
from sklearn.preprocessing import MinMaxScaler, StandardScaler
```
## 3. 통계처리
```py
# 상관계수
from scipy.stats import pearsonr, spearmanr, kendalltau

# chi-squared test
from scipy.stats import chi2_contingency

# t-test
from scipy.stats import ttest_1samp, ttest_rel, ttest_ind

# varuance
from scipy.stats import bartlett, levene, f_oneway

# ANOVA
from scipy.stats import f_oneway
from statsmodels.formula.api import ols
from statsmodels.stats.anova import anova_lm
from statsmodels.stats.multicomp import pairwise_tukeyhsd
```

## 4. 머신러닝
### 4-1. 데이터 분류
```py
from sklearn.model_selection import train_test_split
```
### 4-2. 모델링
```py
from sklearn.neighbors import KNeighborsClassifier # k-NN
from sklearn.neighbors import KNeighborsRegressor # k-NN

from sklearn.cluster import AgglomerativeClustering # 계층적 군집분석
from sklearn.cluster import KMeans # K-means

from statsmodels.formula.api import ols # 선형회귀
from sklearn.linear_model import LinearRegression # 선형회귀
from statsmodels.api import Logit # 로지스틱 회귀
from sklearn.linear_model import LogisticRegression # 로지스틱 회귀

from sklearn.tree import DecisionTreeClassifier # Decicion Tree
from sklearn.tree import DecisionTreeRegressor

from sklearn.naive_bayes import GaussianNB
```
### 4-3. 평가
```
# 수치
from sklearn.metrics import mean_absolute_error # MAE
from sklearn.metrics import mean_squared_error # MSE

# 분류
from sklearn.metrics import roc_auc_score # AUC
from sklearn.metrics import accuracy_score
from sklearn.metrics import precision_score
from sklearn.metrics import recall_score
from sklearn.metrics import f1_score
```
