---
title:  "[Statistics] GWR vs OLS"
excerpt: "스터디-통계 "

categories: [Study, Statistics]
tags:
  - [최소자승, 최소제곱, 가중평균, 통계, GWR, OLS, weighted sum, Least square, statistic, statistics]

toc: true
toc_sticky: true
 
date: 2022-12-10
last_modified_at: 2022-12-10
math: true
comments : true
mermaid: true
---

## Paper 1 : 지리적 가중회귀모형을 이용한 지역별 심정지 발생요인에 관한 연구
- > 보건사회연구 33(3), 2013, 237-257 Health and Social Welfare Review
- > 투고일 : 2013.06.11
- > 본 연구는 전진호 외(2012)의 ‘심정지 발생 및 생존 관련 요인의 자료수집 및 관리체계 구축’ 연구보고서 (질병관리본부 발주)에 수록된 내용의 일부를 수정 및 보완한 것이다.
  
### Abstract
- 데이터 : 심정지 조사 자료, 지역사회건강 조사 자료
- 방법론 : 생태학적 방법론, 지리적 가중회귀모형(GWR)
- 결과 : 지역별 심정지 발생의 주요 원인 규명 + GWR 모형의 지역별 심정지 예발관리 사업에 적용하는 것의 유용성 검토
  - 중증도 신체활동 실천율
  - 비만율
  - 고혈압 평생 의사 진단 경험률
  - 당뇨병 평생 의사 진단 경험률
  - GWR은 모형개발에 사용된 자료의 한계로 인해 본 연구에서 설명력이 낮으나, 전통적인 OLS 모형보다는 우수한 모형인 것으로 나타남

### Keywords : 심정지 발생률, 생태학적 방법론, OLS모형, 지리적 가중회귀모형

### 서론
- 심정지 발병은 증가하나 생존율은 낮음. 위험요인을 규명해봐야!
- 선행연구 : 인구 사회경제학적 요인, 질환 요인, 생활행태 요인으로 분류
  - 연령, 소득, 교육수준, 독신가구
  - 허혈성 심장질환, 죽상경화증, 심근병증, 심장판막증, 선천성 심장 질환, 당뇨병, 고혈압 등
  - 흡연, 음주, 격렬한 운동, 커피섭취 등
- 효과적인 심정지 관리를 위해서는 지역 특성에 맞는 지역별 심정지 예방 사업 수립해야! == GWR 사용
- `OLS(Ordinary Least Square)분석` : 최소제곱법으로 모수를 추정하여 특정질환의 발생 위험요인을 규명하고자 함에 쓰임
- > 생태학적 접근방법론 + 지리적 __가중회귀모형(GWR; Geographically Weighted Regression, 이하 GWR)__

### 연구방법
#### 지리적 가중회귀모형
- `일반 최소제곱법(OLS)`
  - 전통적 회귀분석으로 주로 언급됨
  - 관찰들 관의 독립성과 오차 동분산성(homoscedasticity)를 가정하여 공간적 변이 측면을 고려하지 못함.
  - 전통적 회귀분석에서는 표집 위치에 상관없이 관찰들은 서로 독립적이어야 하고, 종속변수의 관찰값과 추정값의 차이인 오차(errors)가 상호 독립적이며 분산이 일정한 것으로 가정
- 그러나 공간적으로 근접한 위치에 표집 된 사례일수록 유사한 값을 가지는 경향이 있기 때문에 현실적으로 이러한 가정이 충족되기는 어려움
- 따라서 공간적 이질성 또는 의존성이란 특성들이 존재하는 현상을 OLS
회귀모형으로 분석하게 되면 모수 추정치의 효율성이 떨어짐
- `지리적 가중회귀분석`이 대안이 될 수 있음. 
  - 지역별로 각각 다른 계수의 추정이 가능하여 기존 모형들로는 파악하기 어려운 공간적으로 이질적인 패턴을 확인

![](/assets/img/2022-12-09-02-08-30.png)

