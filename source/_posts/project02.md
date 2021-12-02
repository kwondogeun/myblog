---
title: project02
date: 2021-12-02 09:54:53
tags: R
---

## Classification with Tidymodels

## 개요
 - 새로운 ML 라이브러리인 ``` tidymodels```를 활용하여 분류 모델을 개발

## 데이터
 - URL: https://datahack.analyticsvidhya.com/contest/practice-problem-loan-prediction-iii/#ProblemStatement
 - Train file, Test file, Submission File

## 대회목적
 - 대출 승인 여부를 결정하는 모델을 만드는 것이 대회의 주 목적이며. 평가지표는 분류모형의 ```Accurarcy```로 결정한다.

## 패키지 및 데이터 볼러오기
 - 필수 패키지 불러오기
```python
# 데이터 수집
library(readr)

# 데이터 가공
library(dplyr) # 데이터 가공
library(tidyr) # 컬럼 변경
library(stringr) # 문자열 데이터 다루기 
library(forcats) # 범주형 데이터 다루기
library(skimr) # 데이터 요약
library(magrittr) # 파이프라인 작성


# 데이터 시각화
library(ggplot2) # 데이터 시각화 
library(corrr) # 상관관계 시각화
library(skimr) # 데이터 요약
library(patchwork) # 데이터 시각화 분할
library(GGally) # 산점도

# 데이터 모델링
library(tidymodels) # ML Packages 
library(themis) # class imbalance 처리
library(discrim) # 베이지안 모델링
library(tidyposterior) # 베이지안 모델링 성능 비교
library(doParallel) # CPU cores 확인
library(treesnip) # https://github.com/curso-r/treesnip 사이트에서 받아야함

train = read_csv("data/train_ctrUa4K.csv")
```
```python
train %<>% rename(Applicant_Income = ApplicantIncome,
                  CoApplicant_Income = CoapplicantIncome,
                  Loan_Amount = LoanAmount) 
# %<>% : 옵션바꾸고 바로적용 저장

loan_id = train$Loan_ID
train %<>% select(-Loan_ID) %>% mutate(Credit_History = as.character(Credit_History))
str(train)
```

![data](/img/data불러오기.PNG)
- 총 614개의 데이터  13개의 칼럼

## 탐색적 자료분석(EDA)
- 우선 ```skim()```함수 사용
```python
skim(train)
```
![skim](/img/skim.PNG)

## 데이터 시각화

## 단변량 시각화
- 각 개별적인 칼럼에 대해 시각화 자동으로 할 수 있는 코드 작성
```python
plot_by_column_type <- function(x, y) {
  # cat("y is:", y)
  viz_title <- str_replace_all(y, "_", " ") %>% 
    str_to_title()
  
  if ("factor" %in% class(x)) {
    ggplot(train, aes(x, fill = x)) + 
      geom_bar() + 
      theme(legend.position = "none", 
            axis.text.x = element_text(angle = 45, hjust = 1), 
            axis.text = element_text(size = 8)) + 
      scale_fill_viridis_d() + 
      theme_minimal() + 
      labs(title = viz_title, y = "", x = "")
  } else if ("numeric" %in% class(x)) {
    ggplot(train, aes(x)) + 
      geom_histogram() + 
      scale_fill_viridis_d() + 
      theme_minimal() + 
      labs(title = viz_title, y = "", x = "")
  } else if ("integer" %in% class(x)) {
    ggplot(train, aes(x)) + 
      geom_histogram() + 
      scale_fill_viridis_d() + 
      theme_minimal() + 
      labs(title = viz_title, y = "", x = "")
  } else if ("character" %in% class(x)) {
    ggplot(train, aes(x, fill = x)) + 
      geom_bar() + 
      theme(legend.position = "none", 
            axis.text.x = element_text(angle = 45, hjust = 1), 
            axis.text = element_text(size = 8)) + 
      scale_fill_viridis_d() + 
      theme_minimal() + 
      labs(title = viz_title, y = "", x = "")
  }
}

multiple_plots = map2(train, colnames(train), plot_by_column_type) %>% 
  wrap_plots(ncol = 3, nrow = 5)

multiple_plots
```
![단변량](/img/단변량.PNG)

 * 대출 지원자의 성별은 남성이 여성보다 많다.
 * 대출 지원자의 결혼 유무는 기혼자가 더 많다.
 * 대출 지원자 중 상당수는 자녀가 없다.
 * 대출 지원자 중 상당수는 대학을 졸업했고, self-employed가 아니다.
 * 대출 지원자의 수입은 right skewed이다.
 * co-applicant의 수입도 right skewed이다.
 * 대출 지원자 중 약 2/3은 대출을 승인받았다.

## 양적 변수 시각화
* 양적 변수 시각화를 하기 위해서는 산점도를 작성하는 것이 좋다.
* 관계성을 파악하기에도 매우 유용하다

