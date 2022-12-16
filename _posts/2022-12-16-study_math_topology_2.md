---
title:  "[Math] Topology - 2. General Topological Space"
excerpt: "스터디-수학 위상수학 정리 "

categories: [Study, Math]
tags:
  - [위상, 위상수학, 거리, 거리공간, topology, metric, math]

toc: true
toc_sticky: true
 
date: 2022-12-16
last_modified_at: 2022-12-16
math: true
comments : true
mermaid: true
---


집합에 위상을 준다는 것은 무엇일까? 이는 달리 말하면 __어떤 것을 open set 으로 줄 것인가?__ 에 대한 것이다. 예를 들어보면 아래와 같은 것들이 있다.
- __metric topology__ : metric space인 경우, 그냥 open ball로 open set을 정의할 수 있다.
- __discrete topology__ : $\mathcal{T} = P(X)$
- __indiscrete topology__ : $\mathcal{T} = \{\emptyset, X\}$
- __cofinite topology__ : $\mathcal{T} = \{S \subset X : X-S \text{ is finite or }S=\emptyset \}$

여기서 __discrete__ 의 의미는 이산공간, 즉 부분집합만을 open set으로 인정한다는 의미로 사용되는 것으로 이해할 수 있다. __indiscrete topology__ 는 trivial topology라고도 한다.

어떤 open set이 주어질 지는 모르지만, 위상공간이 주어진다는 것은 이제 open set을 생각할 수 있다는 말이 된다. 따라서 다음을 정의할 수 있다.


> ## Definition
>
> 점 $x$를 포함하는 열린집합을 __근방(neighborhood)__ 이라 한다.


> ## Definition
>
> 집합 $A$의 여집합 $A^c$가 열린집합이면 $A$를 __닫힌집합(closed set)__ 이라 한다.


> ## Definition
>
> 집합 $A$에 대하여 이와 서로소인 집합들 중, 가장 큰 열린집합을 __외부(exterior)__ 라 하고, ext$A$로 표기한다.


> ## Definition
>
> 집합 $A$에 대하여 다음 집합
> $$\{x \in X : \text{ for any neighborhood } O \text{ of } x, O \cap A \neq \emptyset \text{ and } O \cap (X-A) \neq \emptyset \} $$
> 을   $A$의  __경계(boundary)__ 라 하고, $\partial A$로 표기한다.


> ## Proposition
>
> $X$는 임의의 집합 $A$로부터 분할이 가능하다. 즉,
> $$ X = \text{int}A \sqcup \text{ext}A \sqcup \partial A$$


> ## Definition
>
> 집합 $A$의 __폐포(closure)__ 는 다음과 같이 정의한다.
> $$ \overline{A} = \text{int}A \sqcup \partial A$$


이로부터 유용한 위상적 정리들을 얻어낼 수 있다.

> ## Theorem
>
> 집합 $A$에 대하여 다음이 성립한다.
> 1. $\text{int}A \subset A \subset \overline{A}$
> 2. $A$ : closed $\iff$ $A = \overline{A}$
> 3. $A$ : open $\iff$ $A=\text{int}A$


> ## Theorem
>
> $f : X \longrightarrow Y$에 대하여 다음은 equivalent.
> 1. $f$ is continuous
> 2. For all open set $U$ in $Y$, $f^{-1}(U)$ : open in $X$
> 3. For all closed set $B$ in $Y$, $f^{-1}{B}$ : closed in $X$
> 4. For all $A \subset X$, $f(\overline{A}) \subset \overline{f(A)}$


> ## Definition
>
> 다음을 만족하는 점 $x_0 \in X$를 __$A$의 극한점(limit point)__ 라고 정의한다. 
> $$\text{for any neighborhood $O$ of $x_0$, }(O-\{x_0\}) \cap A \neq \emptyset $$
> 이들을 모은 집합을 __유도집합(derived set)__ 이라고 정의하고, $A'$으로 표기한다.

그러면 다음이 성립한다.
$$ \overline{A} = A \cup A'$$

이제 위상을 만들어내기 위한 유용한 도구인 기저를 정의해보자.

> ## Definition
>
> 집합 $X$가 주어졌을 때 다음 두 조건을 만족하는 집합 $\mathcal{B} \subset P(X)$를 __기저(basis)__ 라 한다.
> 1. For all $x \in X$, there exists $B \in \mathcal{B}$ satisfying $x \in B$. (i.e. $\bigcup \mathcal{B} = X$)
> 2. For all $B_1, B_2 \in \mathcal{B}$, there exists $B_3 \in \mathcal{B}$ such that
> $$\text{For all $x \in B_1 \cap B_2$ }, \quad x \in B_3 \subset B_1 \cap B_2 $$