---

__지리적 가중회귀모형 식__ 

회귀식은 아래와 같이 표현가능하다.

$$y_i(\mu) = \beta_{0i}(\mu) + \beta_{1i}(\mu)x_{1i}+ \cdots + \beta_{mi}(\mu)x_{mi} + \epsilon_i(\mu)$$

  - $\mu$ : 위치
  - $y$ : 종속변수
  - $m$ : 독립변수 $x$의 개수
  - $\beta$ : 회귀계수
  - $\epsilon$ : 오차항
  - $i \in \{1, 2, \cdots, n \}$ : 관측 인덱스

여기서 가중 최소자승법(Weighted Least Square Estimation)을 이용하자. 즉, 

$$\epsilon(\mu) = y_i(\mu) - \beta_{0i}(\mu) + \beta_{1i}(\mu)x_{1i}+ \cdots + \beta_{mi}(\mu)x_{mi}$$

에 대하여 weight $w_i$를 생각하여

$$\underset{\beta_{ij}, i \in \{1, \cdots,n \}, j\in\{1,\cdots,m\}}{\text{minimize }} \sum_{i=1}^m w_i \{\epsilon_i(\mu)\}^2$$

이를 달성하면 된다. 이는 각 $\beta_{ij}$에 대하여 미분하여 얻을 수 있다. 적당한 matrix calculation을 통해 다음을 얻는다.

$$(X^TWX) \hat{\beta} = X^T W Y $$

따라서 최종적인 회귀계수 추정식은 아래와 같이 얻어진다.

$$\hat{\beta} = [X^TWX]^{-1} X^T W Y$$

여기서 가중치행렬 $W$는 여러 커널함수중에 하나를 택할 수 있는데, 주로 Gaussian form을 많이 쓴다.

$$\displaystyle{w_i(\mu) = \exp (-\frac{1}{2} \left(\frac{d_i(\mu)}{h}\right)^2) \\
w_i(\mu) \text{ : 공간좌표에서 관측치 $i$에 대한 가중치} \\
d_i(\mu) : \text{ : 관측치 $i$와 공간좌표 $\mu$간의 거리} \\
h \text{ : 대역폭}}$$

커널함수는 가중치를 만드는 대역폭이 고정되어 있는 __고정방식(Fixed spatial kernel)__, 그리고 관측치 수에 따라 다른 대역폭을 사용하는 __가변방식(adaptive spatial kernel)__ 이 있다. 주로 관측치가 조사지역에 규칙적으로 있으면 전자, 관측치 분포가 다양하면 후자를 쓴다. 확실치 않은 경우, 후자가 안전하다. 

적정 대역폭 설정하기 위해서 __AIC(Akaike Information Criterion)__ 또는 __CV(Cross Validation)__ 가 사용된다. 관찰값과 추정값의 차이 및 모형의 복합성을 고려하는 AIC가 더 많이 선호된다.


