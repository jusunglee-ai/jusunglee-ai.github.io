---
layout: single
title: MLE(Maximum Likelihood Estimate)
category: Mathmatics
tag: [Probability and Statistics]
toc: true
math_use: true

---

## Likelihood정리

---

이번에는 MLE에 대해서 알아보도록 하겠습니다.

 MLE란? Maximum Likelihood Estimate의 약자로 이를 해석하자면 Likelihood의 최대 값을 보고 Estimate 즉, 추정하거나 예측 한다는 의미 입니다.
Likelihood에 대한 정리는 제 블로그에 있으니 해당 링크로 가시면 보실 수 있습니다.
[Probability vs Likelihood](https://jusunglee-ai.github.io/mathmatics/Probability-vs-Likelihood/)
 

혁펜하임님의 Easy! 딥러닝 영상을 보신다면 좀 더 이해가 수월 하실거라고 생각 됩니다.

[링크:[혁펜 하임의 Easy! 딥러닝](https://www.youtube.com/watch?v=M6Hf6R8byvM)]

혁펜하임님께서 말씀하신 부분 중에 가장 영감이 깊었던 부분은 “인공 신경망은 MLE이다.” 라는 부분 입니다.

저도 요즘에 논문을 읽으면서 likelihood가 계속해서 나오고 이걸 쓴 이유는 ~~이런 장점이 있어서다. 라고 적혀있었고 해당 논문을 읽으면서 든 생각이 ~~이런 장점이 있는거는 알겠다.

근데 왜 Likelihood를 썻을 때 이러한 장점이 생기는거지? , 도대체 Likelihood가 어떤 특성이 있길레 그리고 어떤 현상을 수학적으로 표현을 하였기에 이런 특성을 가지는 걸까? 라고 생각이 들어 깊게 공부하다 보니 혁펜하임님이 왜 인공 신경망은 MLE라는지 알 거 같습니다.

그럼 MLE를 설명하기 전에 Likelihood를 간단하게 정리하고 가겠습니다.

Likelihood는 어떤 정해지지 않은 distribution이 있다면, 정해진 variable의 distribution을 해당 distribution이 잘 표현 했을 확률(가능성) 혹은 어떤 distribution에 정해진 variable이 속해 있을 확률 입니다.

<p align="center"><img src="https://github.com/user-attachments/assets/6a669e10-3f9c-42c6-ada4-b829eda2254c" width="65%" height="65%"></p>

[사진 출처:[공돌이의 수학정리 노트](https://angeloyeo.github.io/2020/07/17/MLE.html)]

위의 그림과 같이 정해져 있는 편수 x를 잘 표현한 곡선은 주황색 곡선과 파란색 곡선 중에서 어떤 거일까요?

바로 주황색 곡선이죠 왜냐하면 주황색 곡선이 변수 x의 distribution을 좀 더 잘 표현했을 확률이 높기도 하며, 주황색 곡선이 파란색 곡선보다 좀 더 변수 x가 포함 되어 있을 확률이 높기 때문이죠.

그럼 우리는 이 likelihood를 이용해서 무엇을 예측하고 왜 likelihood의 maximum값을 궁금해 할까요?

그리고 왜 이거를 딥러닝에서 많이 쓰는 걸까요?

## MLE(Maximum Likelihood Estimate)

---

우리는 앞에서 Likelihood는 확률이라고 했습니다. distribution이 아니고요.

그럼 Maximum Likelihood는 가장 높은 확률 값이겠죠.

그럼 likelihood를 통해서 그냥 likelihood 값이 높은 distribution만 찾으면 되는거 아니냐?라고 생각이 드실겁니다.

맞습니다. 그걸 위해서 Maximum Likelihood를 찾는 겁니다.

위의 에시 그림과 같이, 파랑색 곡선이나 주황색 곡선이나 둘 다 Likelihood값을 갖습니다.

근데 우리가 알고자 하는 건 어떤 곡선이 Likelihood 값을 가지는 거냐? 하는게 아니라 어떤 곡선이 우리가 가지고 있는 변수의 distribution을 더 잘 나타내었느냐 혹은 더 잘 나타냈을 확률을 가지는 걸까? 입니다.

그럼 이를 구분하기 위해서는 Likelihood값을 최대로 갖는 distribution을 찾으면 해당distribution이 우리가 알고 있는 변수의 distribution을 가장 잘 표현할 확률이 높다는 것이기 때문에 Maximum Likelihood값을 구한다는 것은 Likelihood 값을 최대로 갖는 distribution을 구하는 것이다. 라는 의미 입니다.

그럼 어떻게 Maximum Likelihood 값을 찾을까?

우리가 Maximum Likelihood 값을 찾기 위해서는 Likelihood 값을 최대로 갖는 distribution을 구하는 것이기 때문에 이 Likelihood 값을 최대로 갖는 distribution의 parameter 값, 즉 이 distribution의 variance와 mean을 구하면 된다는 것 입니다.

이 variance와 mean을 구하는 방법은 그냥 variance와 mean에 대해 각각 편미분을진행하면 된다는 것 입니다.

Likelihood 수식은 다음과 같습니다.

 

<p align="center"><img src="https://github.com/user-attachments/assets/c7fcea4c-535f-47e4-a763-7ddcc3e1c601" width="65%" height="65%"></p>

<p align="center"><img src="https://github.com/user-attachments/assets/2a8e46f3-c4aa-42ed-81e3-f0be4129d017" width="65%" height="65%"></p>

그리고 해당 수식을 μ에 대해 편미분 하게 된다면 Likelihood를 최대 값으로 만들어주는 분산을 구할 수 있습니다.

<p align="center"><img src="https://github.com/user-attachments/assets/909db14a-c574-4c1d-9282-e263a806c152" width="65%" height="65%"></p>

Likelihood를 최대 값으로 만들어 주는 모분산은 다음과 같이 정의가 됩니다.

<p align="center"><img src="https://github.com/user-attachments/assets/eea62539-fa2a-4990-a194-a6dee6af8c81" width="65%" height="65%"></p>

다음은 해당 수식을 σ에 대해 편미분 하게 된다면 Likelihood를 최대 값으로 만들어주는 분산을 구할 수 있습니다. 

<p align="center"><img src="https://github.com/user-attachments/assets/87cb7204-6b18-4740-9174-e7e496735dcf" width="65%" height="65%"></p>

Likelihood를 최대 값으로 만들어 주는 모 표준편차는 다음과 같이 정의가 됩니다.

<p align="center"><img src="https://github.com/user-attachments/assets/bcbed5b8-ab9d-40b9-a209-d57215758d26" width="65%" height="65%"></p>

이렇게 보면서, 느낀게 우리가 모분산, 모평균을 구하는 것 그리고 이에 대한 정의의 뿌리가 결국에는Likelihood인게 아닐까 싶습니다.

또한 이러한 수식을 보면서 생각이 드는 것은 결국에는 딥러닝이란, 확률과 통계의 집합체가 아닐까? 라는 생각도 동시에 드네요.

이렇게 MSE(Maximum Likelihood Estimate)에 대해 마치도록 하겠습니다.

아래는 그냥 MSE를 보면서 왜 딥러닝이 확률과 통계의 집합체라고 생각을 하고 생각이 든건지에 대한 제 개인적인 생각과 의견을 적어 보려고 합니다.

## 왜? 딥러닝은 확률과 통계의 집합체일까?

---

MSE를 공부하면서 느낀게, 혁펜하임님 강의를 봐서도 있지만 결국에는 우리가 정답을 생각하는 방식이나 딥러닝이 정답을 생각하는 방식이 어떠한 확신이 있어서라기 보다는 우리가 가지고 있는 정보 혹은 근거를 가지고 이 답이 정답일 확률이 더 높기 때문에 이러한 정답을 결과로 내놓는게 아닐까 싶습니다.

그리고 그러한 과정이 MSE이고요.

대표적인 예시로 x라는 variable이 단순히 숫자 값이 아니라 오늘 내가 하루 동안 커피를 마신 잔의 개수이고, 뒤에 있는 분포 distribution이 아니라 내가 오늘 잠을 몇 시간이나 잘까? 혹은 잠을 잘 잘 수 있을까? 라는 사건이라면, 결국에는 MSE는 내가 오늘 하루 동안 커피를 마신 잔의 개수를 기반으로 내가 오늘 잠을 몇 시간이나 잘까 혹은 잠을 잘 잘 수 있을까?에 대한 확률을 구하고 확률이 높은 사건을 기준으로 판단하여 몇 시간을 잔다 혹은 잠을 잘 잔다라고 판단하지 않을까 싶습니다.

이러한 과정에서 딥러닝의 훈련과정을 생각해 본다면,

모델이 예측한 결과 값이 실제 값과 많이 다르게 되어 확률이 낮아진다→모델이 해당 데이터의 분포에 대한 분포를 잘 만들지 못했다 즉, MSE값이 낮다는 의미이며 확률을 높이기 위해서는 MSE값을 더 높게 가지는 parameter를 수정해서 구함으로써, 모델 성능을 올리는 과정이라고 생각할 수 있다고 생각이 듭니다.

그리고 혁펜하임님께서는 이러한 과정을 거치도록 해주는 함수가 Loss function이라고 합니다.

저도 그 말씀을 왜 하신지 이해가 됩니다.

왜냐하면 결국에는 parameter 수정을 통해 데이터를 좀 더 잘 표현하는 distribution을 만드는 과정이 필요하고 이 과정을 통해서 조금이라도 더 MSE값이 더 큰 값이 나오도록 해야 하기 때문이죠.

공부를 하면 할수록 딥러닝이 재밌고 이렇게 분석하고 스스로 생각하고 깊게 고민하는 재미가 있네요. 

예전에는 그냥 컴퓨터가 단순히 학습하다 보니 이렇게 됬네? 이 함수를 쓰면 더 잘된다고 하네? 이걸 쓰니까 더 컴퓨터가 학습을 잘하네? 정도로만 생각을 했었습니다.

또한, 왜 ? 이 함수를 쓰면 더 잘되고, 어떻게? 컴퓨터가 학습을 해서 문제를 푸는거고, 왜? 이걸 쓰니까 더 컴퓨터가 잘하는 걸까? 라는 생각을 해본 적이 없었습니다.

그런데, 요즘 들어 이런 생각을 하고 이거를 고민하고 정답을 찾아가니까 연구하고 공부하는게 더욱 재미가 있어집니다. 

## 참고 문헌

---

[혁펜 하임의 Easy! 딥러닝](https://www.youtube.com/watch?v=M6Hf6R8byvM)

[공돌이의 수학정리 노트](https://angeloyeo.github.io/2020/07/17/MLE.html)
