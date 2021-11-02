---
title: pandas
date: 2021-11-02 14:22:06
tags: phython
---

## 라이브러리 불러오기


```python
import pandas as pd
print(pd.__version__)
```

    1.1.5
    

### 테스트


```python
df = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4]})
print(type(df))
```

    <class 'pandas.core.frame.DataFrame'>
    

## 구글 드라이브 연동


```python
from google.colab import drive
drive.mount('/content/drive')
```

    Mounted at /content/drive

### * 주의사항 : 경로 중복되지않게!! *
