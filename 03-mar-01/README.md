# 2022년 03월

## TIL20220301

### 데이터 요약

#### 범주형 변수 요약

기술통계와 추론통계, 대부분은 모집단을 설명하는 추론통계이지만 모집단을 잘 설명하기 위해서는 표본집단을 잘 이해사고 적절한 통계기법을 선택하는 것이 중요하다.

**빈도표**

```
if(!require(MASS)) { install.packages("MASS"); library(MASS); }
```

```
str(survey)
```

```
levels(survey$Smoke)
```

```
frqtab <- table(survey$Smoke)
frqtab
```

```
class(frqtab)
```

```
frqtab[2]
```

```
frqtab["Never"]
```

**최빈값**

```
frqtab == max(frqtab)
```

```
frqtab[frqtab == max(frqtab)]
```

```
names(frqtab[frqtab == max(frqtab)])
```

```
which.max(frqtab)
```

```
frqtab[which.max(frqtab)]
```

```
names(frqtab[which.max(frqtab)])
```

**비율도표**

```
frqtab.prop <- prop.table(frqtab)
frqtab.prop
```

```
frqtab.prop["Never"]
```

```
frqtab.prop * 100
```

***

## TIL20220302

### 데이터 요약

#### 범주형 변수 요약

**비율 계산**

```
if(!require(MASS)) { install.packages("MASS"); library(MASS); }
```

```
survey$Smoke=="Never" # 비흡연자에 대한 논리연산
mean(survey$Smoke=="Never", na.rm = T) # 비흡연자에 대한 비율
```

```
head(anorexia)
```

```
anorexia$Postwt > anorexia$Prewt # 치료 후의 몸무게가 치료 전의 몸무게보다 큰가?
mean(anorexia$Postwt > anorexia$Prewt)
```

```
head(mammals)
```

```
# 두뇌의 무게가 2개의 표준편차보다 큰 논리연산식
abs(mammals$brain - mean(mammals$brain)) > 2*sd(mammals$brain)
```

```
mean(abs(mammals$brain - mean(mammals$brain)) > 2*sd(mammals$brain))
```

```
head(SP500)
```

```
# 수익률이 전일보다 증가한 일자 논리식
head(diff(SP500) > 0, 10)
```

```
mean(diff(SP500) > 0)
```

```
if(!require(vcd)) { install.packages("vcd"); library(vcd); }
```

```
str(Arthritis) # 류마티스 관절염 치료 효과
```

```
levels(Arthritis$Treatment)
levels(Arthritis$Improved)
```

```
crosstab <- table(Arthritis$Improved, Arthritis$Treatment,
                  dnn=c("Improved", "Treatment"))
crosstab
```

```
crosstab["Marked", "Treated"]
```

```
crosstab <- xtabs(~ Improved + Treatment, data = Arthritis)
crosstab
```

```
margin.table(crosstab, margin = 1) # 행
```

```
margin.table(crosstab, margin = 2) # 열
```

```
prop.table(crosstab, margin = 1) # 행의 합이 1
```

```
prop.table(crosstab, margin = 2) # 열의 합이 1
```

```
prop.table(crosstab)
```

```
addmargins(crosstab, margin = 1) # 합의 행을 생성
```

```
addmargins(crosstab, margin = 2) # 합의 열을 생성
```

```
addmargins(crosstab)
```

```
addmargins(prop.table(crosstab, margin = 2), 1)
```

```
if(!require(gmodels)) { install.packages("gmodels"); library(gmodels); }
```

```
CrossTable(Arthritis$Improved, Arthritis$Treatment,
           dnn=c("Improved", "Treatment"))
```

```
multtab <- table(Arthritis$Improved, Arthritis$Sex, Arthritis$Treatment)
multtab
```

```
multtab <- xtabs(~ Improved + Sex + Treatment, data = Arthritis)
multtab
```

```
ftable(multtab)
```

```
ftable(multtab, row.vars = c(2,3))
```

```
ftable(Arthritis[c("Improved", "Sex", "Treatment")], row.vars = c(2,3))
```

```
margin.table(multtab, 1)
margin.table(multtab, 2)
margin.table(multtab, 3)
```

```
ftable(prop.table(multtab, c(2,3)))
```

```
ftable(addmargins(prop.table(multtab, c(2,3))))
```

***

## TIL20220303

### 데이터 요약

#### 연속형 변수 요약

**중심경향 지표**

중심경향 지표(measures of central tendency)는 데이터가 특정 값을 중심으로 집중되어 있는 정도를 뜻한다.

* 중위수(median)
* 백분위수(quantile, percentile)
* 사분위수(quartile)
* 평균(mean)

```
if(!require(MASS)) { install.packages("MASS"); library(MASS) }
```

```
median(survey$Pulse) # 결측, 즉 NA 값에 따른 결과
```

```
median(survey$Pulse, na.rm=T) # 결측값 제거 후 계산산
```

