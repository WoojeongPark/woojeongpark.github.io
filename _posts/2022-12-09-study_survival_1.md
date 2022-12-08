---
title:  "[Statistics] Survival Analysis 생존분석 기초개념 정리"
excerpt: "스터디-통계 "

categories: [Study, Statistics]
tags:
  - [생존분석, 보건통계, 통계, survival, survival analysis, HR, statistic, statistics]

toc: true
toc_sticky: true
 
date: 2022-12-09
last_modified_at: 2022-12-09
math: true
comments : true
mermaid: true
---


# 1. 생존분석

## 1.1. 개괄
- 생존분석 : 관심사건(event of interest)이 발생하기까지 걸린 시간을 분석하는 통계적 방법론
- 생존시간과 관심사건 발생여부가 종속변수
- 생존함수를 추정하거나 생존함수에 유의한 영향을 미치는 독립변수를 파악하고 그 효과를 추정하는데 사용


## 1.2. 생존자료 survival data
- 생존자료 : 생존시간 $T$, 사건 $D$
  - 개체 $i(i=1, \cdots, n)$에 대한 관측 : $(t_i, d_i), t_i>0, d_i=0, 1.$
  - $d_i=1$이면 $T=t_i$에서 사건(event, 사망)이 발생하였음을 의미한다.
  - $d_i = 0$인 경우는 $T=t_i$에서 관측불능(fail to observe) 상황이 되었음을 의미한다.
    - 추적 실패(loss to follow up) 
    - 연구의 종료
- 생존분포 : 생존시간 $T$에 대한 확률분포
  - 지수분포 $f_T(t; \lambda) = \lambda e^{-\lambda t}, t>0, \lambda >0$
  - 와이블 분포 $f_T(t;\alpha, \beta) = \frac{\alpha}{\beta} (\frac{t}{\beta})^{\alpha-1} e^{-(\frac{t}{\beta})^\alpha}, t>0; \alpha>0, \beta>0$
    - $\alpha=1$, $\lambda=\frac{1}{\beta}$이면 지수분포와 같다.
- 생존함수(survival function): $S_T(t) = P(T \geq t), t>0$
  - 생존함수는 임의개체가 시점 $t>0$에 생존해 있을 확률이다.
  - $S_T(t) = 1-F_T(t_-)$, 여기서 $F_T(t)$는 분포함수, 즉 누적확률을 의미한다. $t_-$는 $t$보다 약간 작은 시점을 의미한다.
  - 지수분포 : $S_T(t; \lambda) = e^{-\lambda t}, t\geq0$
  - 와이블 분포 : $S_T(t;\alpha, \beta) = e^{-(\frac{t}{\beta})^\alpha}, t>0$
  - 둘 다 감소하는 형태이다.
  
- 위험함수(hazard function) : $h_T(t) = \frac{f_T(t)}{S_T(t)}, t>0$
- 위험함수는 $t>0$에서의 조건부 사건 발생률이다.
$$
h_T(t) =\lim_{h->0^+} \frac{1}{h} P(t \leq T < t+h | T \geq t)
$$
- 지수분포의 경우 $h_T(t; \lambda) = \lambda, t>0$
  - 위험률은 시간의 흐름과 관계없이 일정하다.
- 와이블 분포 : $h_T(t; \alpha, \beta) = (t/ \beta)^{\alpha-1}, t>0$
- $\alpha>1$인 경우, 시간의 흐름에 따라 위험률이 증가한다.
  
---
## 1.3. 모수적 생존분포의 추정

### 1.3.1. 최대가능도 추정
$$\underset{\theta}{\text{max}} \Pi_{i=1}^n f_T(t_i;\theta)^{d_i} \{1-F_T(t_i; \theta)\}^{1-d_i}$$


------

# 2. Workshop

## 2.1. Cox proportional hazards(PH) model

