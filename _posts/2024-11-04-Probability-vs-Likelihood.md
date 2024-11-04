---
layout: single
title: Probability vs Likelihood
category: Mathmatics
tag: [Probability and Statistics]
toc: true
math_use: true

---

## Probability vs Likelihood

---

논문을 읽다 보거나 통계학을 공부하다 보면 Probability 랑 Likelihood가 나옵니다.

Probability의 경우 우리가 중고등학교 때 배운 확률과 통계와 같이  Probability의 사전적 정의는 확률입니다.

즉 어떤 사건이 일어날 확률(가능성) 혹은 어떤 데이터나 혹은 변수를 주었을 때 해당 변수 혹은 데이터가 특정 distribution에 속할 확률(가능성) 입니다.

  

Likelihood의 사전적 정의는 가능도, 가능성 입니다.

???: ~~ㅅㅂ~~ 확률도 어떤 사건이 발생할 가능성 아님? 

맞습니다.  확률이라는 단어의 정의 자체가 어떤 사건이 발생할 확률이죠.  

그리고 Likelihood의 정의도 어떤 사건이 발생할 가능성이라고 해석이 가능합니다.

???:그러면 왜 두 단어가 같은 의미, 정의를 하고 있는데 두 단어를 구분하고 나누는거임?   같은 뜻 아님?

사전적 정의는 같으나 Likelihood와 Probability는 전혀 다른 관점을 가지고 있는 확률입니다.

앞서 설명을 했듯이, Probability의 경우 어떤 데이터나 혹은 변수를 주었을 때 데이터가 특정 distribution에 속할 확률입니다. 

여기서 중요한 것은 특정 distribution입니다. 분포가 특정 되었다는 것은 우리가 해당 분포를 알고 있다는 것이며, 분포가 고정되어 있다는 뜻 입니다.

그리고 이는 이러한 고정된 distribution에서 어떤 데이터나 변수가 주어져 있을 때  해당 데이터가 이 고정된 distribution에 속할 확률 즉 가능성을 얘기할 때 우리는 probability를 사용합니다.

그럼 Likelihood의 경우 어떨 때 사용할까요?

Likelihood는 Probability와 다르게 어떤 distribution을 주었을 때 해당 distribution에  특정 변수나 혹은 데이터가 있을 가능성 혹은 특정 사건이 발생할 가능성 입니다.

???:도대체 뭐가 다른거냐? 결국에는 어떠한 사건이나 변수가 있을 가능성이 아니냐?

여기서 제가 빨간색으로 글씨를 칠한 이유가 있습니다.

 바로 probability의 경우 distribution이 고정되어 있고 사건이 변화한다는 것이며, likelihood는 사건이 고정되어 있고 distribution이 변화한다는 점 입니다.

 

이렇게 말로만 사실 표현을 하고 설명하면 잘 이해가 되지 않으실 겁니다. 그래서 간단한 예제를 들어 보도록 하겠습니다.

만약 우리가 1~50 사이의 숫자가 적힌 로또를 뽑았을 때 해당 숫자가 10~20사이일 확률은 다음 그림과 같이 표현을 할 수 있습니다.

  

<p align="center"><img src="https://github.com/user-attachments/assets/0f4b396b-4dff-4640-8ef8-9246a92b8ebd" width="65%" height="65%"></p>

