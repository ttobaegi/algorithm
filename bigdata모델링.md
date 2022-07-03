## 모델링 & 하이퍼파라미터 튜닝 & 앙상블

```py
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(n_estimators=100, max_depth=5, random_state=2022)
model.fit(X, y['gender'])
print(model.score(X, y['gender']))
predictions = model.predict_proba(test)
predictions[:,1]
```
## csv생성
```py
output = pd.DataFrame({'cust_id': cust_id, 'gender': predictions[:,1]})
# 아웃풋 확인
output.head()
output.to_csv("123456789.csv", index=False)
```
- dataframe column 추출하기 : `pop()`
```py
cust_id = test.pop('cust_id')
```
- 데이터프레임만들기 : `pd.DataFrame({'컬럼':데이터})`
```py
output = pd.DataFrame({'cust_id': cust_id, 'gender': predictions[:,1]})
```