### 2.1.1. 위험함수(Hazard function)
- 어떤 시간까지 생존했다고 가정했을 때, 바로 다음의 매우 작은 시간간격 사이에서 사건이 발생할 확률
- 환자가 특정 시험 $t$ 직후에 바로 사망할 확률(=순간위험율)
- 
  $
  h(t) = P(T=t | T \geq t) = \frac{f(t)}{S(t)}
  $
  - $h(t)$ : $t$ 시점에서의 위험을 의미
  - $T \geq t$는 t까지 살아남았을 때를 의미
  
- 생존곡선에 영향을 주는 위험요인과의 관련성을 모형화하는 것이 목적이다.
- 생존자료에서 다른 변수들의 효과를 보정한 후, treat효과를 볼 수 있는 갖아 대표적인 통계모형이다.

## 1.2. Cox PH model

### 1.2.1. Semi-parametric model
- 시간에 대한 분포가정은 없지만, 생존시간과 위험요인 사이의 관계는 모형이 가정된다.
- 공변량, 보정변수들을 고려하여 이들의 선형관계식으로 표현
  
- 위험비율은 시간에 관계없이 일정하다는 '비례위험(proportional hazard)' 가정을 만족해야 한다.
  - 비례가정은 반드시 확인하는 것이 원칙이다.
  - 비례가정이 만족되지 않을 경우 time dependent covariate approach Extended Cox 모형을 사용한다.
- Hazard Ratio(HR)로 위험의 크기를 해석한다.

### 1.2.2. 생존시간 T에 영향을 주는 변수들
- $x_1, x_2, \cdots, x_p$
  
### 1.2.3. Hazard function
- $h(t) = h_0(t) \exp(\beta_1x_1+\cdots+\beta_px_p)$
  - $h_0(t)$ : 기저위험함수, 모든 $x$들이 0일 때의 위험함수
- 비례위험(proportional hazards)
  - $\frac{h_i(t)}{h_j(t)} = \exp [\beta_1(x_{i1}-x_{j1}) + \cdots + \beta_p (x_{ip}-x_{jp})]$
  - $i$번째 환자와 $j$번째 환자의 위험비는 시간과 무관하게 상수가 된다.

## 1.2. Cox PH model : 이산형변수

### 1.2.1. 성별에 따른 차이
- Female : $x_1 = 1$
- Male : $x_1 = 0$

### 1.2.2. Female
- $$\log h(t|Female) = \log h_0(t)+\beta_1 \times 1 + \cdots + \beta_px_p $$

### 1.2.3. Male
- $$\log h(t|Male) = \log h_o(t) + \beta_1 \times 0 + \cdots + \beta_p x_p$$

### 1.2.4. HR
- $$\log{h(t | Female)} - \log{h(t|Male)}= \log{ \frac{h(t|Female)}{h(t|Male)}} = \beta_1 \times 1 - \beta_1 \times 0 = \beta_1$$
- Hazard Ratio(HR) : 
  $$\frac{h(t|Female)}{h(t|Male)} = \exp{\beta_1}$$
- if HR=1.25($\beta=0.22$), reference=Male이라면 남자에 비해 여자가 1.25배 위험하다는 뜻이다.
- 생존분석에서는 $\beta_1$보다는 $\exp(\beta_1)$을 구해서 두 그룹의 위험비율을 생각한다.

## 1.2. Cox PH model : 연속형변수

### 1.2.1. 연령의 효과($x_1$)
- Age : $x_1 = x+1$ vs $x_1=x$
- Age = $x+1$
  - $$ \log{h(t|Age = x+1)} = \log{h_0(t)}+\beta_1 (x+1)+\cdots+\beta_px_p $$
- Age = $x$
  - $$\log h(t|Age=x) = \log h_0(t) + \beta_1 (x) + \cdots + \beta_p x_p$$

- 둘이 빼면 
  - $$\frac{h(t|Age=x+1)}{h(t|Age=x)} = \exp(\beta_1)$$
  - Hazard Ratio(HR)

- HR = 1.75($\beta = 0.56$)
  - 연령이 1세 증가할수록 위험비가 1.75배 증가
- HR = 0.75($\beta = -0.29$)
  - 연령이 1세 증가할수록 위험비가 0.75배 증가
  - 연령이 1세 감소할수록 0.75의 역수인 1.33배 증가

