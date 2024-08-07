---
layout: single
title: U-Net':'Convolutional Networks for Biomedical Image Segmentation paper review(논문 리뷰)
category: DeepLearning
tag: [논문 리뷰, Paper Review, DeepLearning]
toc: true
math_use: true

---

이번에는 굉장히 유명한 U-Net 네트워크를 Reveiw 해보도록 하겠습니다.

해당 네트워크는 네트워크 구조가 U자 모양이라 U net이라고 불리어 집니다.

해당 네트워크는 ISBI라는 노인성 황반병성 당뇨망막 병증 등 이러한 질환 판독을 하는 의료 이미지 판별 대회를 위해 만들어졌습니다.

그럼 리뷰해보도록 하겠습니다.

## Abstract

---

deep neural network를 성공적으로 학습시키기 위해서는 주석이 달린 수천개의 훈련 샘플이 필요하다는 것에 대해 많은 동의가 있다고 합니다.

여기서 주석은 labeling을 의미합니다.

그래서 이 논문에서는 주석이 달린 이러한 훈련용 데이터 샘플을 보다 효율적으로 사용하기 위해 네트워크 및 학습 전략을 제시한다고 하네요.

<p align="center"><img src="https://github.com/user-attachments/assets/31c27983-7958-4800-8ccb-99e92547eee7" width="65%" height="65%"></p>

또한 네트워크는 위 사진과 같이  중앙을 기준으로 왼쪽은 Contracting path, Expanding Path로 이루어져 있습니다.

그리고 Contracting path는 한국어로 번역하자면 수축 경로 즉 이미지를 수축해주는 구간이고 Expanding path는 이미지를 확장시켜주는 구간 입니다.

이러한 구조의 네트워크는 ISBI에서 우승을 차지하였으며, 기존 형태의 cnn보다 성능도 좋고 속도도 엄청 빠르다고 합니다.

512 by 512 크기의 이미지를 분할하는데 1초도 걸리지 않는다고 하네요.

Introduction

---

기존의 지난 네트워크들은 많이 발전은 했지만 가능한 훈련 데이터의 양과 제한된 네트워크 크기로 인해 성공적인 학습이 제한이 되었다고 하네요.

기존 연구들은 Image net을 이용하여 훈련을 진행하였으나, 해당 데이터들은 단일 클래스 labeling 분류 작업을 위한 작업이였습니다.

즉 이미지를 클래스 별로 분류하는 작업을 의미합니다.

하지만 의료 이미지 같은 경우 단순히 이미지 전체를 보고 이미지 클래스를 분류하는 것이 아닌, 이미지에 있는 픽셀별로 픽셀들을 클래스 분류가 필요하며, 위치 정보도 파악이 되어야 한다는 것 입니다.

즉 이미지 픽셀 별 위치가 굉장히 중요하다는 것이겠지요.

왜냐하면 의료 분야 이미지 같은 경우 단순히 이미지 전체를 보고 해당 병에 대한 양성 음성 비교를 하는 것 뿐 아닌 어떤 위치에 종양이 있는지, 위치 별 픽셀 정보값이 매우 중요하다는 것을 나타내고 싶은 것 같습니다.

그리고 각 클래스별 수천개의 이미지로는 의료 이미지를 성공적으로 학습시키기에는 너무나도 부족한 이미지 데이터 수량 이라고 합니다.

그렇기 때문에 U Net을 개발했다고 합니다.

<p align="center"><img src="https://github.com/user-attachments/assets/c48683a1-26ce-4d09-bcf0-18e35887c7d2" width="65%" height="65%"></p>

위 사진은 model architecture입니다.

정말로 U자모양의 네트워크 구조이죠.

각 박스별 역할의 설명입니다.

- Blue box : multi-channel feature map
- White box : 복사된(=copied) feature map
- Top of the box : 채널의 수 표기
- The arrow : different operation
- Lower left edge of the box : X-Y size

