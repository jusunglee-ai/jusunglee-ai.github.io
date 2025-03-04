---
layout: single
title: Imagic':' Text-Based Real Image Editing with Diffusion Models paper review(논문 리뷰)
category: DeepLearning
tag: [논문 리뷰, Paper Review, DeepLearning]
toc: true
math_use: true

---
# Imagic: Text-Based Real Image Editing with Diffusion Models

Text-conditioned image editing 분야는 해당 논문이 나온 기준인 2023년 기준으로 굉장히 매력적으로 인기를 끌었던 분야라고 합니다.

하지만 대부분의 기존 방법들(object overlay, style transfer)은 한계 점이 명확했다고 합니다.

이미지 합성을 통해 새로운 이미지를 생성하는 방법이나  한 개의 일반 object에 여러가지 input image를 요구한다던지와 같은 한계 점이 있었다고 합니다.

그래서 저자는 한 개의 Image에 text condition을 추가 함으로써, 이 이미지를 수정할 수 있는 방법을 제안했습니다.

이전 연구와 달리 저자의 연구는 단순히 한 장의 image에 우리가 수정하고 싶은 객체와 그 수정하고자하는 내용의 text만 넣으면 가능하다는 점에서 큰 장점이 있습니다.

추가적인 mask나 객체의 다른 여러가지 시점의 이미지 필요 없이요. 그래서 저자는 이러한 방식을imagic이라고 칭했습니다.

그리고 저자는 이 방법을 통해 퀄리티 있고 다양성이 있는 이미지를 다양한 도메인으로부터 구현을 성공하였다고 합니다.

      

## Introduction

---

실제 사진에 사소한 semantic 수정을 적용하는 것은 image processing에서 오랫동안 관심을 많이 받는 task였습니다.

단순한 자연어 text를 이용하여 간단한 text에 적힌대로 이미지 수정을 구현하는 방식은 인간의 의사소통으로부터 영감을 받았다고 합니다. 

예를 들어서, 그림을 그리는 기업에서 그림 작가(A씨)에게 편집자(B씨)가 “A씨 이 그림에서 강아지 자세를 앉아 있는 자세로 바꿔 주세요”라고 간단한 피드백이나 요청을 하면 A씨가 그 그림에서 강아지라는 객체의 자세만 앉은 자세로 수정하는 방식에서 영감을 받았다고 생각하면 좋을 것 같습니다.

이미지 수정 분야에서의 최근 연구는 3가지의 결점이 있다고 합니다.

1.  이미지 위에 그림을 덫칠하거나 객체를 추가하거나 transferring style를 추가하는 것과 같은 특정   

   편집 셋트로 제한이 된다고 합니다.—> 왜? 이게 결점임?

2.특정 domain 또는 합성되어 생성된 image에서만 작동 됨.

3.추가적인 input image나 mask와 같은 추가적인 요소나 같은 한 가지 객체에 대한 여러 가지 이미지를 추가한다거나 혹은  원본 이미지에 대한 추가적인 설명 text가 필요한 것과 같은 요소가 추가적으로 필요 하다는 단점이 있다고 합니다. 

그래서 저자는 이러한 결점을 모두 해결하는 해결하는 아래와 같은 semantic image editing 방식을 제안 한다고 합니다. 

오직 한 장의 이미지와 수정하고자 하는 객체와 수정 내용이 포함 된 단순한 text prompt만 input으로 넣어 고 화질의 수정 된 이미지를 만들어 내는 방식 해당 논문에서는 설명하고 제안 한다고 합니다.

  

그리고 이러한 방법으로 만들어 낸 output은 아래의 그림과 같이 original image와 비교하였을 때 배경이나 이미지 구조나 이미지를 구성하는 요소들은 온전하게 보존하며, 우리가 text를 통해 원하는 객체와 그 객체의 원하는 수정사항만 반영하여, output을 내는 퍼포먼스를  보여 주었다고 합니다.   