위상을 이루는 것은 단연 open set이다. 기저는 open set의 가장 표준적인 형태를 제공한다고 보면 이해하기 쉽다. 기저의 정의 1은 open set property를, 정의 2는 상당히 작은 크기의 open set은 $\mathcal{B}$가 거의 다 갖고 있다고 이해해볼 수 있다.

이제 기저를 통해 위상을 만들어보자.
> ## Proposition
>
> 집합 $X$에 기저 $\mathcal{B}$가 주어졌다고 하자. 그러면 
> $$\begin{aligned}\mathcal{T} &= \{U \in P(X) : \text{For all $x \in U$, there exists $B \in \mathcal{B}$ satisfying $x \in B \subset U$}\} \\
&=\{U \in P(X) : \text{$U$ is union of elements in $\mathcal{B}$} \}\end{aligned}$$
> 은 위상을 이룬다.


당연히 위상에 대한 기저는 유일성이 보장되지 않는다. 다음을 생각해보자.
$$\begin{aligned} \mathcal{B}_{std} &= \{(a,b) \in P(\mathbb{R}) : a, b \in \mathbb{R}\} \\ \mathcal{B}_l &= \{[a, b) \in P(\mathbb{R}) : a, b \in \mathbb{R}\} \end{aligned}$$
이들이 만드는 위상이 있을 것이다. 이를 각각 $\mathcal{T}_{std}$(__standard topology__), $\mathcal{T}_l$(__lower limit topology__)라고 두면 다음이 성립할 것이다.
$$ \mathcal{T}_{std} \subsetneq \mathcal{T}_l$$

> ## Definition
>
> 두 위상 $\mathcal{T}, \mathcal{T}'$ 사이에 $\mathcal{T} \subset \mathcal{T}'$의 관계가 성립하면 $\mathcal{T}'$ __is finer(coarser) than__ 
 $\mathcal{T}$라 한다.

위에서 finer는 섬세하다의 뜻을, coarser는 거칠다의 뜻을 갖고 있다. 

> ## Theorem
>
> 집합 $X$의 두 기저 $\mathcal{B}, \mathcal{B}'$이 이루는 위상을 각각 $\mathcal{T}, \mathcal{T}'$라 하자. 그러면 다음이 성립한다.
> $$ \mathcal{T} \subset \mathcal{T}' \iff \text{For all $B \in \mathcal{B}$ and $x \in B$, there exists $B' \in \mathcal{B}'$ satisfying} $$
> $$ x \in B '\subset B$$


그럼 기저를 구성하기 위한 집합에는 어떤 것들이 있을까? 이를 이해하기 위해 부분기저를 정의한다.

> ## Definition
>
> 집합 $X$가 주어졌을 때
> $$\text{For all $x \in X$, there exists $S \in \mathcal{S}$ satisfying $x \in S$}$$
> 를 만족하는 집합 $\mathcal{S} \subset P(X)$를 __부분기저(subbasis)__ 라 한다.

위에서도 여전히 다음을 만족할 것이다.
$$ \bigcup \mathcal{S} = X$$

> ## Proposition
>
> 집합 $X$에 부분기저 $\mathcal{S}$가 주어졌다고 하자. 그러면 다음 집합
> $$\mathcal{B} = \{U \in P(X) : \text{$U$ is finite intersection of elements in $\mathcal{S}$}\}$$
> 은 $X$의 기저를 이룬다.

이를 통해서 부분위상도 정의가능하다.

> ## Definition
>
> Topological space $X$와 그의 부분집합 $A$가 주어졌을 때, 위상
> $$\mathcal{T}_A = \{A\cap U \in P(A) : \text{$U$ is open in $X$}\}$$
> 는 $A$의 위상이 된다. 이를 __부분위상(subspace topology)__ 또는 __상대위상(relative topology)__ 라 한다.

부분위상은 포함사상
$$i_A : A \hookrightarrow X$$
이 연속함수가 되게 하는 가장 작은(finer or coarser) 위상이다. 앞으로 위상공간의 부분공간을 논하면, 자연스럽게 위와 같은 부분위상을 생각하는 것이 좋다.

> ## Proposition
>
> $\mathcal{B}$를 기저로 하는 위상공간 $X$와 그의 부분집합 $A$가 주어졌다고 하자. 그러면 다음 기저
> $$\mathcal{B}_A = \{A \cap B \in P(A) : B \in \mathcal{B}\} $$
> 로 유도되는 위상은 부분위상이다.

