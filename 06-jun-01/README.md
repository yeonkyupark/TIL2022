# 2022년 06월

## TIL20220601

### 데이터 분석 절차

1.  데이터 수집

2.  데이터 정제

3.  데이터 가공

4.  데이터 분할

5.  모델 학습

6.  예측 및 평가

7.  성능개선

8.  결과 활용

#### 데이터 수집

[UCL](http://archive.ics.uci.edu/ml/index.php)에서 데이터셋 불러 오기

-   wine dataset - <http://archive.ics.uci.edu/ml/machine-learning-databases/wine/wine.data>

```{r}
wine.fl <- "http://archive.ics.uci.edu/ml/machine-learning-databases/wine/wine.data"
wine <- read.csv(wine.fl,header = F)
wine.names <- c("Alcohol", "Malic acid", "Ash", "Alcalinity of ash", "Magnesium",
"Total phenols", "Flavanoids", "Nonflavanoid phenols", "Proanthocyanins",
"Color intensity", "Hue", "OD280/OD315 of diluted wines", "Proline")
colnames(wine)[2:14] <- wine.names
colnames(wine)[1] <- "Class"
str(wine)
```

#### 데이터 정제

##### 결측치 처리

```{r}
# 결측치 확인
wine_na <- colSums(is.na(wine))
as.matrix(wine_na)
```

```{r}
if(!require(naniar)) { install.packages("naniar"); library(naniar); }
n_miss(wine)
miss_case_summary(wine)
vis_miss(wine)
```

```{r}
table(wine$Class, useNA="ifany")
```


결측치 처리 방법

:   1.  결측치 제거
    2.  단순대체
    3.  다중대체

```{r}
x <- c(1,2,3,4,NA,6,7,8,NA,10)
summary(x)
```

```{r}
# 1. 결측치 제거
x_1 <- na.omit(x)
summary(x_1)
```

```{r}
# 2. 단순대체
x_mean <- mean(x, na.rm = T); x_mean
x_2 <- x
x_2[is.na(x)] <- x_mean
round(x_2,2)
```


##### 이상치 처리

```{r}
if(!require(ggplot2)) { install.packages("ggplot2"); library(ggplot2); }
ggplot(wine, aes(x=as.factor(Class), y=Alcohol)) + geom_boxplot()
```

```{r}
ggplot(wine, aes(x=as.factor(Class), y=wine$Proline)) + geom_boxplot()
```

#### 데이터 가공

#### 데이터 분할

#### 모델 학습

#### 예측 및 평가

#### 성능개선

#### 결과 활용