## Paper 2 : 공간 자료를 이용한 대기오염이 순환기계 건강에 미치는 영향 분석
- > Received 22 August 2016, 1st revised 11 September 2016, accepted 12 September 2016
- > 2016, The Korean Society for Quality Management
- > This is an Open Access article distributed under the terms of the Creative Commons Attribution Non-Commercial License (http://creativecommons.org/licenses/by-nc/3.0) which permits unrestricted non-Commercial use, distribution, and reproduction in any medium, provided the original work is properly cited.

### Abstract
- OLS의 한계 극복 위해 GWR 사용
- 지리가중회귀분석을 사용하여 추정된 회귀계수를 K-means 군집분석을 통해 대기오염의 지역적 분포의 특성을 살펴봄
- 지역 탐색을 위한 포아송 분포를 바탕으로 한 우도비(Likelihood Ratio) 검정법, 지리적 가중회귀분석을 소개

### 지리가중회귀분석(Geographically weighted regression)
기본적인 식은 아래와 같다.
$$Y_i = \beta_{0i} + \sum_{k=1}^m \beta_{ki}X_{ki} + \epsilon_i$$
이것의 solution은 위와 같은 방법으로 구해지며, 다음과 같이 표현된다.
$$\hat{\beta}_i = (\hat{\beta_{i0}},\hat{\beta_{i1}},\cdots,\hat{\beta_{im}})^T = (X^T W_i X)^{-1} (X^T W_i Y)$$

여기서 공간가중행렬 $W_i$는 $i$번째 관측값과 다른 모든 관측값을 반영하는 공간행렬로, $i$번째 관측값의 거리에 기초한 가중치 $d_i$를 포함하는 $n \times n$ 대각행렬이다.

$$W_i = 
\begin{bmatrix}
w_{i1} & 0 & 0 & \cdots & 0 \\
0 & w_{i2} & 0 & \cdots & 0 \\
\vdots & \vdots & \vdots & \cdots & \vdots \\
0 & 0 & 0 & \cdots & w_{in} \\
\end{bmatrix}$$

그리고 가중함수는 Gauss kernel을 통해서 계산된다.
$$w_{ij} = \exp [- \frac{1}{2} \times \left(\frac{d_{ij}}{\theta} \right)^2]$$
이 값은 대역폭 $\theta$가 커질수록 동일한 거리에 대한 가중치가 1로 계산되고, 이 경우 OLS와 같은 결과를 지닌다. 반면, 대역폭이 작아지면 가중치는 0으로 계산될 것이다.

#### AIC
- AIC 값을 최소화하는 대역폭을 선택하는 것이 바람직하다.
- AIC는 동일한 종속변수에 대해 상이한 독립변수로 구성된 모형을 비교하는 데 유용 
- 일반적으로 비교되는 두 모형 OLS, GWR에서 AIC 값의 차이가 2 또는 4보다 작은 경우 두 모형은 사실상 차이가 없는 것으로 본다.

#### 자기상관성 측정
- __Moran I 통계량__ : 잔차의 공간적 자기상관성 측정 위해 가장 많이 쓰이는 지표
$$I = \frac{n \sum_{i=1}^n \sum_{j=1}^n w_{ij} (y_i-\bar{y})(y_j-\bar{y})}{\sum_{i=1}^n \sum_{j=1}^n w_{ij} \times \sum_{i=1}^n (y_i-\bar{y})^2}$$
- $n$ : 지역단위 수
- $\bar{y}$ : 종속변수 $y$의 평균
- $w_{ij}$ : $(i,j)$ 지점의 공간가중행렬
Moran I 지수 지역간의 인접성을 나타내는 공간가중행렬과 인접하는 지역들 간의 속성데이터 유사성을 측정하는 것
$$Z = \frac{I - \mathbb{E}[I]}{S_\epsilon (I)}$$
- $\mathbb{E}[I], S_\epsilon(I)$ : 통계량 $I$의 평균과 표준편차
- $Z=1$이다 == 유사한 값 가진 지역들이 인접하는 경향이 강함 
- $Z=-1$이다 == 큰 값과 작은값 가진 지역들이 골고루 인접함
- 이렇듯, 큰 값들과 작은 값들이 공간적으로 밀집해 있는 경우 모두 동일하게 자기상관도가 크게 산출된다.

Moran I 지수의 통계적 유의성 검정을 통해 공간적 자기상관을 판정하여 __공간적 자기상관이 존재한다면__ 지리가중회귀분석으로 모형을 추정한다.

__공간적 자기상관이 없는 것으로 판정되면__ 단순회귀분석으로 모형을 추정하는 것이
가능하다.

---
# Comparison of Ordinary Least Square Regression, Spatial Autoregression, and Geographically Weighted Regression for Modeling Forest Structural Attributes Using a Geographical Information System (GIS)/Remote Sensing (RS) Approach

## Review of Regression Techniques
#### Ordinary Least Square Regression(OLS)
- 생태학적 방법론에서 자주 씀(NDVI, SR ...)
- spatial dependency 존재
- linear models (OLS), generalized additive model(GAM), classification and regression tree (CART), multivariate adaptive regression spline (MARS) and artificial neural network (ANN). 
- No significant difference among these techniques
- MARS and GAM performed marginally better
- Complexity 높을수록 OLS 성능 좋음

#### Spatial Autoregression(SAR) : OLS의 한계
- Spatial autocorrelation : 가까이 위치한 관측치들의 lack of independence
- OLS는 관측치들의 independence를 가정하기 때문에 the presence of spatial autocorrelation in a dataset is troublesome for OLS regression
- This premise has been the foundation for a new regression technique called geographically weighted regression (GWR) __to capture both spatial dependency and spatial non-stationarity in the modeling process.__

#### Geographically Weighted Regression
- GWR is an extended version of traditional OLS regression
- global만 집중하는 OLS에 비해 local reality 반영 위해 GWR 사용

### Theoratical background
#### OLS
$$y_i = \beta_0 + \sum_{j=1}^p X_{ij} \beta_j + \epsilon_i$$
Where
$$\displaystyle{\beta_0 = \text{ Intercept coefficient}\\
\beta_j = \text{ Solpe Coefficient for the $j$th independent variable $X_j$} \\
\epsilon_i = \text{ Random error term with N(0, $\sigma^2I$)} \\
I = n \times n \text{ identity matrix}}$$

In the matrix notation
$$Y = X \beta + \epsilon$$

The least square estimate of $\beta$ is
$$\hat{\beta} = (X^T X)^{-1} X^T y$$

ANOVA can be performed to check whether the regression model is statistically significant or not(F-value and corresponding p-value).

T-test(p-value) for eaach parameter estimates can be perforemd to see whether they are statistically significant or not.

$$T = \frac{\hat{\beta}}{s / \sqrt{s_{xx}}}$$

Where
$$\displaystyle{\hat{\beta} = \frac{s_{xy}}{s_{xx}}\\
s_{xy} = \sum (x-\bar{x})(y-\bar{y}) \\
s_{xx} = \sum (x-\bar{x})^2}$$

Coefficient of determination can be calculated to see how well the model is successful at explaining variability as
$$R^2 = \frac{S_{xy}^2}{S_{xx}S_{yy}}$$

To check normality assumption, __Shairo-Wilk test__ can be performed
$$W = \frac{\left( \sum_{i=1}^n a_i x_{(i)} \right)^2}{\sum_{i=1}^n (x_i - \bar{x})^2}$$
Where
$$\displaystyle x_{(i)} = \text{ Ordered sample values($x_{(l)}$ is the smallest)} \\
\displaystyle a_i = \text{ constants generated from the means, variances and covariances of the order statistics of a sample of size $n$ from a normal distribution.}$$
__Shairo-Wilk test__ tests the null hypothesis that a sample $x_1, \cdots, x_n$ came from a normally distributed population. The test rejects the null hypothesis if $W$ is too small.

Jarque-Bera test can be also performed for testing the normality assumption.
$$JB = \frac{n}{6} \left( S^2 + \frac{K^2}{4}\right)$$
Where
$$\displaystyle S = \text{Skewness} \\
\displaystyle K = \text{Kurtosis} \\
\displaystyle n = \text{number of observations}$$
이는 카이제곱분포를 따르고, 위의 경우과 같은 귀무가설을 테스트한다.

__The Breusch-Pagan test__ on random coefficients and __White test__ on specification robust can be performed to check the presence of spatial heteroscedasticity (i.e. spatial non-stationarity).
- Breusch-Pagan Test : whether the estimated variance of the residuals from a regression depend on the values of the independent variables or not.
  
$$\displaystyle \text{regression : } Y_i = \alpha + \beta X_i + \epsilon_i \\
\displaystyle \text{auxiliary regression : } Z_i^2 = \phi + \delta X_i + \nu_i$$

Where
$$\displaystyle i \in \{1, 2,\cdots, N\} \\
\displaystyle \mathbb{E}(\epsilon_i) = 0 \\
\displaystyle S^2 = \sum \hat{u_i}^2 / N \\
\displaystyle Z_i^2 = \sum \hat{u_i}^2 / S^2$$
The testable hypothesis are expressed as follows:
$$\displaystyle H_0 : \delta = 0 \text{ (homoscedastic error variance)} \\
\displaystyle H_a : \delta != 0 \text{ (homoscedastic error variance)}$$
- $\delta=0$이면, 즉 귀무가설 성립 시 empirical error variance는 상수텀이고, 대립가설이 참이면 empirical error variance는 $X$ variable에 대한 함수라고 해석할 수 있다.
- White : The residuals are computed from the original model and an empirical measure for the error variances is constructed by squaring them.
$$\displaystyle \text{regression : }Y_i = \alpha + \beta_i X + \beta_2 W + \epsilon_i \\
\text{auxiliary regression : } \hat{u_i}^2 = \phi + \delta_1 X_i + \delta_2 W_i + \delta_3 X_2 + \delta_4 W_2 + \delta_5 X_i \times W_i + \nu_i$$
The testable hypotheses are expressed as follows:
$$\displaystyle H_0 : \delta = 0 \text{ (homoscedastic error variance)} \\
H_a : \delta \neq 0 \text{ (homoscedastic error variance)}$$
White test는 등분산성, 이분산성 하에서 least square estimator의 표본분산을 비교한다. 귀무가설이 참이라면, variance에서 발생하는 차이들은 sampling에 의한 오차이지, 근본적 차이에 의한 오차가 아니라고 볼 수 있다.

Spatial autoregression를 보기 위해 __Lagrange Multiplier-Lag statistics__ 와 __Robust Lagrange Multiplier-Lag statistics__ 를 생각해볼 수 있다. 

$$LM_{Lag} = \frac{(e'Wy / s^2)^2}{(WXb')MWX\beta / s^2 + tr(W'W + W^2)}$$
Where
$$\displaystyle  M = I - X(X'X)^{-1}X'M \\
\displaystyle y = \text{vector containing the dependent variable} \\
\displaystyle e = \text{vector of OLS residuals} \\
\displaystyle W = \text{spatial weights matrix} \\
\displaystyle s^2 = e'e / N \text{(ML estimate for residual variance)}\\
\displaystyle b = \text{vector of OLS estimates} $$
The Lagrange Multiplier lag Test($LM_{Lag}$)는 $\chi^2$ distribution with one degree of freedom을 갖는다.

### Spatial Autoregression
Autocorrelation를 regression modelling process에 추가하여 spatial autoregression을 고려해보자. 이는
- additional regressor in the form of spatially lagged dependent variable
- error structure
들을 추가하여 구현가능하다.
$$y = \rho Wy + X\beta + \epsilon_i$$
Where
$$\displaystyle y = \text{$n$ by 1 vector of observations on the dependent variable} \\
\displaystyle W = \text{$n$ by $n$ spatial weights matrix that formalizes} \\
\displaystyle \rho = \text{spatial autoregressive parameter} \\
\displaystyle X = \text{$n$ by $k$ matrix of observations on the exgenous variables with an associated $k$ by 1 regression coefficient vector $\beta$} \\
\displaystyle \epsilon = \text{a vector or random error terms}$$
The log-likelihood for the spatial autoregression can be estimated by
$$\ln L = -\frac{1}{2 \sigma^2} (y-\rho Wy-X\beta)'(y- \rho Wy - X\beta)$$
The least square estimator and variance for spatial autoregression can be estimated by
$$\displaystyle \hat{\beta}_{ML} = (X'X)^{-1} X' (y-\lambda Wy) \\
\displaystyle \hat{\sigma}_{ML} = (e_o - \rho e_L)'(e_o - \rho e_L)/N$$
Where
$$\displaystyle e_o = y-X\hat{\beta}_o \\
\displaystyle e_L = y-X\hat{\beta}_L$$

__Moran's I__ is one the most popular measures of spatial autocorrelation.Similarity between observations for a given variables as a function of spatial distance가 측정된다.
$$I = \frac{\sum_i^n \sum_j^n W_{ij} (x_i-\bar{x})(x_j-\bar{x})}{S^2 \sum_i^n \sum_j^n W_{ij}}$$
- $I>0$ : 특정 거리만큼 떨어진 observation들이 비슷하다고 여겨질 때 나옴
- $I<0$ : 특정 거리만큼 떨어진 observation들이 비슷하지 않다고 여겨질 때 나옴
- $I=0$ : 랜덤하게 + 독립적으로 관측값들이 뿌려져 있음

Spatial autoregression model을 위해서 __Likelihood Ratio Test__ 가 시행될 수 있다. which corresponds to twice the difference between the log likelihood in this model and the log- likelihood in the standard regression model with the same independent variables with l equaling zero. 이는 $\chi^2$ dsitributed with one degree of freedom으로 시행된다.

#### Geographically Weighted Regression
$(u_i, v_i)$ : set of location co-ordinates of $i$-th point over space.

Then, GWR extends global OLS regression framework as

$$y_i = \beta_0 (u_i, v_i) + \sum_{j=1}^p X_{ij}\beta_j (u_i, v_i) + \epsilon_i$$
Where
$$\displaystyle \beta_k(u_i, v_i) = \text{ Continuous function of the location $(u_i, v_i)$ at point $i$} \\
\epsilon_i = \text{ Random error term with $N(0, \sigma^2 I)$}$$

In matrix notation,
$$Y = \beta \bigotimes X + \epsilon$$
Where $\bigotimes$ means componentwise-multiplication. 

The matrix $\beta$ consists of $n$ sets of local parameters, which is given as
$$\beta = 
\begin{bmatrix}
  \beta_0 (u_1, v_1) & \beta_1(u_1, v_1) & \cdots & \beta_k (u_1, v_1) \\
  \beta_0 (u_2, v_2) & \beta_1(u_2, v_2) & \cdots & \beta_k (u_2, v_2) \\
  \cdots & \cdots & \cdots & \cdots \\
  \beta_0 (u_n, v_n) & \beta_1(u_n, v_n) & \cdots & \beta_k (u_n, v_n) \\
\end{bmatrix}$$

GWR estimator of $\beta_i$ is given by
$$\hat{\beta}_i = (X^T W_i X)^{-1} X^T W_i y$$
Where
$$W_i = 
\begin{bmatrix}
  w_{i1} & 0 & \cdots & 0 \\
  0 & w_{i2} & \cdots & 0 \\
  \vdots & \vdots & \cdots & \cdots \\
  0 & 0 & \cdots & w_{in} 
\end{bmatrix}$$

In adoptive kernel, where the regression points are closely spaced, smaller bandwidths are applied than those of when the regression points are widely spaced. The weight of $k$th data point at $i$th regression point is given by
$$\displaystyle w_{ik} = \left[ 1 - \left(\frac{d_{ik}}{h_i}\right)^2\right]^2 \text{ (when } d_{ik} \leq h_i) \\
= 0 \text{ (when } d_{ik} > h_i)$$

GWR의 bandwidth는 smoothing function 기능을 한다.
- high bandwidth : over-smoothed model, producing parameters with too little vairation across space
- low bandwidth : under-smoothed model, greater variation in model parameters over space than what is realistic.

bandwidth value의 선택방법은 3가지가 존재한다.

First : selected based on existing knowledge. With a very large data set, bandwidth selection can be made using the desired percentage of the sample points to save time or otherwise can used all data. 

The second method of bandwidth selection in GWR requires no prior knowledge, and estimates bandwidth through a __cross-validation technique__ which minimizes the squared error as
$$z = \sum_i [y_i - y_{\neq 1}(h)]^2$$
Where
$$y_{\neq 1}(h) = \text{ Fitted value of $y_i$ with observation for location i omitted from the estimation process}$$
This technique is only possible when the regression point locations are the same as the data point locations.

The third method for bandwidth selection in GWR employs a technique which minimizes Akaike Information Criterion (AIC) for fitting the best regression model as
$$AIC_c = 2n \log_e(\hat{\sigma}) + n \log_e(2 \pi) + n \times \frac{n+tr(S)}{n-2-tr(S)}$$
Where
$$\displaystyle n = \text{Sample size} \\
\displaystyle \hat{\sigma} = \text{Estimated standard deviation of the error term} \\
\displaystyle c = \text{subscript for corrected AIC estimate}$$
- lower AIC : reality에 가까운 model 

The aim of a __non-stationarity test__ is to examine whether the local variations as generated by GWR are significantly different over space.(차이가 있어야 GWR 사용한 것이 의미가 있음.)
- First method : `comparing the range of the local parameter estimates with a confidence interval around the OLS estimate of the equivalent parameter`.
  - The parameter is considered to be `nonstationary` if the interquartile range of GWR estimates is greater than ±1 standard
deviation of the same global parameter
- Second method : `Monto Carlo test`, which uses a pseudo-random number generator to relocate the observations across the space.
- Third method : `Leung’s parameter variation test`
  - The F-test for checking improvement of GWR over OLS

$$F = \frac{RSS_0 / \nu_0}{RSS_w / \nu_w}$$
Where
$$\displaystyle  RSS_0 = \text{Residual sum of squares for OLS} \\
\displaystyle RSS_w = \text{Residual sum of squares for GWR} \\
\displaystyle \nu_0 = \text{Degree of freedoms for OLS} \\
\displaystyle \nu_w = \text{Degree of freedoms for GWR}$$

GWR provides four important diagnostics statistics at each point, which helps to understand information locally. 

1. __standardized residuals__
  - `Residual` : difference between the calculated value of $Y$ and the actual observed value of $Y$
  - `Standardized residuals` values greater than ±3 are unusual observations and thus should be examined carefully
  - `Standardized residuals` is calculated as residuals divided by standard error of the residuals.
$$r_i = \frac{e_i}{\sqrt{MS_{ReS0}}} (i \in \{1, 2, \cdots, n\})$$

2. __local variations of the $R^2$ statistics__
- regression point 근처를 잘 반영하고 있는가?
- These values should be interpreted very carefully because the model calibrated at one location may not be suitable to replicate the data at other locations.
- `local` $R^2$ `statistics` are calculated as
$$r_i^2 = \frac{TSS_w - RSS_w}{TSS_w}$$
Where
$$TSS_w = \sum_j W_{ij} (y_i-\bar{y})^2 \text{ (Geographically weighted total sum of squares)}\\
RSS_w = \sum_j w_{ij} (y_i-\bar{y})^2 \text{ (Geographically weighted residual sum of squares)} \\
w_{ij} = \text{ Weight of data point $j$ at regrssion point $i$}$$

3. __leverage values__
- measure the influence of an observation on the model calibration.
- high value : 특정 관측치가 $X$ observation의 중심과 멀다.
- If leverage values exceed $2p/n = \text{(number of variables devided by number of observations)}$, then it is considered as cut off points for leverage. 
- The leverage of an observation at $x_i$ of the $X$ matrix can be written as
$$h_{ii} = x_i (X^TX)^{-1}x_i^T$$

4. __Cook’s Distance__
- another indication of the influence of an observation
- high value : 관측치가 influential하다
- 1보다 크다 == large studentized residual 가진다.
- `Cook's Distance` can be calculated as
$$D_i = \frac{r_i^2}{p} \times \left( \frac{h_{ii}}{1-h_{ii}}\right)$$
Where
$$\displaystyle r_i = \text{Studentized residual}\\
\displaystyle h_{ii} = \text{Leverage} \\
\displaystyle p = \text{number of variables}$$