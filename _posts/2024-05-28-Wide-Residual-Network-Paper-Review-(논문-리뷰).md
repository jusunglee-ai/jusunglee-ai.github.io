---
layout: single
title: Wide Residual Network paper review(논문 리뷰)
category: DeepLearning
tag: [논문 리뷰, Paper Review, DeepLearning]
toc: true
math_use: true

---


이번에는 Wide Residual network를 논문을 리뷰 해보도록 하겠습니다.

해당 논문은 WRN으로 불려지며, ResNet을 개량한 모델에 대해 다루는 논문입니다.

그럼 어떻게  기존 ResNet에서 바꾸었을까요?

논문의 제목 그대로 Wide하게 바꾼겁니다. Wide하게 바꾼게 무슨 뜻일까요 이때 wide는 넓이를 증가시키고 깊이를 감소시킨 모델입니다.

그리고 신경망의 넓이를 증가시킨다는 것은 filter수를 증가시킨다는 것을 의미하죠.

그럼 전체적으로 이 논문이 어떤 모델을 다루는지 간단하게 요약을 해보았으니, 전체적으로 리뷰를 해보도록 하겠습니다.

## Abstract

---

Deep Residual Network 즉 이 ResNet은 이때까지 최대 수천 개의 레이어를 확장할 수 있으며 모델을 더 깊게 할수록 성능이 향상 되는 것으로 나타났다고 합니다.

하지만 항상 모델을 깊게하면 깊게 할수록 발생하는 문제인 바로 매우 깊은 네트워크를 학습하면 훈련 속도가 늦어지게 되는데요. 특히 이 저자는 기능 재사용이 줄어드는 문제가 있었다고 합니다.

???:그래서 이 기능 재사용 감소(diminishing feature Reuse)이 뭐임?
이는 Forward Propagation에서 발생하는 문제이며, 기울기 소실 즉 Gradient Vanishing과 비슷한 문제 입니다.

입력과 가까운 계층이 학습한 feature가 최종 계층까지 도달하지 못하고 사라지는 문제인데요.

이 이유는 너무나도 Network가 깊어짐으로써, 계속해서 convolution 연산을 하게 되며, 계속되는 Convolution 연산으로 인하여 결국에는 사라지는건데요 예를 들어 이미 작은 Feature인데 거기에 또 convolution 연산을 반복하여 결국에는 사라지는 것이죠.

그래서 여러가지 실험을 하면서 ResNet을 깊게 만들기보다는 넓게 만들어서 기능을 향상 시켰다고 하네요 그리고 이 실험 결과는 대표적인 데이터 CIFAR, COCO, ImageNet 등 데이터 셋을 활용하였을 때 성능 향상이 되었다고 보여줍니다.

## Introduction

---

이 논문이 발표될 시절에는 AlexNet, VGG, Inception ,ResNet 등 Imagenet classification 대회에서 엄청난 성과를 보여주었던 모델들이 굉장히 인기가 많았고 이 때 당시에 이런 모델들이 인기가 많아지면서 네트워크를 굉장히 깊게 만드는게 유행이었다고 합니다.

하지만 항상 이러한 형태의 모델들은 많은 parameter가 요구되며, 

Gradient Vanishing/Exploding 문제가 발생하였고, 오히려 성능이 저하되는 경우 등도 있는 여러 어려움이 있었다고 합니다.

그래서 저자는 이러한 문제를 좀 해결하며, 성능을 향상시키고자 Wide Residual Network를 연구하게 되었다고 하네요.

또한 네트워크의 깊이와 파라미터는 줄이고 성능을 향상시키기 위해서 

네트워크를 더욱 깊게 만드는 연구가 아닌 넓이를 넓히는 연구를 했다고 합니다.

???:네트워크를 깊게 한다는 것은 알고 있지만 넓게 한다는 것은 무슨 의미임?

여기서 넓이는 filter의 수를 늘린다는 의미 입니다.

그리고 이 16개의 레이러를 가진 wide residual network는 ResNet-1000과 동일 한 정확도와 비슷한 수의 parameter를 가지지만 훈련속도는 몇 배나 빠르다고 하네요.

<p align="center"><img src="https://github.com/jusunglee-ai/jusunglee-ai.github.io/assets/125032849/d3cd4c67-9e2f-4e31-97af-779dbe80a1da" width="65%" height="65%"></p>

