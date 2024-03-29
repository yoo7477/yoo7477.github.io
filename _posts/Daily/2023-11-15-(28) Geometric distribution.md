---
title : "[Statistics] 기하분포(Geometric Distribution)"
categories :
- DAILY
tag : [Statistics]
toc: true
toc_sticky: true
toc_label : "목록"
author_profile : false
search: true
use_math: true
---
<br/>

# [Statistics] 기하분포(Geometric Distribution)


## 1. 개념
기하분포는 베르누이 시행을 성공할 때까지의 실패 or 시행 횟수에 대한 분포를 의미함. 기존 성공횟수에 관심을 둔 분포들과 다르게 실패 또는 시행 횟수에 관심이 있다는 것이 차이점임. 또한, 실패에 중점을 두냐 횟수에 중점을 두느냐에 따라 확률질량함수도 달라짐. 

## 2. 내용
### 2.1 확률질량함수
성공확률이 p인 베르누이 시행에 대해, k번 시행 후 첫 번째 성공을 얻을 확률은 
$$ P(X=k)=f(k;p)= (1-p)^{k-1}p \qquad k=1,2,3,\cdots$$
또한, 첫 번째 성공까지 시행한 실패의 횟수를 나타내면
$$ P(X=k)=f(k;p)= (1-p)^{k}p \qquad k=0,1,2,\cdots$$
초항이 p이며 공비가 (1-p)인 등비수열(Geometric progression)이됨. 그래서 기하분포라는 이름을 얻었다고 함.

### 2.2 평균, 분산, 최빈값
실패한 횟수와 관련된 기댓값은 
$$E(X)=(1-p)/p$$
시행 횟수와 관련된 기댓값은
$$E(X)=1/p$$
분산은
$$Var(X)=(1-p)/p^2$$

## 3. 예제
- 성능이 매우 안좋은 스팸 분류기의 스팸 분류 확률이 0.1이라고 할 때, 5번째 메일에서 스팸을 스팸이라고 분류할 확률은?

  시행한 실패의 횟수는 4번이고, 이는 5번 시행 후 첫 번째 성공을 얻을 확률이라는 말과 동일함. 따라서 
  $$p(5번 시행 후 첫 번째 성공을 얻을 확률) = (1-0.1)^{5-1}0.1 = 0.06561$$
- 그럼 위와 동일한 조건에서 2번째 내에 스팸을 스팸이라고 분류할 확률은?
  $$p(2번 이내에 스팸을 분류할 확률)=p(한 번에 분류할 확률)+p(두 번만에 분류할 확률)=(1-0.1)^{1-1}0.1 + (1-0.1)^{2-1}0.1 = 0.19$$
  
## 참고


  