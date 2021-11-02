---
title: pandas
date: 2021-11-02 14:22:06
tags: phython
---

##라이브러리 불러오기
- import pandas as pd
- print(pd.__version__)
- 1.1.5

## Test
- df = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4]})
- print(type(df))
   - (출력)
   - <class 'pandas.core.frame.DataFrame'>

## 구글 드라이브 연동
- from google.colab import drive
- drive.mount('/content/drive')

- DATA_PATH = '/content/drive/MyDrive/Colab Notebooks/11-01 phy/PART_I_Intro/data/'
- lemonade = pd.read_csv(DATA_PATH + 'Lemonade2016.csv')
- lemonade.info()
### * 주의사항 : 경로 중복되지않게!! *
