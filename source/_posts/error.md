---
title: error
date: 2021-11-16 11:44:58
tags: phython
---

# 에러

IndexError: index 0 is out of bounds for axis 0 with size 0

```python
#index 값출력 도중 에러발생
df_CQ7 = pd.DataFrame()
df_CQ7['Q7'] = [df_Ch[col][1:].value_counts().index[0] for col in df_Ch.columns[7:20]]
df_CQ7['counts'] = [df_Ch[col][1:].value_counts().values[0] for col in df_Ch.columns[7:20]]

print(df_CQ7)
```
![error](/img/error.PNG)

value값이 0인 칼럼을 제거 했더니 오류가 없어졌다.
```python
df21_Ch_rmQ7P12 = df21_Ch.drop(['Q7_Part_12'], axis='columns')
```
![error01](/img/error01.PNG)

정상출력