```
quantile(survey$Pulse, probs = 0.5, na.rm = T) # 중위수
```

```
quantile(survey$Pulse, probs = c(0.05, 0.95), na.rm = T)
```

```
# Q1, ... Q4
quantile(survey$Pulse, na.rm = T)
```

```
quantile(survey$Pulse, seq(0,1,0.25), na.rm = T)
```

```
# 주어진 값으로 백분위수 계산
survey$Pulse <=80 # 80보다 작거나 같은 맥박수수
mean(survey$Pulse <= 80, na.rm = T)
```

```
mean(survey$Pulse, na.rm = T)
```

```
if(!require(palmerpenguins)) { install.packages("palmerpenguins"); library(palmerpenguins); }
```

```
summary(penguins$body_mass_g)
```

```
summary(penguins$species)
```

```
summary(as.character(penguins$species))
```

```
summary(penguins)
```

```
# list 형태를 인자로 입력하는 경우
penguins.list <- as.list(penguins)
summary(penguins.list)
```

```
# lapply()를 통해 요약통계량 계산
lapply(penguins.list, summary)
```

### 변동성 지표

변동성 지표(measures of variability)는 데이터의 산포 정도를 뜻한다.

* 범위(range)
* 사분위 범위(interquartile range)
* 분산(variance)
* 표준편차(standard deviation)

```
range(survey$Pulse, na.rm = T)
```

```
var(survey$Pulse, na.rm = T)
```

```
sd(survey$Pulse, na.rm = T)
```

R에서는 다양한 기술 통계량을 계산하는 함수들을 제공한다.

```
if(!require(pastecs)) { install.packages("pastecs"); library(pastecs); }
```

```
stat.desc(mtcars[c("mpg", "hp", "wt")])
```

```
if(!require(psych)) { install.packages("psych"); library(psych); }
```

```
describe(mtcars[c("mpg", "hp", "wt")])
```

집단별 기술 통계량을 계산한다.

```
levels(survey$Exer)
```

```
tapply(survey$Pulse, survey$Exer, mean, na.rm = T)
```

```
tapply(survey$Pulse, list(survey$Exer, survey$Sex), mean, na.rm = T)
```

```
aggregate(survey$Pulse, list(Exercise=survey$Exer, Sex=survey$Sex), mean, na.rm = T)
```

```
aggregate(survey[c("Pulse", "Age")],
          list(Exercise=survey$Exer, Sex=survey$Sex), 
          mean, na.rm = T)
```

aggregate()는 FUN 인수에 사용자 정의 함수를 사용할 수 있다.

```
myStats <- function(x, na.rm = F) {
  if(na.rm) x <- x[!is.na(x)]
  n <- length(x)
  mean <- mean(x)
  sd <- sd(x)
  skew <- sum((x-mean)^3/sd^3)/n
  kurt <- sum((x-mean)^4/sd^4)/n - 3
  return(c(n=n, mean=mean, sd=sd, skewness=skew, kurtosis=kurt))
}
```

```
aggregate(survey$Pulse, list(Exercise=survey$Exer, Sex=survey$Sex), myStats, na.rm = T)
```

```
by(survey[c("Pulse", "Age")], 
   list(Exercise=survey$Exer, Sex=survey$Sex), 
   summary)
```

```
aggregate(survey[c("Pulse", "Age")], 
   list(Exercise=survey$Exer, Sex=survey$Sex), 
   summary)
```

```
by(survey[c("Pulse", "Age")], 
   list(Exercise=survey$Exer, Sex=survey$Sex), 
   function(x) sapply(x, myStats, na.rm=T))
```

```
describeBy(survey[c("Pulse", "Age")], group = list(Exercise=survey$Exer))
```

***

## TIL20220304

### 가설검정

**가설의 종류**

* 대립가설(alternative hypothesis), 모집단에 대한 새로운 주장
* 귀무가설(null hypothesis), 기존의 주장

통계적 검정(statistical test) 또는 가설검정(hypothesis test)이란 표본 데이터를 기반으로 모집단에 대한 새로운 주장의 옮고 그름을 추론하는 과정을 말한다.

**가설검정 절차**

귀무가설이 사실이라는 전제하에서 수행되며 일반적으로 다음과 같은 절차를 따른다.

1. 표본으로부터 검정하고자 하는 **검정통계량(test statistic)** 계산
2. 검정통계량과 그 **확률분포**로부터 p-값(p-value) 계산

* 귀무가설이 사실이라는 가정하에서 관측한 통계량과 같거나 그보다 더 극단적인 값이 발생할 확률을 의미
* 유의확률(significance probability)이라고도 함

1. p-값이 매우 작으면 귀무가설 기각

* 판단의 기준으로 사용하는 5% 또는 1%의 확률을 유의수준(significance level)이라고 함
* 표본으로부터 관측된 결과(즉 계산된 통계량)가 나타날 가능성이 5% 미만 또는 1% 미만이 되는 귀무가설을 기각하면 이를 통계적으로 유의하다(statistically significant)라고 표현함

