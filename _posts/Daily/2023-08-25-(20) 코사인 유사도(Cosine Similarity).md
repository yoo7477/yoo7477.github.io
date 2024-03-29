---
title : "코사인 유사도(Cosine Similarity)"
categories :
- DAILY
tag : [MATH, ML]
toc: true
toc_sticky: true
toc_label : "목록"
author_profile : false
search: true
use_math: true
---
<br/>

# 코사인 유사도(Cosine Similarity)


## 1. 개념  
벡터와 벡터간 유사도를 비교할 때 벡터의 크기보다 벡터의 패턴(방향)이 얼마나 유사한지 측정하는 척도임.

## 2. 사용하는 이유
좌표평면 상에 벡터로 표현된 두 데이터 $\mathbf{a}=(a_1, a_2), \mathbf{b}=(b_1, b_2)$가 아래 그림과 같은 형태라고 할 때 $\mathbf{a}$ 와 $\mathbf{b}$의 패턴(방향)은 유사하지만 벡터 간의 거리는 매우 크게 되어 거리 척도(Euclidean, Manhattan distance 등)를 활용해서는 $\mathbf{a}$와 $\mathbf{b}$가 관계 없다고 나타나기 때문에 개념에서 설명했던 것처럼 두 데이터의 패턴(방향)에 관심 있을 때 활용함.

![정의](../../assets/images/post_images/2023-08-25-(01)/figure1.png){: .align-center  width="30%" height="30%"}

## 3. 측정방법
두 벡터사이의 사잇각($\theta$)을 구해서 $\theta$가 작으면 데이터의 유사도가 높고 $\theta$가 크면 유사도가 낮다고 판단할 수 있음. 사잇각은 벡터의 내적(Inner product)로부터 정의되므로 $\theta$를 직접 계산하기 보다는 벡터의 내적을 이용해 $\theta$의 코사인 값으로 유사도를 측정함.


### 3.1 내적의 성질
a. $\mathbf{a \cdot a}$ = $\parallel\mathbf{a}\parallel^2>=0$, $\mathbf{a \cdot a}$ $\Leftrightarrow$ **a**=0   
b. $a \cdot b = b\cdot a$(교환법칙)  
c. $(a+b)\cdot c = ac+bc$(분배법칙)  
d. $(ka)\cdot b = a\cdot (kb) = k\cdot(ab)$

### 3.2 사잇각 계산
벡터의 내적은 두 벡터가 이루는 사잇각과 관련 있고, 아래 그림에서 피타고라스 정리를 통해 알 수 있음.

![정의](../../assets/images/post_images/2023-08-25-(01)/figure2.png){: .align-center  width="30%" height="30%"}

이를 벡터를 이용해 다시 표현하고, 내적의 성질에 의해 아래와 같은 수식이 나오고
- $\parallel\mathbf{a-b}\parallel^2$ = $\parallel\mathbf{a}\parallel^2$ + $\parallel\mathbf{b}\parallel^2 -2\parallel\mathbf{a}\parallel\parallel\mathbf{b}\parallel\cos(\theta)$ 
- $\parallel\mathbf{a-b}\parallel^2$ = $(\mathbf{a-b})\cdot(\mathbf{a-b})$  = $\mathbf{a}\cdot\mathbf{a}$ - $\mathbf{a}\cdot\mathbf{b}$ - $\mathbf{b}\cdot\mathbf{a}$ + $\mathbf{b}\cdot\mathbf{b}$ = $\parallel\mathbf{a}^2\parallel$ +$\parallel\mathbf{b}^2\parallel$ $-2(\mathbf{a}\cdot\mathbf{b})$  

두 식을 비교하면 다음을 얻을 수 있음.  
<center>

$\cos(\theta)$ = $\frac{\mathbf{a\cdot b}}{\parallel\mathbf{a}\parallel\mathbf{b}\parallel}$
</center>

## 4. 코사인 유사도 계산 
두 데이터 $\mathbf{a}=(a_1, a_2)$와 $\mathbf{b}=(b_1, b_2)$의 코사인 유사도는   
 <center> 
 cos$\theta$ = $\frac{\mathbf{a}\cdot {\mathbf{b}}}{\parallel\mathbf{a}\parallel \parallel \mathbf{b}\parallel}$ = $\frac{\sum(\mathbf{ab})}{\sqrt{\sum\mathbf{a_i^2}} \cdot \sqrt{\sum\mathbf{b_i^2}}}$   
 </center> 

$n$차원 공간 $\mathbb{R}^n$의 두 벡터 $\mathbf{a}=(a_1, a_2,\cdots,a_n),\mathbf{b}=(b_1,b_2,\cdots,b_n)$에 대해서도 동일하게 성립된다. 

