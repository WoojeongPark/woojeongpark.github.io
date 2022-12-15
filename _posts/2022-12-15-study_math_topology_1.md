---
title:  "[Math] Topology - 1. Metric space와 Generalization"
excerpt: "스터디-수학 위상수학 정리 "

categories: [Study, Math]
tags:
  - [위상, 위상수학, 거리, 거리공간, topology, metric, math]

toc: true
toc_sticky: true
 
date: 2022-12-15
last_modified_at: 2022-12-15
math: true
comments : true
mermaid: true
---

# 1. 거리공간(Metric Space)

$\mathbb{R}^n$에서는 거리가 자연스럽게 정의된다.
$X = (a_1, a_2, \cdots, a_n), Y = (b_1, b_2, \cdots, b_n) \in \mathbb{R}^n$에 대하여 __내적(inner product)__ 는 다음과 같이 정의된다.
$$\langle X, Y \rangle = \sum_{i=1}^n a_i b_i$$

__크기(norm)__ 도 자연스럽게 주어진다.
$$\| X\| = \sqrt{\langle X, X\rangle}$$

크기가 주어지면 __거리(distance)__ 도 정의할 수 있다.
$$d(X, Y) = \| X - Y \|$$

거리함수는 일반적으로 아래 3가지 공리를 만족하는 함수를 말한다.
> ## Definition
> ---
> 아래의 3가지 공리를 만족하는 함수를 __거리함수(distance function)__ 이라하며, 이 함수가 정의된 공간을 __거리공간(metric space)__ 라 한다.
> 1. $d(X,Y) \geq 0$ and $d(X,Y)=0$ iff $X=Y$ <br>
> 2. $d(X,Y) = d(Y,X)$ <br>
> 3. $d(X,Y) \geq d(X,Z) + d(Z, Y)$

이제 일반적인 거리공간으로부터 시작하여 열린집합을 정의해보자. 이를 위해서 다음을 정의한다.

> ## Definition
>
> 거리공간 $X$가 주어졌을 때, $p \in X$, $r>0$에 대하여 <br>
> $$B_r(p) = \{x \in X : d(x,p) < r \} $$ <br>
> 을 __$p$를 중심으로 하고 반지름이 $r$인 열린 공(open ball)__ 이라 한다.


> ## Definition
>
> 거리공간 $X$가 주어졌을 때, <br>
> $$\forall x \in U, \quad \exists \delta>0 \quad \text{such that} \quad B_\delta(x) \subset U$$ <br>
> 를 만족하는 $U \subset X$를 __열린집합(open set)__ 이라 한다.

이는 다음을 만족한다.
> ## Proposition
>
> 열린 공은 열린집합이다.


> ## Proposition
>
> 거리공간 $X$가 주어졌을 때 다음 세 가지 조건을 만족한다.
> 1. 공집합과 $X$는 열린집합이다.
> 2. arbitrary union of open sets은 open이다.
> 3. finite intersection of open sets은 open이다.

> ### Proof
> (1) : trivial <br>
> (2) 
> family of open sets $\{U_\alpha\}_{\alpha \in \mathcal{A}}$ 와 이것의 원소 $x \in \underset{\alpha \in \mathcal{A}}{\bigcup}U_\alpha$ 에 대해 $x$를 포함하는 열린집합 $U_\beta$ 를 하나 잡을 수 있다. 그러면 열린집합의 정의에 의해<br>
> $$B_\delta(x) \subset U_\beta \subset \underset{\alpha \in \mathcal{A}}{\bigcup}U_\alpha$$<br>
> 를 만족하는 $B_\delta(x)$가 존재하므로 열린집합이다. <br>
> (3) family of finite open sets들로부터 이들 안에 들어가는 open ball들을 잡고, 새로운 open ball을 minimum radius를 갖도록 정의하면 이는 finite intersection of open sets에 속한다. $\blacksquare$.


__Note__
- open set들의 무한 개의 intersection은 open을 유지할 수 없다.
- 예) $$U_n = \left(-\frac{1}{n}, \frac{1}{n} \right) (n \in \mathbb{N})$$

이제 위상공간을 정의하자.
> ## Definition
>
> 공간 $X$가 주어졌다고 하자. 다음 세 가지 조건
> 1. $\emptyset, X \in \mathcal{T}$
> 2. For all family of sets $\{U_\alpha\}_{\alpha \in \mathcal{A}}$ where $U_\alpha \in \mathcal{T}$, 
> $$\underset{\alpha \in \mathcal{A}}{\bigcup}U_\alpha \in \mathcal{T}$$
> 3. For all family of __finite__ sets $\{U_i\}_{i \in \mathcal{I}}$ where $U_i \in \mathcal{T}$, 
> $$\underset{i \in \mathcal{I}}{\bigcap}U_i \in \mathcal{T}$$
> 을 만족하는 집합 $\mathcal{T} \subset P(X)$를 __위상(topology)__ 이라고 하며, 위상이 정의된 공간을 __위상공간(topological space)__ 라고 부른다.

이제 해석개론에서와는 다른 방식으로 연속함수를 정의해볼 수 있다. 해석개론에서는 오로지 `거리공간`에서만 다루는 반면, 위상공간에서는 그와 독립적이므로 새로운 정의를 해볼 수 있다.

> ## Lemma
>
> 함수 $f : X \Longrightarrow Y$와 $A\subset B, B\subset Y$가 주어졌다고 하자. 다음 세 명제는 equivalent.
> 1. $x \in A \implies f(x) \in B$
> 2. $f(A) \subset B$
> 3. $A \subset f^{-1}(B)$

이러한 특징을 이용하면 연속함수를 다시 정의해볼 수 있다.

> ## Definition
>
> 함수 $f : X \Longrightarrow Y$와 $x_0 \in X$가 주어졌을 때, __$f$가 점 $x_0$에서 연속__ 이라 함은 $f(x_0)$를 포함하는 $Y$의 열린집합 $V$에 대하여 $f^{-1}(V)$가 $x_0$를 포함하는 어떤 열린집합을 포함하는 경우를 말한다. 정의역의 모든 점에서 연속인 함수를 __연속함수__ 라고 한다.