**가설검정과 검정력**

![](http://www.ktword.co.kr/img\_data/5094\_2.JPG)출처^\[http://www.ktword.co.kr/img\_data/5094\_2.JPG]

### 확률분포

![](https://miro.medium.com/max/1400/1\*fP1TTrA7TYD58rYgMHiL\_A.png)출처^\[https://miro.medium.com/max/1400/1\*fP1TTrA7TYD58rYgMHiL\_A.png]

**이항분포(binomial distribution)**

대표적인 이산확률분포(discrete probability distribution)로서 매회 어떤 사건이 일어날 확률이 동일한 독립 시행의 경우에 있어서 이 사건이 일어나는 횟수가 만들어 내는 분포이다. 예를 들면 동전 던지기로 동전을 일정 횟수 반복하여 던지는 실험에서 매 시행시마다 숫자면이 나타날 확률이 1/2이라고 할 때 숫자면이 나타나는 횟수는 이항분포를 따른다고 할 수 있다.

```
dbinom(7, 10, 0.5)  # 10번 던져 숫자면이 7번 나타날 확률
```

```
pbinom(7, 10, 0.5)  # 10번 던져 숫자면이 7번 이하가 나타날 확률
```

누적확률은 밀도함수의 합으로 계산이 가능하다.

```
sum(dbinom(c(0:7), 10, 0.5)) # 0번, 1번, ..., 7번 나타날 확률의 합
```

```
pbinom(7, 10, 0.5, lower.tail = F) # 1 - pbinom(7, 10, 0.5)
```

```
# 4번 이상 7번 이하 발생할 누적확률, 7번에서 4번의 누적확률을 빼서 계산
pbinom(7, 10, 0.5) - pbinom(3, 10, 0.5)
```

```
diff(pbinom(c(3,7), 10, 0.5))
```

```
set.seed(1)
rbinom(1, size=10, prob = 0.5)
rbinom(5, size=10, prob = 0.5)
```

***

## TIL20220305

### 정규분포

정규분포(normal distribution)는 대표적인 연속확률분포(continuous probability distribution)으로 통계적 검정을 위해 가장 널리 사용되는 분포이다. 정규분포에서는 대부분의 관측값이 중앙에 몰려 있으며 중앙에서 멀어질수록 그 빈도수가 점점 작아지는 종 모양의 대칭인 모습을 가진다.

```
if(!require(ggplot2)) { install.packages("ggplot2"); library(ggplot2); } 

x <- seq(-4, 4, length=100)
y <- dnorm(x)
df <- data.frame(x=x, y=y)
ggplot(df, aes(x,y)) +
  geom_line() + theme_bw()
```

```
ggplot(data = data.frame(x=c(65,135)), aes(x)) +
  stat_function(fun=dnorm, n=101, args=list(mean=100, sd=10)) +
  labs(title="Normal Distribution", x="x", y="") +
  scale_y_continuous(breaks = NULL) +
  theme_bw()
```

```
# IQ가 110 이하일 누적확률 계산
pnorm(110, mean=100, sd=10)
```

```
# IQ가 110 초과일 누적확률 계산
pnorm(110, mean=100, sd=10, lower.tail = F) # 1 - pnorm(110, mean=100, sd=10)
```

```
pnorm(0) # 표준정규 분포를 가정정
```

```
pnorm(0, mean=0, sd=1)
```

```
# 90 ~ 110 사이의 누적확률
pnorm(110, mean=100, sd=10) - pnorm(90, mean=100, sd=10)
```

```
diff(pnorm(c(90, 110), mean=100, sd=10))
```

주어진 누적확률의 관측값을 알고자 할 때는 qnorm() 함수를 수행한다.

```
qnorm(0.05, mean=100, sd=10)
```

```
qnorm(0.95, mean=100, sd=10)
```

```
qnorm(c(0.05, 0.95), mean=100, sd=10)
```

```
qnorm(c(0.025, 0.975))
```

```
rnorm(1, mean=100, sd=10)
```

```
rnorm(5, mean=100, sd=10)
```

```
rnorm(1)
```

```
rnorm(5)
```

### 데이터의 정규성 검정

```
set.seed(123)
shapiro.test(rnorm(100, mean=100, sd=10)) # 정규분포
```

```
shapiro.test(runif(100, min=2, max=4)) # 일항분포
```

```
set.seed(123)
qqnorm(rnorm(100, mean=100, sd=10), col="blue", main = "Sample from Normal Distribution")
qqline(rnorm(100, mean=100, sd=10))
```

x축은 이론적 정규 분포에 의해 생성된 표본이고 y축은 실제 표본이다.

```
set.seed(123)
qqnorm(runif(100, min=2, max=4), col="red", main = "Sample from Uniform Distribution")
qqline(runif(100, min=2, max=4))
```

***

## TIL20220306

### 대응표본 평균검정

독립표본 평균검정은 두 개의 표본이 서로 독립인 모집단으로부터추출되었다는 가정을 전제로 한다. 두 표본의 값이 쌍(pair)을 이루고 있는 경우 쌍을 이룬 값은 서로 독립이 아니며, 이처럼 검정하려고 하는 두 개의 표본이 서로 독립이 아닌 모집단으로부터 추출되었을 대 `대응표본 평균검정`(paired-samples t test)을 이용하여 두 집단 간의차이 검정을 수행할 수 있다.

| 독립표본                                                             | 대응표본                                                      |
| ---------------------------------------------------------------- | --------------------------------------------------------- |
| 무작위로 실험 대상자를선정하여 두 개의 집단으로 나눔                                    | 무작위로 실험 대상자를 선정                                           |
| 한 집단에는 앛미식사를 하고 IQ 테스트에 응하도록 하고 다른 집단에는 앛미식사를 거르고 IQ 테스트에참가하도록 함 | 각 실험 대아자를 대상으로 IQ 테스트를 두 차례 실시                            |
| 각 실험 대상자에 대해 하나씩의 IQ 테스트 점수를 얻게 됨                                | 한번은 아침칫가를 하고 테스트에 응하고 다른 한번은 아침식사를 하지 않은 상태로 테스트에 참가하도록 함 |
|                                                                  | 각 식험 대상자에 대해 두 개의 IQ 테스트 점수를 얻게 됨                         |

```
str(sleep)
```

```
t.test(extra ~ group, data = sleep, paired = T)
```

주어진 표본이 wide format일 경우 벡터를 직접 지정하여 수행한다.

```
if(!require(tidyr)) { install.packages("tidyr"); library(tidyr); }

sleep.wide <- spread(sleep, key = group, value = extra)
sleep.wide
```

```
t.test(sleep.wide$`1`, sleep.wide$`2`, paired = T)
```

### 독립표본 비율검정

* 귀무가설: 폐질환자 대비 흡연자의 비율이 병원별로 같다.
* 대립가설: 폐질환자 대비 흡연자의 비율이 병원별로 다르다.

```
# 4개 병원에 대한 폐질환자 및 흡연자 비율
patients <- c(86, 93, 136, 82) # 폐질환자
smokers <- c(83, 90, 129,70)   # 흡연자
smokers/patients # 페질환자 대비 흡연자 비율
```

```
prop.test(x=smokers, n=patients)
```

검정 수행 결과 네 병원의 폐질환자 대비 흡연자 수는 값다고 볼 수 없다.

### 독립표본 평균검정

`독립표본 평균검정`(two-independent samples t test)는 두 개의 독립표본 데이터를 이용하여 각각 대응되는 두 개의 모집단 평균이 서로 동일한지 검정한다. 두 집단이 서로 차이가 있는지를 검정하고자 할 때 수행한다.

* 귀무가설: 두 집단의 평균에는 차이가 없다(같다).
* 대립가설: 두 집단의 평균에는 차이가 있다(다르다).

**예제**

고양이의 성별에 따른 몸무게의 차이가 있는지를 검정한다.

* 귀무가설: 고양이 성별에 따른 몸무게 차이는 없다.
* 대립가설: 고양이 성별에 따른 몸무게 차이는 있다.

```
t.test(formula = Bwt ~ Sex, data = cats)
```

```
Bwt.f <- cats$Bwt[cats$Sex=="F"]
Bwt.m <- cats$Bwt[cats$Sex=="M"]
mean(Bwt.f); mean(Bwt.m);
t.test(Bwt.f, Bwt.m)
```

### 일표본 비율검정

`prop.test()` 함수는 모집단에 대한 표본의 비율에 대한 검정을 수행한다.

**예제**

프로야구 팀이 30경기 중 18승을 거두었을 때, 승률이 50%가 넘는다고 말할 수 있는가?

* 귀무가설: 승률이 50% 이하다.
* 대립가설: 승률이 50% 이상이다.

```
# prop.test(x=성공횟수, n=시행횟수, p=검정코자하는비율)
prop.test(x=18, n=30, p=0.5, alternative = "greater")
```

### 일표본 평균검정

일표본 평균검정(one-sample t test)는 하나의 표본 데이터를 이용하여 모집단의 평균이 특정 값과 같은지 검정하는 것이다. 표본집단이 특정 모집단과 일치하는지 혹은 그렇지 않은지를 알고 싶을 때 이용한다.

```
str(cats)
```

* 귀무가설: 고양이의 몸무게가 2.6kg이다.
* 대립가설: 고양이의 몸무게가 2.6kg이 아니다.

```
t.result <- t.test(x=cats$Bwt, mu=2.6); t.result
```

```
p95 <- qt(0.975, df=143)

ggplot(data = data.frame(x=c(-4,4)), aes(x)) +
  stat_function(fun=dt, args = list(df=143)) +
  labs(title="t Distribution", x="x", y="") +
  scale_y_continuous(breaks = NULL) +
  geom_vline(xintercept=t.result$statistic, color="blue", linetype = "dashed", size=1) +
  geom_text(x=t.result$statistic+0.4, y=0.02, aes(label=round(t.result$statistic,2)), col="blue") +
  geom_vline(xintercept=p95, color="red", linetype = "dashed", size=1) +
  geom_text(x=p95+0.3, y=0.06, aes(label=round(p95,2)), col="red") +
  theme_bw()
```

* 귀무가설: 고양이의 몸무게가 2.7kg이다.
* 대립가설: 고양이의 몸무게가 2.7kg이 아니다.

```
t.result <- t.test(x=cats$Bwt, mu=2.7); t.result
```

```
p95 <- qt(0.975, df=143)

ggplot(data = data.frame(x=c(-4,4)), aes(x)) +
  stat_function(fun=dt, args = list(df=143)) +
  labs(title="t Distribution", x="x", y="") +
  scale_y_continuous(breaks = NULL) +
  geom_vline(xintercept=t.result$statistic, color="blue", linetype = "dashed", size=1) +
  geom_text(x=t.result$statistic+0.4, y=0.02, aes(label=round(t.result$statistic,2)), col="blue") +
  geom_vline(xintercept=p95, color="red", linetype = "dashed", size=1) +
  geom_text(x=p95+0.3, y=0.06, aes(label=round(p95,2)), col="red") +
  theme_bw()
```

### 평균검정

`평균검정`은 평균에 대한 가설검정을 의미한다. 선정한 표본이 특정 평균값을 갖는 모집단에 속하는지(즉 표본의 평균과 모집단의 평균이 동일한지) 또는 두 표본 집단의 평균값 간에 차이가 존재하는지(즉 두 표본집단이 동일한 모집단에 속하는지) 검정한다. 일표본 평균검정, 독립표본 평균검정, 대응표본 평균 검정이 있다.

평균에 대한 가설검정은 t검정(t test)을 통해 수행할 수 있다. 표본평균이 모집단 평균과 동일한지 여부는 t값을 검정 통계량으로 사용하여 검정한다.

$$
t = \frac{\bar{x}-\mu}{\frac{s}{\sqrt{n}}}
$$

**예제**

* 귀무가설: 벤처기업 경영자의 혈압은 일반일과 같다
* 대립가설; 벤터기업 경영자의 혈압은 일반일과 다르다
* 표본: 20명의 벤처기업 경영자 평균 135, 표준편차 25
* 모집단: 일반인 혈압 평균 115

$$
검정통계량 \ \ t = \frac{135-115}{\frac{25}{\sqrt{20}}} = 3.58
$$

```
t <- 3.58; n <- 20;
pt(t, df=n-1) # t값에 해당하는 누적확률 계산

# 특정 t값 이상의 누적확률에 관심이 있으므로 lower.tail을 F로 설정
# 반대편도 고려해야 함으로 두배 함
pt(t, df=n-1, lower.tail = F)*2
```

모집단 평균 115라는 가정하에서 135라는 평균은 0.002의 유의확률을 가지므로 5% 유의수준 하에서 귀무가설을 기각하고 대립가설을 채택한다.

유사한 방식으로 유의수준 0.05에 해당하는 t값을 계산하고 관측된 t값을 비교하여 검정한다.

```
p95 <- qt(0.025, df=n-1, lower.tail = F); p95
```

주어진 t 값은 유의수준 5%에 해당하는 t값의 오른쪽에 위치함으로 귀무가설을 기각하고 대립가설을 채택한다.

```
dt_range <- function(x) {
  y <- dt(x, df=19)
  y[x < 2.09] <- NA
  return(y)
}

ggplot(data = data.frame(x=c(-4,4)), aes(x)) +
  stat_function(fun=dt, args = list(df=19)) +
  stat_function(fun=dt_range, geom="area", fill="salmon", alpha=.5) +
  labs(title="t Distribution", x="x", y="") +
  scale_y_continuous(breaks = NULL) +
  geom_vline(xintercept=t, color="blue", linetype = "dashed", size=1) +
  geom_text(x=t+0.3, y=0.02, aes(label=t), col="blue") +
  geom_vline(xintercept=p95, color="red", linetype = "dashed", size=1) +
  geom_text(x=p95+0.3, y=0.06, aes(label=round(p95,2)), col="red") +
  theme_bw()
```

***

## TIL20220307

### 결측치 처리

#### 결측치 종류

![결측치 종류](https://miro.medium.com/max/1400/1\*cPNnAnoOYArYyTDPNjJg3A.gif)

#### 확인

```
## summary()
summary(penguins)
```

```
colSums(is.na(penguins)); nrow(penguins)
```

등등등

#### 제거

```
penguins.naomit <- na.omit(penguins)
colSums(is.na(penguins.naomit)); nrow(penguins.naomit)
```

```
penguins.naomit <- penguins[complete.cases(penguins), ]
colSums(is.na(penguins.naomit)); nrow(penguins.naomit)
```

제거 후 11개 행이 감소된 것을 볼 수 있다.

#### 대체

#### 0으로 대체

```
# 연속형 변수에 대해서만 적용
if(!require(dplyr)) { install.packages("dplyr"); library(dplyr); }

penguins.0 <- penguins[c(3:6)] %>%
  select_if(function(x) any(is.na(x))) %>% 
  replace(is.na(.), 0)
colSums(is.na(penguins.0))
```

#### 평균으로 대체

```
penguins.mean <- penguins[c(3:6)] %>% 
  select_if(function(x) any(is.na(x))) %>% 
  mutate(bill_length_mm = ifelse(is.na(bill_length_mm), mean(bill_length_mm, na.rm=T), bill_length_mm),
         bill_depth_mm = ifelse(is.na(bill_depth_mm), mean(bill_depth_mm, na.rm=T), bill_depth_mm),
         flipper_length_mm = ifelse(is.na(flipper_length_mm), mean(flipper_length_mm, na.rm=T), flipper_length_mm),
         body_mass_g = ifelse(is.na(body_mass_g), mean(body_mass_g, na.rm=T), body_mass_g))
colSums(is.na(penguins.mean))
```

```
# 0으로 대체한 경우와 평균값으로 대체한 경우의 차이
colMeans(penguins[c(3:6)], na.rm = T); colMeans(penguins.0); colMeans(round(penguins.mean,1));
```

```
all_column_median <- apply(penguins[c(3:6)], 2, median, na.rm=T); all_column_median
```

```
penguins.median <- penguins[c(3:6)]
for(i in colnames(penguins.median)) { 
  penguins.median[is.na(penguins.median[,i]), i] <- all_column_median[i]
}
colMeans(round(penguins.median))
```

***

## TIL20220308

### R 에러 수정

```
> library(dplyr)

Error: package or namespace load failed for ‘dplyr’ in loadNamespace(i, c(lib.loc, .libPaths()), versionCheck = vI[[i]]):

 ‘rlang’이라고 불리는 패키지가 없습니다

In addition: Warning message:

패키지 ‘dplyr’는 R 버전 3.4.4에서 작성되었습니다 
```

이런 식으로 에러가 발생하면 깔끔하게 R을 재설치 하자. libpath나 패키지 재설치 등의 방법이 언급되지만 안되는 경우가 있다. 한시간 반 소비하고 내린 결론이다.

4.0.3에서 문제가 일어났고 4.1.2로 버전 업해서 문제 해결되었다.

```
Error:
! Assigned data `all_column_mean[i]` must be compatible with existing data.
i Error occurred for column `flipper_length_mm`.
x Can't convert from <double> to <integer> due to loss of precision.
* Locations: 1.
Backtrace:
  1. base::`[<-`(`*tmp*`, is.na(p.mean[, i]), i, value = `<dbl>`)
 19. tibble `<fn>`(`<vctrs___>`)
```

`p.mean <- as.data.frame(penguins[c(3:6)])`와 같이 데이터 형태를 명시적으로 지정해 준다.

### 결측치 시각화

```
if(!require(mice)) { install.packages("mice"); library(mice); }

md.pattern(penguins, plot=T, rotate.names = T)
```

***

## TIL20220309

### 클래스 불균형과 샘플링

분류 분석의 경우 관찰된 표본 범주 비율이 큰 쪽으로 편향되는 경향이 있다. 이를 해결하기 위해 범주의 비율을 조절하여 정제한다.

![Downsampling & Upsampling^\[https://raw.githubusercontent.com/rafjaa/machine\_learning\_fecib/master/src/static/img/resampling.png\]](https://raw.githubusercontent.com/rafjaa/machine\_learning\_fecib/master/src/static/img/resampling.png)

![SMOTE^\[https://raw.githubusercontent.com/rafjaa/machine\_learning\_fecib/master/src/static/img/smote.png\]](https://raw.githubusercontent.com/rafjaa/machine\_learning\_fecib/master/src/static/img/smote.png)

* Upsampling: this method increases the size of the minority class by sampling with replacement so that the classes will have the same size.
* Downsampling: in contrast to the above method, this one decreases the size of the majority class to be the same or closer to the minority class size by just taking out a random sample.
* Hybrid methods : The well known hybrid methods are ROSE (Random oversampling examples), and SMOTE (Synthetic minority oversampling technique), they downsample the majority class, and creat new artificial points in the minority class. For more detail about SMOTE method click here, and for ROSE click here.

from: Methods for dealing with imbalanced data^\[https://www.r-bloggers.com/2019/04/methods-for-dealing-with-imbalanced-data/]

```
```

***

## TIL20220310

```
if(!require(MASS)) { install.packages("MASS"); library(MASS); }

data("BreastCancer")
bc <- BreastCancer[, -1] # Id 열 제외
str(bc)
```

```
train.index <- createDataPartition(bc$Class, p=0.75, list=F)
bc.train <- bc[train.index, ]; bc.test <- bc[-train.index, ];
rbind(TrainData = table(bc.train$Class), TestData = table(bc.test$Class))
```

```
# upsampling / downsample / SMOTE
bc.train.up <- upSample(subset(bc.train, select = -Class), bc.train$Class)
bc.train.down <- downSample(subset(bc.train, select = -Class), bc.train$Class)
bc.train.smote <- SMOTE(Class ~ ., bc.train, prec.over = 900, perc.under=150)
rbind(Upsampling = table(bc.train.up$Class),
      Downsampling = table(bc.train.down$Class),
      SMOTE = table(bc.train.smote$Class))
```

```
p.dt <- rpart(Class ~ ., bc.train)
p.dt.pred <- predict(p.dt, bc.test, type = "class")
orig.cm <- confusionMatrix(p.dt.pred, bc.test$Class)$overall[1]
```

```
p.dt <- rpart(Class ~ ., bc.train.up)
p.dt.pred <- predict(p.dt, bc.test, type = "class")
up.cm <- confusionMatrix(p.dt.pred, bc.test$Class)$overall[1]
```

```
p.dt <- rpart(Class ~ ., bc.train.down)
p.dt.pred <- predict(p.dt, bc.test, type = "class")
down.cm <- confusionMatrix(p.dt.pred, bc.test$Class)$overall[1]
```

```
p.dt <- rpart(Class ~ ., bc.train.smote)
p.dt.pred <- predict(p.dt, bc.test, type = "class")
smote.cm <- confusionMatrix(p.dt.pred, bc.test$Class)$overall[1]
```

```
rbind(Orig = orig.cm,
      Upsampling = up.cm,
      Downsampling = down.cm,
      SMOTE = smote.cm)
```

상황에 따라 결과가 다르게 나오지만 대체적으로 SMOTE에서 높은 정확도를 보인다.

### SMOTE 데이터 형식 오류

[Why do I get 'Error in T\[, col\] <- data\[, col\]' when I use SMOTE in R?](https://stackoverflow.com/questions/62750638/why-do-i-get-error-in-t-col-data-col-when-i-use-smote-in-r)

변수는 facter형이고, tibble 형식을 지원하지 않는다.

***

## TIL20220311

DWmR 패키지는 github actions로 설치 안되는 걸로...\
RStudio에서 rendering 후 업로드 하자.

### URL을 통해 직접 패키지 설치

Install an R package directly from a URL for the package source^\[https://stackoverflow.com/questions/16412638/install-an-r-package-directly-from-a-url-for-the-package-source]

```
install.packages("https://cran.r-project.org/src/contrib/Archive/DMwR/DMwR_0.4.1.tar.gz", repos=NULL, method="libcurl")
```

```
data("BreastCancer")
bc <- BreastCancer[, -1] # Id 열 제외
```

```
bc.smote <- SMOTE(Class ~ ., bc, perc.over = 100, perc.under = 200)
bc.smote.compete <- complete(bc.smote)
rbind(Orig = table(bc$Class), SMOTE = table(bc.smote.compete$Class))
```

***

## TIL20220312

### RStudio Chunk options

R Code Chunks^\[https://zorba78.github.io/cnu-r-programming-lecture-note/r-code-chunks.html]

Rmarkdown으로 문서 작성 시 꼭 필요한 사용하게 된다. 알아 둘 것.

```
knitr::opts_chunk$set(# root.dir = '../..', # 프로젝트 폴더 지정
                      eval = TRUE,
                      echo = FALSE,
                      cache = FALSE,
                      include = TRUE,
                      tidy = TRUE,
                      tidy.opts = list(blank=FALSE, width.cutoff=120), # 소스 출력길이 지정
                      message = FALSE,
                      warning = FALSE,
                      engine = "R", # Chunks will always have R code, unless noted
                      error = TRUE,
                      fig.path="Figures/",  # Set the figure options
                      fig.align = "center",
                      fig.width = 7,
                      fig.height = 7,
                      fig.keep='all', fig.retina=2)
```

***

## TIL20220313

### 시계열 데이터 분할

출처: 시계열 데이터 - 항공여객(Air Passenger) 데이터 ^\[http://aispiration.com/model/model-rsampling-time-series.html]

시계열은 일반적인 방법으로 표본상에서 랜덤하게 원소를 추출할 수 없다. 시간 흐름을 고려하여 훈련 데이터와 시험 데이터로 분할해야 한다.

```
train = 1:18
test = 19:24
par(mar=c(0,0,0,0))
{plot(0,0,xlim=c(0,26),ylim=c(0,2),xaxt="n",yaxt="n",bty="n",xlab="",ylab="",type="n")
arrows(0,0.5,25,0.5,0.05)
points(train, train*0+0.5, pch=19, col="blue")
points(test,  test*0+0.5,  pch=19, col="red")
text(26,0.5,"시간")
text(10,0.7,"훈련데이터",col="blue")
text(21,0.7,"시험데이터",col="red")}
```

```
# Core Tidyverse
if(!require(tidyverse)) { install.packages("tidyverse"); library(tidyverse); }
if(!require(glue)) { install.packages("glue"); library(glue); }
if(!require(forcats)) { install.packages("forcats"); library(forcats); }

# Time Series
if(!require(timetk)) { install.packages("timetk"); library(timetk); }
if(!require(tidyquant)) { install.packages("tidyquant"); library(tidyquant); }
if(!require(tibbletime)) { install.packages("tibbletime"); library(tibbletime); }
if(!require(sweep)) { install.packages("sweep"); library(sweep); }

# Visualization
if(!require(cowplot)) { install.packages("cowplot"); library(cowplot); }

# Preprocessing
if(!require(recipes)) { install.packages("recipes"); library(recipes); }

# Sampling / Accuracy
if(!require(rsample)) { install.packages("rsample"); library(rsample); }
if(!require(yardstick)) { install.packages("yardstick"); library(yardstick); }

# Modeling
if(!require(forecast)) { install.packages("forecast"); library(forecast); }

data("AirPassengers")

ap_ts <- AirPassengers %>% 
  tk_tbl() %>% 
  mutate(index = as_date(index)) %>% 
  as_tbl_time(index = index) %>% 
  filter(index >= "1950-01-01", index <= "1959-12-31")

ggplot(ap_ts, aes(x=index, y=value)) +
  geom_line()
```

오늘은 여기까지...

***

## TIL20220314

데이터 분할, 이건 내일 정리하자. 양이 많네.

### 일반적인 데이터 분할

```
if(!require(caret)) { install.packages("caret"); library(caret); }

trainIndex <- createDataPartition(penguins$species, p=.7, list=F)
pTrain <- penguins[trainIndex, ]
pTest <- penguins[-trainIndex, ]
addmargins(addmargins(rbind(
  pTrain = table(pTrain$species),
  pTest = table(pTest$species)
),2),1)
```

***

## TIL20220315

### caret을 이용한 기계학습 절차

* 데이터 전처리
* 데이터 분할
* 학습
* 성능평가
* 하이퍼 파라메터 튜닝

```
# 0. 데이터 준비
data("penguins")
str(penguins)
```

```
summary(penguins)
```

```
# 1. 데이터 전처리

if(!require(mice)) { install.packages("mice"); library(mice); }

penguins.preprocessing <- mice(penguins, m=1, print=F)

# 결측치 처리
data <- complete(penguins.preprocessing)

# 수치형 변수 정규화
data[, c(3:6)] <- scale(data[, c(3:6)])

# 년도 범주로 변환
data$year <- as.factor(data$year)
```

```
summary(data)
```

```
# 2. 데이터 분할
train.index <- createDataPartition(data$sex, p=0.7, list=F)
data.train <- data[train.index, ]
data.test <- data[-train.index, ]

addmargins(rbind(
  TrainSet = table(data.train$sex),
  TestSet = table(data.test$sex)
),2)
```

```
# 3. 학습
fitControl <- trainControl(method = "repeatedcv", repeats = 5)
model.rf <- train(sex ~ ., data=data.train, method = "rf", trControl = fitControl); model.rf
```

```
# 4. 성능평가
model.rf.pred <- predict(model.rf, newdata = data.test)
model.rf.cm <- confusionMatrix(model.rf.pred, data.test$sex); model.rf.cm
```

```
# 5. 하이퍼 파라메터 튜닝

## 5-1. custom search grid
customGrid <- expand.grid(mtry = 1:(dim(data.train)[2]-1))
model.rf.tuned <- train(sex ~ ., data=data.train, method = "rf", 
                        trControl = fitControl,
                        tuneGrid = customGrid); model.rf.tuned
```

```
model.rf.tuned.pred <- predict(model.rf.tuned, newdata = data.test)
model.rf.tuned.cm <- confusionMatrix(model.rf.tuned.pred, data.test$sex); model.rf.tuned.cm
```

```
# 5-2. Random Search Grid
fitControl.random <- trainControl(method = "repeatedcv", repeats = 5, search = "random")
model.rf.tuned2 <- train(sex ~ ., data=data.train, method = "rf", 
                        trControl = fitControl.random,
                        tuneLength = 10); model.rf.tuned2
```

```
model.rf.tuned2.pred <- predict(model.rf.tuned2, newdata = data.test)
model.rf.tuned2.cm <- confusionMatrix(model.rf.tuned2.pred, data.test$sex); model.rf.tuned2.cm
```