해당 네트워크는 End to End 방식의 Fully Convolution Network를 기반으로 한 모델입니다.

End to End는 신경망 한쪽 끝에서 입력을 받아들이고 이게 신경망을 통과하면서 다른 반대 쪽 끝에서 출력을 하게 되는데, 이때 이 입력 데이터를 네트워크를 통과하면서 모든 네트워크의 parameter가 해당 데이터 한개를 통과하며 사용되는 손실함수에 대해서 동시에 훈련되는 방식을 의미합니다.

이를 통해서 Backpropagation을 진행이 원활하게 되며 네트워크의 가중치가 모두 최적화 되는 방식입니다.

해당 네트워크의 특징은 먼저, localize가 가능합니다

여기서 localize란 이미지의 특정 객체가 이미지 안에 어떤 위치에 있는지 위치 정보를 출력해주는 것 입니다.

두 번째는 패치 측면의 훈련 데이터는 훈련이미지 수 보다 더많다고 합니다.

단점으로는 두 가지가 있는데요.

패치마다 네트워크를 별도로 운영해야하기 때문에 속도가 상당히 느리고 패치가 겹쳐서 중복성이 많다고 합니다.

두 번째는 현지화 정확도와 컨텍스트 사용 간에는 상충 관계가 있다고 합니다.

이 모델은 매우 적은 수의 훈련 데이터 이미지로도 잘 작동하고 정확한 segmentation을 생성하도록 아키텍처를 수정하고 확장한다고 합니다.

그럼 각 구역별로 자세히 알아보도록 하겠습니다.

## Contracting Path

---

수축 경로에서는 이미지를 downsampling 하는 과정을 반복합니다.

<p align="center"><img src="https://github.com/user-attachments/assets/31c27983-7958-4800-8ccb-99e92547eee7" width="65%" height="65%"></p>

순서는 다음과 같습니다.

1. **3×3 Convolution Layer + ReLu + BatchNorm (No Padding, Stride 1)**
2. **3×3 Convolution Layer + ReLu + BatchNorm (No Padding, Stride 1)**
3. **2×2 Max-polling Layer (Stride 2)**

이 과정을 통해서 이미지의 주변 픽셀들을 참조하는 범위를 넓혀가며 정보를 추출하는 과정이 이루어 집니다.

3x3 Convolution을 수행할 때 이 모델은 패딩을 하지 않기 때문에 feature map크기가 점점 감소하게 됩니다.

대신 Downsampling을 진행할 때 마다 channel수를 2배 증가시키면서 진행을 하기 때문에

처음 Input channel을 64개로 증가시키는 부분을 제외한다면 전체적인 과정은 1→64→128→256→512-1024가 됩니다.

## Bottle Neck(전환 구간)

---

이 부분은 모델 구조에서 정 중앙에 위치해 있는 구간으로 Contracting 구간에서 Expanding 구간으로 전환이 되는 중간 구간입니다.

<p align="center"><img src="https://github.com/user-attachments/assets/31c27983-7958-4800-8ccb-99e92547eee7" width="65%" height="65%"></p>

해당 구간의 구조는 다음과 같습니다.

1. **3×3 Convolution Layer + ReLu + BatchNorm (No Padding, Stride 1)**
2. **3×3 Convolution Layer + ReLu + BatchNorm (No Padding, Stride 1)**
3. **Dropout Layer**

마지막에 적용된 Dropout을 통해서 모델을 Normalize하고 노이즈에 견고하게(Robust)만드는 구간 입니다.

## Expanding Path

---

확장 경로에서는 Contracting Path와 반대로 Upsampling 하는 과정을 반복하여 Feature맵을 생성합니다.

해당 구간의 구조는 다음과 같습니다.

<p align="center"><img src="https://github.com/user-attachments/assets/31c27983-7958-4800-8ccb-99e92547eee7" width="65%" height="65%"></p>