```python
num_df <- train %>% 
  select(Loan_Status, where(is.numeric)) 

str(num_df)
```
```python
ggpairs(num_df, aes(color = train$Loan_Status, alpha = 0.3)) + 
  theme_minimal() + 
  scale_fill_viridis_d(aesthetics = c("color", "fill"), begin = 0.15, end = 0.85) + 
  labs(title = "Numeric Data Analysis")
```

![양적변수](/img/양적변수.PNG)

## 질적 변수 시각화
* 이번에는 질적 변수 시각화를 진행하도록 한다.
* 우선, 질적 변수 시각화를 진행하기에 앞서서 평균과 신뢰구간을 구하도록 한다.
* 평균을 구하려면 우선 숫자 데이터를 만들어야 하는데, Loan_Status 대출을 승인받았으면 1, 그렇지 않으면 0이라고 표시를 한다.

```python
qual_df <- train %>% 
  select(where(is.character)) %>% 
  drop_na() %>% 
  mutate(Loan_Status = if_else(Loan_Status == "Y", 1, 0)) %>% 
  pivot_longer(1:7, names_to = "Variables", values_to = "Values") %>% 
  group_by(Variables, Values) %>% 
  summarise(mean = mean(Loan_Status), 
            conf_val = 1.96 * sd(Loan_Status) / sqrt(n())) %>% 
  pivot_wider(names_from = Variables, values_from = Values)
```
```python
qual_df
```
```python
viz_plot <- function(data, column_name) {
  column <- sym(column_name)
  # cat("column:", enquo(column_name))
  data %>% select({{ column }}, mean, conf_val) %>% 
  drop_na() %>% 
  ggplot(aes(x= {{ column }}, y = mean, color = {{ column }})) +
  geom_point() +
  geom_errorbar(aes(ymin = mean - conf_val, ymax = mean + conf_val), width = 0.1) +
  theme_minimal() +
  theme(legend.position = "none",
        axis.title.x = element_blank(),
        axis.title.y = element_blank()) +
  scale_colour_viridis_d(aesthetics = c("color", "fill"), begin = 0.15, end = 0.85) +
  labs(title=column_name)
}

column_names = colnames(qual_df %>% select(-c(mean, conf_val)))
plots <- list()
for (i in seq_along(column_names)) {
  p1 <- viz_plot(qual_df, column_names[i])
  plots[[i]] <- p1
}

wrap_plots(plots) + plot_annotation(
  title = 'Proportion of Loan Data - Categorical Variables',
  subtitle = 'With 95% Confidence Intervals',
  caption = 'Data Source: Loan Prediction Problem by Analytics Vidhya'
)
```
![질적변수](/img/질적변수.PNG)

* Married 지원자가 대출을 승인 받을 가능성이 더 높다.
* 대졸자가 그렇지 않은 사람보다 대출을 승인 받을 가능성이 더 높다.
* 자녀들 변수는 큰 영향이 없는 것으로 보인다.
* 여성 신청자수는 변동성이 큰 반면, 남성들의 경우 상대적으로 변동성이 작아 보인다.
* Credit History의 유무에 따라 매우 큰 변동성이 있는 것으로 확인되었다.

## 데이터 분리
* 약 8:2로 데이터를 분리하도록 하는데, Loan_Status의 비율에 따라서 층화추출(Stratified Sampling) 방식을 취하도록 한다.
```python
set.seed(101)
loan_split <- initial_split(train, prop = 0.8, strata = Loan_Status)
```

## 모델 개발
* 분류 모형을 개발하도록 한다.
* 이때, logistic, decision tree, random forest, xgboost 총 4개의 모델을 개발하도록 한다.

```python
logistic_ml = logistic_reg(penalty = tune(), mixture = tune()) %>% 
  set_engine("glmnet") %>% 
  set_mode("classification")

dt_ml <- decision_tree(cost_complexity = tune(), 
                       tree_depth = tune(), 
                       min_n = tune()) %>% 
  set_engine("rpart") %>% 
  set_mode("classification")

rf_ml <- rand_forest(mtry = tune(), trees = tune(), min_n = tune()) %>% 
  set_engine("ranger") %>% 
  set_mode("classification")
  
xgboost_ml <- boost_tree(mtry = tune(), tree = tune(), min_n = tune(), tree_depth = tune(), learn_rate = tune(), loss_reduction = tune(), sample_size = tune()) %>% 
  set_engine("xgboost") %>% 
  set_mode("classification")
```

## Feature Engineering
* ```tidymodels```에서는 feature engineering을 수행하기 위해 recipe 함수를 적용한다.
* 결측치 처리를 위해 bagged tree models, impute_mean, impute_node 등을 사용했다.