그 다음 성능 향상을 위해서 Resdual block안에 dropout을 적용하는 방안은 저자는 고민을 많이 하였다고 하네요 기존에는 residual block과 convolution layer사이에 drop out을 적용시켰다면 이번에는 Residual block 안에서 dropout을 적용시켜 이를 테스트 했다고 합니다.

a와b는 기존의 Resnet의 구조이며, b는 기존의 bottleneck구조입니다.

이는 Resnet 논문을 읽어 보셧다면 아실 겁니다.

c와 d는 WRN의 Residual blcok구조이며, 위와 같은 Residual block들은 BatchNorm-ReLU-Convlayer 형태로 이루어져 있다고 합니다.

그리고 d의 구조가 바로 이 저자가 연구하고자 하였던 Residual block 안에 dropout을 적용한 형태 입니다.

## Wide Residual Blocks

---

<p align="center"><img src="https://github.com/jusunglee-ai/jusunglee-ai.github.io/assets/125032849/8693f520-9971-4f63-ae63-6adf4fd0f459" width="65%" height="65%"></p>

다음은 Residual block의 identity mapping 과정을 알려드리도록 하겠습니다.

x_l+1과 x_l은 l번째 네트워크의 output과 input을 의미합니다.

또한 F는 residual function이며, W_l은 block parameter를 나타냅니다.


<p align="center"><img src="https://github.com/jusunglee-ai/jusunglee-ai.github.io/assets/125032849/688dd00d-250d-4f14-bb78-0219cc8478c1" width="65%" height="65%"></p>

해당 표는 Wide Residual Network의 구조를 나타낸 표 입니다.

여기서 k는 네트워크의 width 즉 넓이 폭을 의미하며, N은 해당 블록의 개수를 의미합니다.

여기서 3x3는 Kernel_size를 의미하며, k는 기존 convolution layer의 필터 수의 k배를 해주는 것 입니다 만약에 k가 2라면 필터수가 기존보다 2개 늘어나겠죠 그리고 N은 이러한 형태의 Residual block이 몇 개 있는지 나타내기에 N-2이면 위와 같은 형태의 Residual block이 두 개 있는 것 입니다.

residual block의 표현력을 높이는 방법은 총 3가지가 있다고 저자는 말하는데요 

여기서 표현력은 더 많고 다양한 feature를 출력하는 의미로 해석이 됩니다.

왜냐하면 이미지의 표현력을 높인다는 것은 해당 residual block을 통과한 이미지로부터 여러가지 종류의 feature들을 추출한다는 의미로 해석이 이어지기 때문입니다.

그럼 3가지 방법을 알아보도록 하겠습니다.

첫 번째는 block한 개당 convolution layer를 늘리는 것

두 번째는 더 많은 특성을 추가하기 위해 convlayer를 넓히는 것 입니다.(filter수를 늘린다는 의미)

세 번째는 convlayer의 filter 사이즈들을 늘리는 것 입니다.

## Result of experimental

---

그럼 실험에 쓰인 residual block구조를 살펴보도록 하겠습니다.

<p align="center"><img src="https://github.com/jusunglee-ai/jusunglee-ai.github.io/assets/125032849/bb5f5f06-4acc-4dd1-af6a-51192331b43a" width="65%" height="65%"></p>
1번째 B(3,3)은 기존의 Residual block, 2번째 B(3,1,3)은 중간에 1x1 conv layer 를 추가 하였습니다.

3번째 B(1,3,1)은 모든 conv layer의 차원이 똑같으며 1x1 ,3x3 ,1x1 layer의 형태입니다.

4번째도 1x1,3x3형태

5번째는 이전 residual block과 비슷한 형태의 레이어이며, 3x3 ,1x1 구조입니다.

6번째는 3x3,1x1,1x1형태이며 network in network스타일 구조라고 합니다.

<p align="center"><img src="https://github.com/jusunglee-ai/jusunglee-ai.github.io/assets/125032849/5b30d3b5-60bc-4d36-b2c5-b0ed6c703044" width="65%" height="65%"></p>

해당 좌측는 Residual block을 구성하는 conv layer의 개수와, kernel size에 따른 테스트 에러 표입니다.