![image.png](https://github.com/user-attachments/assets/dafcb667-83a2-4641-b5ba-4ebd21792d4f)

저자가 제안하는 방법에 대해서는 크게 3가지 장점이 있다고 언급을 합니다.

첫 번째로는, 제가 위에서 언급했던 바와 같이 text로 언급한 수정요소 및 객체를 제외하고는 나머지 모든 이미지의 구성 요소나 배경들을 모두 온전히 유지하면서 text로 언급한 부분만 수정이 된다는 점 입니다.

두 번째로는 최근 SOTA성능을 내보이는 Diffsuion모델을 사용하여 이미지 생성 분야에서 가장 좋은 성능과 다양한 고 퀄리티 이미지 합성 생성을 가능하게 하는 능력을가지고 있습니다.

또한 diffusion의 경우, 저자가 사용하는 text condition을 diffusion에 사용을 하였을 때 강력하고 좋은 성능을 낼 수 있는 능력이 있기 때문에 저자는 이런 부분을 장점으로 꼽았습니다.

세 번째로는 저자가 제안하는 방법으로는 3가지 step의 진행 과정으로 이루어져 있기 때문에 굉장히 간단하다고 합니다.

![image.png](https://github.com/user-attachments/assets/a1f885a9-9ad5-4eb8-b297-a953d98e0124)

위의 그림이 저자가 제안하는 방식의 진행과정입니다.

진행 과정에 대해서는 이후 내용에서 더욱 자세히 다룰 예정이니,  일단은 3가지 간단한 과정으로 이루어진다는 점만 참고 해주시면 감사하겠습니다.

마지막으로 저자는 TEdBench라는 Textual Editing Benchmark라는 새로운 평가 지표를 주제로 삼아서 다루었습니다.

이 부분은 ablation study에서 다루었으니 뒷 부분에서 다루도록 하겠습니다.

그래서 저자가 이 논문에서 다루는 3가지 주제를 요약하자면 다음과 같습니다.

1.Imagic이라는 text base의 semantic image  수정 기술을 소개를 하는데, 이 기술은 원본 이미지의 배경이나 구성 요소들을 유지하면서 text에서 수정하고자 하는 객체와 수정하고자 하는 부분만 수정해서 이미지를 수정하는 기술입니다.

2.저자가 제안한 방법에서는 두 가지의 text embedding 문장 간의 선형 보간을 통해 좀 더 semantical한 부분이 더욱 강하게 구현을 시켰으며, text - to -image diffusion model에서의 구성 요소들을 밝혀 냈습니다.

3.TEdBench라는 새로운 평가지표를 소개합니다.

해당 지표는 글과 복잡한 이미지 수정 벤치마크로써, text base의 이미지 수정 방식들을 비교하며 평가하는 평가지표입니다. 

그럼 다음은 바로 Method에 대해서 설명 드리도록 하겠습니다.

## Method

---

저자는 Diffusion model들이 image generation 분야에서 최근 SOTA 성능을 내보이며, 이 뿐만 아닌 하위 분야 (downstream task) 대표적으로 SR(Super Resolution), Image restoration, image classification과 같은 다양한 컴퓨터 비전 분야에서 적용이 가능할 뿐만 아니라 이러한 분야에서 좋은 성과를 내보여주고 있기 떄문에 diffusion model에 대해 간단히 설명하며 채택을 했다고 합니다.

기본적으로 저자가 제안하는 방식에서 사용되는 diffusion 모델의 작동 방식에 대해서 설명을 드리도록 하겠습니다.

   

![image.png](https://github.com/user-attachments/assets/8fd2e139-b2b5-4030-8e8f-7b2a40a23cbd)

 

이게 기본적으로 저자가 사용하는 backbone diffusion model의 작동 과정이자 이미지가 생성되는 과정입니다.

여기서 각 parameter들에 대해 설명을 드리자면 아래와 같습니다.

x=이미지

t=반복 시점 (예시: t=1이면 , 처음으로 노이즈를 끼는 시점 t=0인 경우 노이즈를 사용하지 않은 원본 이미지.)

α=노이즈를 얼만큼 부여할지에 대한 혹은 원본 이미지를 얼만큼 반영 할지에 대한 hyperparameter

ϵ=평균이0이고 분산이 I 인 정규분포 형태를 가지고있는 가우시안 노이즈, 여기서 중요한 것은 분산이 1인 가우시안 노이즈가 아닌 단위 공분산 행렬을 적용한 가우시안 노이즈를 적용한 것이 핵심 입니다.

 

![image.png](https://github.com/user-attachments/assets/7cc3f506-4c6d-4bf8-b3df-e4dffa0e450d)

어떤말인지 이해가 되지 않을 수 있습니다.

좀 더 직관적으로 예시를 들어보도록 하겠습니다.

우리는 기본적으로 가우시안 노이즈를 이미지에 적용할 때 이미지의 픽셀(차원)별로 0과 1사이의 값을 갖는 랜덤한 노이즈를 가지게 됩니다.

그리고 이러한 노이즈는 특정 차원(픽셀)은 강한 노이즈를 부여받게 되고 특정 차원(픽셀)은 약한 노이즈를 부여받게 되죠.

디퓨전 모델의 특성상 이러한 노이즈를 학습하고 다음에 올 노이즈가 낀 이미지 혹은 노이즈가 제거 된 이미지를 학습하기 때문에 이런 부분에서 편향이 발생할 수 밖에 없게 됩니다.

그래서 저자는 이러한 부분을 해결하기 위해서 단위 공분산 행렬을 필터처럼 적용하여 모든 차원(픽셀)에 균등한 노이즈를 부여하고자 하였다고 합니다.

그래서 본 수식을 해석하자면 t시점의 이미지에 원본 이미지를  α비율 만큼 반영하고 1-a의 루트 값 만큼 노이즈를 부여해서 노이즈가 낀 이미지를 생성하는 방식의 diffusion모델을 사용하였다고 합니다.

여기서 α의 경우 처음에는 1이였다가 점점 시행 횟수(t)가 커질수록 0에 가까워지면 최종적인 시행횟수(T)때는 0이 되는 값이라고 합니다.

그리고 값이 줄어드는 비율의 경우 사용자가 설정할 수 있는 hyper parameter라고 합니다.

기본적인 diffusion model의 수행과정은 여기까지 다루도록 하고 저자가 제안하는 핵심 과정에 대해서 자세하게 설명드리도록 하겠습니다.

### Text embedding optimization

---

![image.png](https://github.com/user-attachments/assets/18de6e03-f6fb-431c-af0e-81f737272590)

해당 그림의 경우 1번째로 수행하는 저자가 제안한 방법의 과정입니다.

해당 과정은 먼저 target embedding과 optimized embedding이 존재하는데요.

target embedding의 경우 우리가 수정하고자 하는 객체와 그리고 그 객체의 수정 내용에 해당되는 문장의 embedding 값 입니다.

해당 그림의 예시로 들자면 “A bird spreading wings”  라는 문장의 embedding 값이 됩니다.

먼저 Exploring Limits of Transfer Learning with a Unified Text-to-Text Transformer라는 논문에 나오는 모델의 Encoder에  “A bird spreading wings”문장을 입력으로 넣어 통과 시켜줍니다. 

그리고 encoder를 통해 나온 output이 바로 target embedding이 되는 것이죠.

해당 embedding값의 차원의 경우 T x d(T의 경우 토큰 수, d의 경우 embedding dimension)의크기를 갖게 된다고 합니다.

다음 과정에서는 아래의 수식 과정이 이루어지게 됩니다.

![image.png](https://github.com/user-attachments/assets/76f20da8-6ce5-4e36-84e5-46427cb5fc02)

해당 과정에서는 pre-trained diffusion model의 parameter들은 모두 freeze(학습을 하는데도 불구하고 모든 parameter들이 변경되지 않게 얼린다는 의미)한 상태에서 denoising diffusion process를 진행함으로써 embedding 값을 최적화 한다고 합니다. 그리고 해당 과정의 Loss 함수이자 목적 함수는 위의 함수 입니다.

해당 과정을 해석을 해보자면, 실제 노이즈와 모델에게 위의 input들(t시점의 노이즈가 낀 이미지, 시점, embedding vector)을 넣었을 때의 노이즈간의 차이를 최소화하는 과정을 나타내는 함수 입니다.

해당 과정을 통해서 저자는 target embedding과의 거리가 굉장히 가깝게 유지되며, 입력 이미지와 최대한 일치하는 embedding을 얻게 되는데 이 embedding을 optimized embedding이라고 저자는 칭했습니다. 

여기서 저자는 굉장히 적은 step으로 과정을 수행한다고 합니다. 

이 두 embedding을 얻는 이유는 다음과 같습니다. 두 embedding을 통해서 선형 보간(linear interpolation)을 가능하게 만들기 때문 입니다.

### Model fine-tunning

---

다음은 모델의 fine-tunning 과정 입니다. 

논문의 원본에서는 저자가 다음과 같이 설명하고 있습니다.

우리가 1번째로 구한 optimized embedding을 넣었을 때 input image인 x와 이어지지는 않는다고 합니다.

즉, 우리가 앞에서 구한 optimized embedding을 이용하여 이미지를 복원하거나 하였을 때 무조건 input image와 동일하게 복원이 되지 않는다는 점 입니다.

그야 우리는 input image의 embedding과 최대한 일치하면서 target embedding과 가까운 embedding vector를 구한 것이지, input image의 embedding vector를 구한 것이 아니니까요.

 

그래서 해당 과정의 경우, embedding vector를 수정하는 것이 아닌 embedding vector는 고정한 채로 모델의 parameter를 최적화 해주는 과정을 진행한다고 합니다.

해당 과정의 경우 1번째 과정에서 수행했던 loss function과 동일하게 과정을 수행합니다.

![image.png](https://github.com/user-attachments/assets/76f20da8-6ce5-4e36-84e5-46427cb5fc02)

해당 과정의 경우, optimized embedding vector가 diffusion process를 통과하여 이미지를 생성할 때 input image와 일치 할 수 있도록 모델의 parameter를 조정하는 과정이라고 볼 수 있습니다.

동시에 generative 방법을 사용하는 대표적인 예시로 SR모델과 같은 보조 모델들도 finetunning 시킨다고 합니다. 이때 사용되는 loss의 경우 동일하다고 하네요.

대신에, 이때 편집된 이미지에서 보조 모델들이 작동하기 때문에 optimized embedding이 아닌 target embedding을 사용한다고 합니다.

이 보조 diffusion model들도 왜 fine-tunning을 해주냐면은 super-resolution이 되지 않은 input image x에 있는 고주파수 특징들을 보존해준다고 합니다.  

왜 사용했냐면 opt 보다 성능을 더 잘 내주었기 때문이라고 하네요.

## Text embedding interpolation

---

먼저, 생성형 diffusion model은 opt embedding 공간에서 input image x를 완전히 재 생성할 수 있도록 훈련이 되었기 때문에,  저자는 diffusion model이 target embedding 방향으로 이미지를 수정할 수 있게 tgt embedding과 opt embedding간의 선형 작업을 한다고 합니다.

그리고 그 작업은 아래의 수식과 같이 이루어집니다.  

![image.png](https://github.com/user-attachments/assets/c1961704-d5e5-4b78-b117-172debaf4d58)

여기서  η의경우 0과 1사이에 있는 hyper parameter입니다.

그리고 이 수식의 결과 값은 선형보간을 통해 얻은 embedding vector 값이고요.

그럼 해석을 한번해보도록 합시다. 해당 수식은 target embedding을 η의 값 즉 , η만큼 tgt embedding을 반영하고, opt embedding의 비율은 나머지 비율 만큼 반영해서 선형 보간을 진행합니다.

기본 적으로 선형 보간을 진행하는 방법에 대해서는 다음과 같습니다.

![image.png](https://github.com/user-attachments/assets/83002432-90a7-4028-8263-2322c2457af5)

![image.png](https://github.com/user-attachments/assets/d67a1e11-deb1-44f8-97b5-e4c9f5df6610)

[사진 출처:[https://darkpgmr.tistory.com/117](https://darkpgmr.tistory.com/117)]

우리가 선형 보간을 통해 알아 내고자 하는 지점을 x라고 가정을 했을 때, d_1은 x_1으로부터의 거리 , d_2는 , x_2로부터의 거리 입니다.

그리고 x와 f(x)에 해당 되는 점을 구하기 위해서는 여기서의 거리 비율이 반영이 되는데, 궁금증이 생길 수 있습니다.

어? 왜 ? f(x_1)의 비율을 반영하는데 d_2/전체거리(d_1+d_2) 과정이 수행 되는거야?

이 부분에서 d_2의 값이 크면 클 수록 x_2로부터의 거리가 멀어지고 x_1으로 부터 거리가 가까워 집니다.

이를 임베딩 vector 차원 관점으로 보자면 vector x가 x_1 vector에 더 가까워진다는 것은 x_1의 성분이 더 많이 반영이 되고 x_2보다는 x_1과 더 유사해지기 때문입니다. 그래서 x_1 성분 반영 비율을 계산할 때 d_2의 거리 비율이 들어가게 됩니다.

그리고 x_2의 비율을 계산할 때는 d_1의 거리 비율이 반영이 되는거구요.

그리고 이 두 비율의 합은 결국에 1이 되며  이를 간단하게 쓴다면 논문의 수식과 같이 아래의 수식으로 정리할 수 있습니다. 

 왜냐하면 결국에는 위 수식이나 아래의 수식이나 똑같이 embedding vector의 반영 비율을 얼만큼 반영 할지 이며, 나머지 embedding vector는 첫 번째 반영한 비율을 1에서 뺀 것이기 때문 입니다.

![image.png](https://github.com/user-attachments/assets/c1961704-d5e5-4b78-b117-172debaf4d58)

# Implementation Details

---

저자가 제안하는 framework의 경우, 일반적이고 다른 종류의 generative model과 결합하여 사용을 할 수 있다고 합니다.

그리고 저자는 Image generation 분야에서 SOTA성능을 내보이는 Imagen과 Stable Diffusion 두 모델을 사용하여 구현을 성공 시켰다고 합니다.

먼저 Imagen의 경우 3가지 모델로 구성이 되어 있는데 1번째로는 64x64 image를 생성하는 diffusion model 그리고 2번째로는 64x64 image를 256x256 로 해상도를 올려주는 SR diffusion model 3번째로는 다른 SR 모델인데, 256x256 이미지를 1024 x 1024로 해상도를 바꾸어주는 모델이라고 합니다.

여기서 1번째 모델의 optimize 과정은 아래와 같습니다.

optimizer:Adam

step: 100

learning late: 1e-3

저자들이 사용한 Ted Bench dataset으로 1500 회 학습.

target embedding과 original image를 1500회 동안 학습 시켯다고합니다.

그 이유는 original image에 존재하는 강한 frequency(original image를 가장 잘 나타내는 핵심적인 feature)를 보존하기 위해서라고 합니다.

결과에 거의 영향을 주지 않기 때문에 이 부분은 선택적으로 할 수 있다고합니다.

그럼에도 저자는 target text를 condition으로 사용한 pre-trained version의 모델을 사용하여  optimization을 수행했다고 합니다.

여기서 optimization process의 경우 2개의 TPU v4 chip을 사용하였으며, 이미지 한 장당 8분이 걸렸다고 합니다.

 두 번째로는 Stable Diffusion model의 최적화 과정입니다.

이 모델에서의 optimize의 경우 forward diffusion process과정에 적용이 되며, pre-trained auto encoder에 적용되며, size가 4 x 64 x 64인  latent space에 적용 된다고 합니다. 그리고 이 크기의 latent space의 경우, 512 x 512 해상도의 이미지를 latent space에 처리했을 때 다음과 같은 크기의 latent space에 처리가 된다고합니다.

optimizer 과정

optimizer: Adam

learning rate:2e-7

 step: 1000

fine-tune

step:1500

learning rate:5e-7

GPU: Tesla A100 한 장

한 장당 걸린 시간은 7분이라고 합니다.

## Experiments

---

![image.png](https://github.com/user-attachments/assets/95cd2db1-8140-4c93-894f-1facbde2748b)

다음은 실험 결과이자 다른 모델과의 성능을 비교해주는 부분입니다.

Imagic(Ours)의 경우 저자들의 모델이며, 비교 모델의 경우 Text2Live, DDIB, SDEdit 입니다.

저자는 이 사진을 통해서 다른 모델과 달리 원본 이미지의 배경이나 구성요소들은 그대로 유지하면서 우리가 수정하고자 하는 객체와 객체의 부분만 수정했다는 것을 보여주고 있습니다. 

![image.png](https://github.com/user-attachments/assets/5db00635-e7eb-4f82-a442-3de4c4bf22ee)

다음은 input image에 대해서 얼 만큼, text embedding interpolation에서 사용되는 tgt optimizer와 opt optimizer의 비율에 따른 이미지 수정 결과 입니다.

여기서  η값이 작을 수록 target embedding 즉, Target Text인 A photo of a pistachio cake라는 문장의 vector성분이 적게 반영이 됩니다. 그렇기 때문에 η값에 따른 반영이 잘 되었다는 결과를 보여주는 실험 결과입니다.

그리고 1번째 행의 경우 pre-trained 모델만을 사용하였을 때의 결과이며, 아래의 경우 3번째 과정인 fine tunning과 pre-trained모델 둘 다 사용하였을 때의 결과입니다. 

이 결과를 통해서 저자는 2번째 step과 3번째 step의 필요성 및 3번째 스텝을 스킵하였을 때의 문제점을 지적하며 이 두 과정을 모두 필수 적으로 진행해야 한다고 합니다.

![image.png](https://github.com/user-attachments/assets/e3615968-7abc-436f-92bf-ba280b5069fe)

마지막으로는  η비율에 따른 CLIP Score(target alingment)와 1-LPIPS(input image fidelity)간의 trade-off 표 입니다.

여기서 보시면  η비율이 높아질 수록 CLIP Score가 높아져 텍스트 내용 반영 점수가 높아지지만 그만큼 원본 이미지의 재현율은 굉장히 낮아지는 것을 볼 수 있습니다.

그리고 반대로  η비율이 낮아질 수록 CLIP Score는 낮아지고 텍스트 내용 반영 점수가 낮아지는 것을 확인 할 수 있습니다.

  

## Limitations

---

![image.png](https://github.com/user-attachments/assets/0093e804-0c45-4d5a-bded-c9b9d5508ddc)

한계 점으로써는, 위의 그림과 같이  실패 사례를 보여주면서 언급을 하였습니다.

첫 번째 언급으로써는, 편집이 굉장히 미묘하게 적용이 된다고 하였습니다.

위의 그림을 보면 1번째 도로 그림에서는 가장 큰 메인도로의 교통체증을 보여준게 아니라 가장 작게 보이는 좁은 도로에서의 교통체증을 나타냄

자동차 그림의 경우 단순히 원본 이미지 자동차에서 레이싱카 번호판만 붙여서 레이싱 카처럼 미묘하게 편집이 적용됨. 

    

두 번째  언급으로써는, 카메라 앵글의 각도나 줌의 정도와 같은 외부적인 요소가 이미지 수정에 있어서 영향을 미친다고 하였습니다.

이 부분에 대해서 자세히 좀 봐보도록 하겠습니다.

위의 예시 그림을 보면 뭔가 카메라 앵글이 원본 이미지랑 다르며 주변 배경 요소들과 target object의 크기를 비교하여 보니 카메라의 zoom의 정도가 차이가 나는 문제점이 발생하였다고 합니다.

이러한 경우를 저자는 편집이 제대로 적용이 되지 않았을 때 발생하는 현상이라고 지적하였습니다.

먼저 편집이 굉장히 미묘하게 적용이 되는 현상의 경우 η 비율이 증가하면 증가 할 수록 현상이 발생하게 된다고 합니다.

일반적으로 η 비율이 증가할 수록 우리가 원하는 결과를 수정 이미지를 얻게 되지만, 가끔 씩, 원본 이미지에서의 디테일 한 부분을 놓치게 되며 이러한 현상이 발견이 된다고 원인을 밝혔습니다.

카메라 줌이나 앵글 각도 문제의 경우,  일반적으로 우리가 원하는 수정 방향으로 수정이 이루어지기 전에 발생한다고 합니다. 그리고 이러한 부분에서 η값을 낮은 값에서 높은 값으로 점점 값을 높여가면서 편집이 이루어지기 때문에 이러한 문제를 해결하기에는 어렵다고 합니다.

이러한 이유에 대해서는 아무래도 diffusion process를 진행할 때 굉장히 많은 횟수의 diffusion proccess를 진행하고 denoising process를 진행하게 되는데 이게 처음부터 높은 값의 η이 아니라 낮은 값에서 높은 값으로 점차 진행되기 때문에 이러한 문제를 해결하기에는 피하기에는 어렵다고 합니다.  이 의미는 높은 값을 부여해서 원하는 방향으로 수정 되기전인 낮은 값을 부여하여 수정할 때 발생하기 때문이라고 합니다.

저자는 그래서 이 부분을 cross attention을 사용하여 조절하면은 풀 수 있지 않을까 라고 생각을 하며 향후 이 방법을 통해서 이러한 문제를 해결하는 방향으로 연구 진행을 할 예정이라고 합니다. 

Imagic의 경우 pre-trained text to image diffusion model을 사용하기 때문에 모델의 한계와 편향이 pre-train한 데이터에 어느정도 있을 수밖에 없으며, 원하는 편집을 하는데 있어서 기존 모델에서 실패한 사례의 편집 부분이라면 해당 저자의 방법을 적용하더라도 원치 않은 결과 물이 생성 된다고 합니다.   

또한 최적화를 하는데 굉장히 오랜 시간이 들어가기 때문에(논문에서 실험한 환경 기준으로 거의 이미지 한장 당 7분에서 8분이 걸림) 이를 앱이나 웹과같은 서비스에 적용되는 application으로 배포하기에는  조금 어려울 수 있다고합니다.
