---
title: plotly04
date: 2021-11-09 10:53:11
tags:
---
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import plotly.express as px
import plotly.graph_objects as go
from warnings import filterwarnings
filterwarnings('ignore')

colors = ['#B1EDED','#B1B2ED','#1DE7ED','#1DA5ED','#1D50ED','#16548E']

df = pd.read_csv('../input/kaggle/kaggle_survey_2021_responses.csv')
df.head()
```

```python
# df_env를 dataframe 변수형식 객체로 지정
df_env = pd.DataFrame()
print(df_env)


# value_counts 함수
# (https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.value_counts.html?highlight=value_counts#pandas.DataFrame.value_counts)

## df_env객체에 dev_env 칼럼을 삽입하고 df 객체의 21~34 칼럼에 해당하는 index를 뽑아서 0에 위치한 값을 저장
df_env['dev_env'] = [df[col][1:].value_counts().index[0] for col in df.columns[21:34]]
print(df_env)

## df_env객체에 counts 칼럼을 삽입하고 df 객체의 21~34 칼럼에 해당하는 value를 뽑아서 0에 위치한 값을 저장
df_env['counts'] = [df[col][1:].value_counts().values[0] for col in df.columns[21:34]]
print(df_env)




# sort_values 함수
# https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html#pandas.DataFrame.sort_values

## df_env 객체에 정렬 기준점을 'counts' colums로 잡고 오름차순(ascending)으로 정렬할지를 설정한다. inplace = True인 경우 해당 정렬을 객체에서 수행한다.
df_env.sort_values(by='counts', ascending=False, inplace=True)
print(df_env)




# plotly.express.treemap  # high-level interface
# H: https://plotly.com/python-api-reference/generated/plotly.express.treemap.html
# L: https://plotly.com/python-api-reference/generated/plotly.graph_objects.Treemap.html#id1

## treemap figure로 시각화
fig = px.treemap(df_env, path=[px.Constant("all"),'dev_env'], 
                 values='counts', color='counts', color_continuous_scale=colors)
# treemap(DF형식 객체, path(경로)=[# path 해석: all 이라는 상수를 만들어 dev_env 칼럼 전체를 삽입했다],
#         values(정렬기준)='객체', color='비율을 color로 표현(우측에 counts에 관한 기준 표현)')
#         color_continuous_scale='CSS 형식의 색상을 정의해서 원하는 연속적인 색상으로 표현'



# figure 

# figure 경로 업데이트
fig.update_traces(root_color="red")
# root 오퍼레이터의 color 변경
# [root] https://plotly.com/python-api-reference/generated/plotly.graph_objects.icicle.html#plotly.graph_objects.icicle.Root
# but, color 표현의 방식이 counts의 비율로 설정되었기 때문에 적용되지 않는다.(by: color='counts')


# figure 구조를 업데이트하고 타이틀 지정
fig.update_layout(title='Development environment used by kagglers')
fig.show()
```
![ad](/img/ad.PNG)
![add](/img/add.PNG)