다른 위상도 정의할 수 있다. 비슷하게 두 위상공간 $X, Y$와 그것의 곱집합 $X \times Y$가 주어졌다고 하자. 그러면 사영함수
$$ \pi_1 : X \times Y \longrightarrow X, \qquad \pi_2 : X \times Y \longrightarrow Y$$
는 연속함수임이 자연스럽다. 한편, 열린집합의 교집합은 여전히 열린집합이므로
$$ U \times V = (U \times Y) \cap (X \times V)$$
라고 생각할 수 있고, 이것이 $X \times Y$의 열린집합이 되기를 바란다.

> ## Definition
> 두 위상 $\mathcal{T}, \mathcal{T}'$이 주어진 집합 $X, Y$에 대하여 
> $$\mathcal{B} = \{U \times V \in P(X\times Y) : U \in \mathcal{T}, V \in \mathcal{T}' \} $$
> 은 곱집합 $X \times Y$의 기저가 되고, 이로부터 유도되는 위상을 __곱위상(product topology)__ 라 한다.

위와 비슷하게 의미를 부여해보면, product topology는 projection function이 연속함수가 되도록 하는 가장 coarser한 위상이라고 생각해볼 수 있다.

지금까지 일반적인 위상 공간의 성질에 대해 다루었다. 특히 같은 집합이라도 다른 위상을 주면 다른 성질을 가지곤 했다. 즉 어떤 두 공간이 집합으로서 같은가는 위상의 맥락으로서 큰 의미를 갖지 않고, 다만 두 공간이 위상적으로 같은 성질을 갖는가가 중요할 뿐이다. 따라서 두 위상 공간 사이의 동치 관계(equivalence relation)를 다음과 같이 정의한다.

> ## Definition
>
> 두 위상공간 $X, Y$에 대하여 $X, Y$가 __위상동형(homeomorphic)__ 하다는 것은 아래를 만족하는 두 함수 $f : X \longrightarrow Y$, $g : Y \longrightarrow X$가 존재하는 것을 말한다.
> $$g \circ f = 1_X, \quad f \circ g = 1_Y $$

에를들어 discrete topology가 주어진 두 집합 $\mathbb{N}, \mathbb{Q}$는 위상동형이다.

또한 마찬가지로, 위상이 주어진 공간의 두 원소가 실제로 같은가(등호로 연결이 되는가)는 중요하지 않다. 서로 다른 두 점이라도 위상적 성질이 완벽히 같을 수 있기 때문이며, 두 원소가 위상적으로 구분이 가능한가를 따지는 것이 위상의 맥락이다.

> ## Definition
>
> 위상공간 $X$의 두 원소 $x, y$에 대하여, 서로소인 각 근방을 찾을 수 있는 경우, __$x, y$가 근방으로써 분리 가능하다(separated by neighborhoods)__ 라고 부른다.
> 위처럼 $X$의 임의의 두 원소를 separated y neighborhoods 가능하면, 이를 __하우스도르프(Hausdorff)__ 또는 
> $$ \mathcal{T}_2$$
> 라고 부른다.


우리에게 익숙한 거리 위상은 물론 하우스도르프를 만족한다. 또한 하우스도르프 공간의 부분공간이나 곱공간 등도 하우스도르프 공리를 만족함을 쉽게 확인할 수 있다.

> ## Proposition
>
> In Hausdorff space, singleton set is closed.

하나 이 조건은 하우스도르프 공리의 충분조건은 아니다. 예를 들어 cofinite topology이 주어진 공간에서 한원소집합은 닫힌집합이나 하우스도르프 공간은 아니다.

> ## Definition
>
> 위상공간 $X$의 두 원소 $x, y$에 대하여 서로를 포함하지 않는 각 근방을 그릴 수 있다면, 즉 $y$를 포함하지 않는 $x$의 근방과 $x$를 포함하지 않도록 하는 $y$의 근방이 각각 존재할 때 __두 원소 $x, y$를 분리가능(separated)__ 이라 부른다. 이러한 $X$의 성질을
> $$ \mathcal{T}_1$$
> 이라고 부른다.

> ## Proposition
>
> 다음은 동치이다.
> 1. 위상공간 $X$가 $\mathcal{T}_1$
> 2. Every singleton set in $X$ is closed.

separable보다 더 약한 정의도 존재한다.

> ## Definition
>
> 위상공간 $X$의 두 원소 $x, y$에 대하여 어느 하나를 포함하지 않도록 하는 다른 하나의 근방이 존재하면, 두 원소 __$x, y$를 구별가능하다(distinguishable)__ 고 말한다. 
> 이러한 성질을 만족하는 $X$를 
> $$ \mathcal{T}_0$$
> 이라고 한다.

대부분의 위상은 $\mathcal{T}_0$에서 이루어지는 경우가 많고, 당연하게도 다음이 성립한다.
$$ \mathcal{T}_0 \subset \mathcal{T}_1 $$