1. **2×2 Deconvolution layer (Stride 2)**
2. 수축 경로에서 동일한 Level의 특징맵(Feature Map)을 추출하고 크기를 맞추기 위하여 자른 후 이전 Layer에서 생성된 특징맵(Feature Map)과 **연결(Concatenation)**합니다.
3. **3×3 Convolution Layer + ReLu + BatchNorm (No Padding, Stride 1)**
4. **3×3 Convolution Layer + ReLu + BatchNorm (No Padding, Stride 1)**

이 Expading path에서는 Skip connection 기법을 통하여 Contracting path에서 생성된 feature 정보와 위치 정보를 결합하는 역할을 합니다.

왜냐하면 이 모델 구조상 downsampling을 계속 하며 padding을 진행하지 않기 떄문에 굉장히 feature맵이 작아진 상태이며 이는 중요한 위치 정보 feature 정보가 손실이 많이 되었을 것이기 때문에 이전 정보를 추가로 넣어주는 것 입니다.

## Training

---

Training 부분에 있어서는 총 4가지 방식으로 학습을 했다고 합니다.

- **Overlap-tile strategy** : 큰 이미지를 겹치는 부분이 있도록 일정크기로 나누고 모델의 Input으로 활용합니다.
- **Mirroring Extrapolate** : 이미지의 경계(Border)부분을 거울이 반사된 것처럼 확장하여 Input으로 활용합니다.
- **Weight Loss** : 모델이 객체간 경계를 구분할 수 있도록 Weight Loss를 구성하고 학습합니다.
- **Data Augmentation** : 적은 데이터로 모델을 잘 학습할 수 있도록 데이터 증강 방법을 활용합니다.
    
    
    <p align="center"><img src="https://github.com/user-attachments/assets/b1fedca2-9ea4-4e48-8169-97f37b1b1e97" width="65%" height="65%"></p>
    
    해당 이미지는 Overlap-tile 과정을 설명하기 위해 참조한 이미지 입니다.
    
    참조[[https://medium.com/@msmapark2/u-net-논문-리뷰-u-net-convolutional-networks-for-biomedical-image-segmentation-456d6901b28a](https://medium.com/@msmapark2/u-net-%EB%85%BC%EB%AC%B8-%EB%A6%AC%EB%B7%B0-u-net-convolutional-networks-for-biomedical-image-segmentation-456d6901b28a)]
    
    이미지의 크기가 큰 경우 이미지를 자른 후 각 이미지에서 특정 픽셀들을 Segmentation을 진행합니다.
    
    그런데 U-net input과 output의 이미지가 다르기 때문에, 위 그림과 같이 노란색 영역을 output으로 추출하기 위해서는 파란색 영역을 넣어야합니다.
    
    또한 초록색 영역을 추출하기 위해서는 빨간색 영역을 input으로 넣어야합니다.
    
    그럼 이렇게 되면 빨간색 영역과 파란색 영역에서 겹치는 부분이 생기며 이렇게 겹치는 부분이 생기도록 이미지를 input으로 넣는 방법이 Overlap-tile strategy입니다.
    

<p align="center"><img src="https://github.com/user-attachments/assets/e72eb158-d945-445b-86d0-5ea28f50c5c5" width="65%" height="65%"></p>

다음은 Mirroring Extrapolate입니다.

이것은 해당 모델이 padding을 하지 않기 때문에, 위의 예시처럼 이미지의 경계에 위치한 이미지를 복사하고 좌우 반전을 통해 Mirror 이미지를 생성한 후 원본 이미지 주변에 붙여 input으로 적용 시킵니다. 

<p align="center"><img src="https://github.com/user-attachments/assets/07e60a02-6e9b-4068-b239-2a7070507ef1" width="65%" height="65%"></p>

다음은 Bio-Medical Image Segmenation 부분입니다.

이런 의료 이미지들은 각 세포 별 경계가 굉장히 중요합니다.

그리고 경계가 분리할 수 있도록 학습이 되어야 합니다. 그래야 세포들을 구별 할 수 있기 때문입니다.

그래서 논문에서는 각 픽셀이 경계부분과 얼마나 가까운지에 따른 가중치 맵을 만들고 학습할 때 경계에 가까운 픽셀의 Loss를 Weight map에 비례하게 증가 시켜 경계를 잘 학습 할 수 있도록 설계를 하였습니다.

그리고 이러한 Loss는 다음 수식과 같이 정의 할 수 있습니다.

<p align="center"><img src="https://github.com/user-attachments/assets/684ab631-4357-4909-826a-aa00683201ba" width="65%" height="65%"></p>

ak(x): 픽셀 x가 Class k일 값(픽셀 별 모델의 Output)

𝑝𝑘(𝑥): 픽셀 x가 Class k일 확률(0~1)

𝑙(𝑥): 픽셀 x의 실제 Label

𝑤0: 논문의 Weight hyper-parameter, 논문에서 10으로 설정

𝜎: 논문의 Weight hyper-parameter, 논문에서 5로 설정

𝑑1(𝑥): 픽셀 x의 위치로부터 가장 가까운 경계와 거리

𝑑2(𝑥): 픽셀 x의 위치로부터 두번째로 가까운 경계와 거리

위 수식을 통해서 w(x)의 경우 픽셀x가 경계와의 거리가 가까울 수록 큰 값을 가지게 되며, 해당 픽셀의 Loss비중이 커지게 됩니다.

이렇게 큰 Loss값은 학습시 경계에 가까운 픽셀들을 더욱 더 잘 학습하게 되는 결과로 이어지는 것 입니다.

<p align="center"><img src="https://github.com/user-attachments/assets/ddb07b56-826e-4b95-b880-c2b69b2a07d7" width="65%" height="65%"></p>

위 그림은 픽셀 위치에 따른 Weight w(x)를 시각화 한 것 입니다.

w(x)값은 객체의 경계 부분에서 큰 값을 가지게 되며 빨간색으로 높은 가중치를 가지게 됩니다.

Data Augumentation은 너무 이전 논문들에서 잘 설명하였으니 넘기도록 하겠습니다.

Result of Experiment

---

<p align="center"><img src="https://github.com/user-attachments/assets/ed5cffd9-ae85-487c-9362-35f322a0d4b5" width="65%" height="65%"></p>

해당 실험결과는 EM Segmentation challenge dataset을 활용하며 이 데이터 셋은 30개 밖에 안되는 training 데이터를 제공합니다.

그리고 해당 데이터는 이미지와 함께 이미지와 배경이 구분 된 즉 0혹은 1로 구분된 Ground Truth Segmentation Map을 포함하고 있습니다.

[Warping Error](https://imagej.net/Topology_preserving_warping_error) : 객체 분할 및 병합이 잘 되었는지 세크멘테이션과 관련된 에러

Warping Error를 기준으로 “EM Segmentation” 데이터에서 U-Net 모델이 가장 좋은 성능을 보이고 있습니다.

세포 분류 대회인 **ISBI cell tracking challeng** 에서 모델의 성능을 평가한 표는 아래와 같습니다. “PhC-U373” 데이터는 위상차 현미경으로 기록한 35개의 이미지를 Training 데이터로 제공합니다. “DIC-HeLa” 데이터는 HeLa 세포를 현미경을 통해 기록하고 20개의 이미지를 Training 데이터로 제공합니다.

<p align="center"><img src="https://github.com/user-attachments/assets/b45d1f6f-7060-4328-b6ff-d99b06f934d4" width="65%" height="65%"></p>

U-Net 모델은 “PhC-U373” 데이터에서 92% IOU Score를 획득하였으며 2등 모델이 획득한 점수 83% 와 현격한 차이를 보이고 있습니다. U-Net 모델은 “DIC-HeLa” 데이터에서 77.5% IOU Score를 획득하였으며 2등 모델이 획득한 점수 46% 와 현격한 차이를 보이고 있습니다.