## 5. 생각해보기
### Q1. 실제 사용하는 경우와 이유는?
a. 텍스트로 된 문서의 유사도를 비교하는데 가장 많이 사용됨. 이유는 문서를 피처 벡터화하면 차원이 매우 많은 희소행렬이 되기 쉬움. 이러한 희소행렬 기반에서 문서와 문서 벡터 간의 크기에 기반한 유사도 지표는 정확도가 떨어지기 쉬움  
b. 추천시스템의 Neighborhood 모형. 이는 Memory-based CF라고도 하는데 해당 사용자와 유사한 사용자를 찾는 방법인 사용자 기반 CF와 특정 상품과 유사한 평점 정보를 가지는 상품들로 해당 상품의 빈 데이터를 예측하는 상품 기반 CF로 구분됨.  
c. 시계열 데이터에서의 유사패턴탐지(DTW, Dynamic Time Warping, 동적시간워핑). 예를 들어 IoT 센서에서 시간마다 생성되는 데이터를 비교하여, 현재 데이트 허름과 과거의 어떤 흐름과 매칭 되는데 체크할 수 있음.(이외 주식 데이터, 음성 데이터 등)  
### Q2. 방향과 크기를 같이 보는 방법은 없을까?
하나의 벡터를 또 다른 벡터에 정사영한 길이를 이용하여 구할 수 있음. 개념은 알겠는데 구현을 어떻게 해야할지 와닿지가 않아서 추후 학습으로 보류 

## 6. 예제로 알아보기
### a. 문서의 유사도 비교 
```python
txt1 = "사과 바나나 딸기 포도"
txt2 = "포도 포도 토마토 사과 딸기"

Counter(txt1.split(" "))
# Counter({'사과': 1, '바나나': 1, '딸기': 1, '포도': 1})
Counter(txt2.split(" "))
# Counter({'포도': 2, '토마토': 1, '사과': 1, '딸기': 1})
```

|   |$\mathbf{a}$|$\mathbf{b}$|$\mathbf{a*b}$|
|---|---|---|---|
|사과|1|1|1|
|바나나|1|0|0|
|딸기|1|1|1|
|포도|1|2|2|
|토마토|0|1|0|

- $\mathbf{a*b} = 1+0+1+2+0 = 4$  
- $\mathbf{\parallel a\parallel*\parallel b\parallel}$=$(\sqrt{\sum\mathbf{a}^2})*(\sqrt{\sum\mathbf{b}^2})$=$\sqrt{1^2+1^2+1^2+1^2+0^2}*\sqrt{1^2+0^2+1^2+2^2+1^2}$=$\sqrt{4}*\sqrt{7}$=$\sqrt{28}$  
코사인 유사도 $=4/\sqrt{28} = 0.75592894$

### b. 추천시스템의 Neighborhood 모형
변수에 유저와 상품의 점수가 들어간다는 점 외에는 a와 동일함 
### c. DTW
```python
import pyupbit
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

tmp = pyupbit.get_ohlcv('KRW-BTC', count=int(2549), interval="minute240")
plt.figure(figsize=(20,10))
plt.subplot(121)
tmp.close.plot()

plt.subplot(122)
tmp.close[50:70].plot()

```

    
![정의](../../assets/images/post_images/2023-08-25-(01)/output_0_1.png){: .align-center  width="80%" height="80%" title="gd"} 


```python

base = tmp.close[50:70]
base = (base - base.min()) / (base.max() - base.min())

window_size = len(base)

moving_cnt = len(tmp) - window_size - 1

def cosine_similarity(x, y):
    return np.dot(x, y)/(np.sqrt(np.dot(x, x))*np.sqrt(np.dot(y, y)))

# 코사인 유사도를 계산하여 저장해줄 리스트를 생성합니다
sim_list = []

for i in range(moving_cnt):
    # i 번째 인덱스 부터 i+window_size 만큼의 범위를 가져와 target 변수에 대입합니다
    target = tmp.close.iloc[i:i+window_size]

    # base와 마찬가지로 정규화를 적용하여 스케일을 맞춰 줍니다
    target = (target - target.min()) / (target.max() - target.min())

    # 코사인 유사도를 계산합니다
    cos_similarity = cosine_similarity(base, target)

    # 계산된 코사인 유사도를 추가합니다
    sim_list.append(cos_similarity)

pd.Series(sim_list).sort_values(ascending=False).head(20)

```




    50      1.000000
    1059    0.993667
    775     0.992528
    774     0.991690
    773     0.991257
    1070    0.990961
    776     0.990825
    1751    0.990255
    49      0.990040
    1062    0.989791
    1061    0.988604
    1064    0.988573
    51      0.988515
    1063    0.987810
    1069    0.987597
    772     0.987374
    1060    0.987211
    1752    0.986763
    1068    0.986628
    1065    0.986006
    dtype: float64


## 참고
[ED vs Cosine](https://cmry.github.io/notes/euclidean-v-cosine)  
[Cosine-문서 예제](https://velog.io/@crescent702/cos-similarity)  
[Cosine-시계열 예제](https://eunhye-zz.tistory.com/27)  
[Cosine-wiki](https://en.wikipedia.org/wiki/Cosine_similarity#Soft_cosine_measure)  
[DTW](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=rkdwnsdud555&logNo=221155705904)  
[추천시스템](https://datascienceschool.net/03%20machine%20learning/07.01%20%EC%B6%94%EC%B2%9C%20%EC%8B%9C%EC%8A%A4%ED%85%9C.html)  
[파이썬 머신러닝 완벽가이드, 권철민, 550p]()