우측표는 테스트 에러 결과 표이며,  l은 layer의 수에 따릅니다.

그리고 bottleneck구조는 WRN-40-2를 사용했다고 합니다.

<p align="center"><img src="https://github.com/jusunglee-ai/jusunglee-ai.github.io/assets/125032849/c9a79f7c-cc47-46c7-be32-fa5584cfa532" width="65%" height="65%"></p>
다음은40,22,16layer가진 모든 네트워크가width가 1배부터 12배까지, depth는 16에서 40까지 증가함 따른 실험 결과 표입니다.

그리고 k=8 혹은 10을 유지하고 깊이를 16에서 28로 변경하면 일관된 개선이 있지만 깊이를 40으로 더 늘리면 정확도가 감소한다고 하네요 대표적인 예시로 WRN-40-8이 WRN-22-8에 비해 정확도가 감소한거를 예시로 들 수 있습니다.

다음은 얇은 네트워크와 wide네트워크간의 비교 표입니다.

<p align="center"><img src="https://github.com/jusunglee-ai/jusunglee-ai.github.io/assets/125032849/3db21bf9-d608-459c-9463-b3076ae80df2" width="65%" height="65%"></p>

여기서 얇은 ResNet은 기존의 ResNet에서 네트워크의 깊이만 깊어진 구조입니다.

그리고 이 실험 결과 보고서에 따르면 WRN-28-10이 RensNet-1001보다 CIFAR-10에서 0.92 % 성능이 뛰어나고 CIFAR-100에서는 3.46%성능이 뛰어나며 성능이 뛰어남에도 불구하고 레이어 수가 36배 적다고합니다.

<p align="center"><img src="https://github.com/jusunglee-ai/jusunglee-ai.github.io/assets/125032849/bc6c2091-1420-46dc-a79f-f37878e92d05" width="65%" height="65%"></p>

다음은 CIFAR 10과 100데이터를 이용하여 ResNet 164와 WRN28-10의 epoch에 따른 train error와 test error비교표입니다.

해당 비교표를 통해, 요약을 하자면,

1.ResNet을 wide하게 표현하는 것은 다양한 깊이의ResNet 성능을 향상시킵니다.

2.depth와 wide를 둘 다 늘리면 parameter가 너무 많아지고 더욱 더 강력한 정규화가 필요할떄까지 도움이 된다고 합니다.

3.기존 ResNet과 동일한 수의 parameter를 가진 WRN은 Residual block이 더욱 더 깊으며, 동일하거나 더 나은 표현을 학습할 수 있기 때문에 정규화 효과가 없다고 합니다.

그리고 기존 네트워크와 비교 하였을 때 wide networks는 기존 네트워크보다 2배 또는 그 이상의 parameter를 성공적으로 학습할 수 있다고 합니다.

<p align="center"><img src="https://github.com/jusunglee-ai/jusunglee-ai.github.io/assets/125032849/91a2950f-c382-4172-9383-3dd311fc8d95" width="65%" height="65%"></p>

다음은 dropout을  Residual block에 적용한 네트워크와 적용하지 않은 네트워크 간의 성능 비교 결과 표 입니다.

이 결과표를 통해서 Residual block사이에 dropout을 적용 시키는 것이 상당한 성능 향상을 이루워 냈다는 것을 알 수 있습니다.

이는 기존 Resnet과 WRN과 상관없이 둘 다 향상이 이루어졌습니다.

<p align="center"><img src="https://github.com/jusunglee-ai/jusunglee-ai.github.io/assets/125032849/5d081f86-7061-4817-8d15-a14b311fc845" width="65%" height="65%"></p>

마지막 결과표는 기존 ResNet과 WRN간의 학습 시간 비교입니다.

위 비교표를 통해 WRN이 압도적으로 학습속도가 빠르다는 것을 알 수 있으며,  가장 의미 있는 결과는 WRN40-4이 ResNet중에서 가장 성능이 좋은 ResNet1004보다 8배나 빠르다는 결과 입니다.

더군다나 성능은 WRN-40-4는 ResNet1001과 거의 동일한 성능을 가지고 있는데도 불구하고 8배나 학습속도가 빠르다는 점이 정말 유의미한 실험 연구 결과라는 것을 알 수 있습니다.

이렇게 Wide Residual Network논문 리뷰를 마치겠습니다.