[사진 출처:[https://jjangjjong.tistory.com/41](https://jjangjjong.tistory.com/41)]

이런 경우 x1은 10의 값을 가지게 되겠고, x2는 20의 값을 가지게 되겠지요.

이와 같이 probability는 정해져 있는 distribution에서 정해지지 않은 variable이 고정되어 있는 distribution에 속해 있을 가능성은? 이라고 해석을 할 때 사용이 됩니다.

그럼 Likelihood는 어떨 때 사용할까요?

반대로 고정되어 있는 특정 variable이 어떤 distribution에 속할 가능성 혹은 특정 사건이 발생할 가능성이라고 이해하시면 됩니다.

만약 우리가 관점을 살짝 다르게 본다면 정해져 있지 않은 어떤 distribution이 정해진 특정 variable의 distribution을 얼마나 잘 표현했냐 혹은 어떤 distribution이 특정 variable의 distribution과 가장 유사할 가능성으로도  볼 수 있습니다.

<p align="center"><img src="https://github.com/user-attachments/assets/d0393845-8992-4505-a52c-67e650d7d2d7" width="65%" height="65%"></p>

[사진 출처:[공돌이의 수학정리 노트](https://angeloyeo.github.io/2020/07/17/MLE.html)]

공돌이의 수학정리트 블로그에서 가져 온 사진 입니다.

이 블로그에 가시면 더욱 시각적인 예제를 볼 수 있으셔서 좀 더 이해하기가 쉬우실 겁니다.

먼저 x=[1,4,5,6,9]가 있을 때 이 특정 변수 x의 분산을 가장 잘 표현한 distribution은 어떤 distribution일까요?

당연히 모두가 주황색 곡선이라고 생각할거에요.

왜냐? 주황색 곡선에 해당 변수 x가 더 많이 분포하고 있기 때문이죠.

그리고 이는 주황색 곡선이 좀 더 변수 x의 distribution을 더 잘 표현하고 있다고 볼 수도 있습니다.

그렇기 때문에 likelihood는 어떠한 distribution이 주어졌을 때 해당 distribution이 특정 변수의 distribution을 얼마나 잘 표현했냐? 혹은 해당 distribution이 특정 distribution과 유사할 가능성으로 볼 수 있는겁니다.

그럼 이번에는 likelihood function에 대해 알아보도록 하겠습니다.  

그리고 이러한 Likelihood는 아래의 수식과 같이 표현 할 수 있습니다.

<p align="center"><img src="https://github.com/user-attachments/assets/b284d026-7fe2-40fb-824f-da179a258224" width="65%" height="65%"></p>

<p align="center"><img src="https://github.com/user-attachments/assets/5764910e-2de7-46b0-98ce-1af8bc71cf97" width="65%" height="65%"></p>

<p align="center"><img src="https://github.com/user-attachments/assets/404677a0-3c1c-40fe-af78-3e184c45c25a" width="65%" height="65%"></p>

<p align="center"><img src="https://github.com/user-attachments/assets/a0beafb5-29d9-4d75-ab79-ca5409872590" width="65%" height="65%"></p>

수식들을 한번 간단하게 설명을 드리고 가겠습니다.

저는 인공지능을 공부하고 있고, 이 글을 보시는 분들도 아마도 인공지능을 공부하시는 분들인 것 같아, 예시를 머신러닝 관련으로 들어보도록 하겠습니다.        

$$
\theta는\ parameter\ x_i는\ i번째 데이터\ X는 데이터 셋 전체\ \\  \mu는\ 평균\   \sigma는\ 분산을\ 의미합니다. 
$$

그럼 해당 수식은 데이터 셋 X가  parameter에 속할 확률 즉 평균이 μ이고, 분산이 σ인 Normal(Gaussian) distribution에 속할 확률을 의미 합니다. 

그리고 이는 해당 distribution이 데이터 셋 X 를 나타낼 확률(가능성)을 의미합니다.

## Log-Likelihood

---

마지막으로 Log-Likelihood에 대해 알아보도록 하겠습니다.

Likelihood의 풀이 과정을 위에서 다루었는데, 이와 같이 Likelihood후드 수식은 exponential function

(지수 함수)를 곱하는 형태로 이루어져 있기 때문에 아래의 수식과 같이 표현 할 수 있습니다. 

<p align="center"><img src="https://github.com/user-attachments/assets/fb734d4a-7eaf-4f56-a988-0c2203f048f4" width="65%" height="65%"></p>

이렇게 Log함수를 취하는 이유는 지수 함수로 구성 되어 있기 때문에 Log함수를 취하게 된다면 곱셈 연산이 훨씬 쉬어지기 때문에 Log함수를 취해서 Log-Likelihood 형태로 구성하여 계산을 진행하는 것 입니다.

이렇게 Likelihood에 대해 설명을 마치도록 하겠습니다.

[MLE(Maximum Likelihood Estimate)](https://www.notion.so/MLE-Maximum-Likelihood-Estimate-134ec2bf4322808ca67cea2a95b996a3?pvs=21)