```python
recipe_1 <- recipe(Loan_Status ~ ., data = training(loan_split)) %>% 
  step_mutate(Credit_History = if_else(Credit_History == 1, 1, -1, 0)) %>% 
  step_scale(all_numeric_predictors(), -Credit_History) %>% 
  step_impute_bag(Gender, 
                  Married, 
                  Dependents, 
                  Self_Employed, 
                  Loan_Amount, 
                  Loan_Amount_Term) %>% 
  step_dummy(all_nominal_predictors())

recipe_2 <- recipe(Loan_Status ~ ., data = training(loan_split)) %>% 
  step_mutate(Credit_History = if_else(Credit_History == 1, 1, -1, 0)) %>% 
  step_scale(all_numeric_predictors(), -Credit_History) %>%  
  step_impute_mean(all_numeric_predictors()) %>%
  step_impute_mode(all_nominal_predictors()) %>% 
  step_dummy(all_nominal_predictors()) %>% 
  step_zv(all_predictors())
```
* 모델 개발을 위해 recipe_1를 적용한 train, validation 데이터를 준비한다.
* 실제 테스트 데이터가 존재하기 때문에, 여기에서는 validation 이라고 명명했다.

```python
loan_train_df = recipe_1 %>% prep() %>% bake(new_data = NULL)
loan_validation_df = recipe_1 %>% prep() %>% bake(testing(loan_split))
```

## Correlation Graph
* 실제 변환된 데이터를 불러와서 상관관계 그래프를 작성하도록 한다.
* 먼저 train & validation 데이터를 합치도록 한다.

```python
loan_train_df %>% 
  bind_rows(loan_validation_df) %>% 
  mutate(Loan_Status = if_else(Loan_Status == "Y", 1, 0)) %>% 
  correlate() %>% 
  rearrange() -> static_correlations
```

```python
static_correlations
```

* 시각화 작성

```python
library(tidyquant)
```

```python
static_correlations %>%
    network_plot(min_cor = 0.05, colours = c("red", "white", "blue"), legend = TRUE) +
    labs(
        title = "Correlation Plot for Trained Loan Dataset",
        subtitle = "", 
        caption = "Image by McBert"
        ) +
    expand_limits(x = c(-0.1, 0.1), y = c(-0.4, 0.4)) +
    theme_tq() +
    theme(legend.position = "bottom", 
          axis.text = element_text(size = 10))
```

![모델개발](/img/모델개발.PNG)

* 위 그래프를 보면, ```Loan_Status```와 가장 연관성이 큰 데이터는 ```Credit_History```이다. 상식적으로 생각해도, 기존 대출 이력이 있는 사람에게 더 많은 대출을 하고자 하는 은행의 경향성을 생각하면 대략적으로 이해가 가는 결과임을 알 수 있다.

## Workflow sets
* Recipe List와 Model List

```python
recipe_list <- list(Recipe1 = recipe_1, Recipe2 = recipe_2)
model_list <- list(Random_Forest = rf_ml, Decision_Tree = dt_ml, Logistic_Regression = logistic_ml, XGBoost = xgboost_ml)
```

* workflow_sets()를 활용하여 최종적인 model_set를 완료한다.
* cross = T는 recipe의 각 조건과 머신러닝 알고리즘과 매칭되는 모든 가능한 조건들을 Combination 하도록 허락하는 설정으로 이해하면 된다.

```python
model_set = workflow_set(preproc = recipe_list, models = model_list, cross = T)
```

## 모델 학습
```python
set.seed(2)
train_resamples = bootstraps(training(loan_split), strata = Loan_Status)
detectCores()
```

```python
registerDoParallel(cores = 6)
all_workflows <- model_set %>% workflow_map(resamples = train_resamples, verbose = TRUE)
```

## 모델학습 비교
* 이제 모형 학습이 완료가 되었다면, 시각화로 어떤 모델이 좋은지를 확인해보도록 한다.
* 우선 학습된 데이터를 확인해보도록 한다.

```python
library(tune)
collect_metrics(all_workflows)
```

* 현재 결과물에서 accuracy에서 추출하고, 그 외 필요한 데이터 가공을 진행하도록 한다.

```python
collect_metrics(all_workflows) %>% 
  tidyr::separate(wflow_id, into = c("Recipe", "Model_Type"), sep = "_", remove = F, extra = "merge") %>% 
  filter(.metric == "accuracy") %>% 
  group_by(model) %>% 
  select(-.config) %>% 
  distinct() %>% 
  group_by(Recipe, Model_Type, .metric) %>% 
  summarise(mean = mean(mean), 
            std_err = mean(std_err), .groups = "drop") %>% 
  mutate(Workflow_Rank = row_number(-mean), 
         .metric = str_to_upper(.metric)) %>% 
  ggplot(aes(x = Workflow_Rank, y = mean, shape = Recipe, color = Model_Type)) + 
  geom_point(size = 2, alpha = 0.7) + 
  geom_errorbar(aes(ymin = mean-std_err, ymax = mean + std_err), position = position_dodge(0.9)) + 
  theme_minimal() + 
  labs(title = "Performance Comparison of Workflow Sets with Tidymodels", 
       subtitle = "Bootstrap Resamplings Procedure 25 Times", 
       caption = "Image Created By McBert", 
       x = "WorkFlow Rank by ML Model", 
       y = "Accuracy", 
       color = "Model Types", 
       shape = "Recipes")
```

![모델비교](/img/모델비교.PNG)
