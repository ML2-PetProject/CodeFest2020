# CodeFest2020

## 🐶강아지를 부탁해!🐶

해당 프로젝트는 [KC-ML2](https://www.kc-ml2.com/)에서 개최한 [CodeFest2020](https://blog.kc-ml2.com/codefest2020/)에 참가하여 진행한 내용입니다.

## 프로젝트 목표

![Untitled](https://user-images.githubusercontent.com/58431910/92466937-cd3b5080-f20b-11ea-8b46-587b4a1a1571.png)

- 1인 가구, 저출산·고령화 현상으로 매년 반려동물을 키우는 가구수가 늘어나면서 관련 시장 규모 또한 상승세에 있다. 그러나 반려견에 대한 기본적인 지식 없이 반려견을 키우는 사람들 역시 증가하고 있다.

![Untitled-2](https://user-images.githubusercontent.com/58431910/92466991-e04e2080-f20b-11ea-8496-6d99d61a7e3d.png)
- 위의 표에서도 보이듯, 그로 인해 보호자가 반려 동물을 통제하지 못하여 다른 사람을 공격하는 등의 사고가 빈번하게 발생하고, 소통 및 훈육 문제로 인한 반려동물 파양, 유기, 학대 문제가 잦아지고 있다. 그렇기 때문에 반려 동물에 대한 전문적인 훈련이 필수적이지만, 그 금액 또한 만만치 않기 때문에 쉽사리 받을 수 없는  현실이다.
- 이러한 문제들을 해결하기 위해 우리는 반려견의 행동을 분석하여 현재 감정 상태 또는 이상 행동의 원인 및 해결 방법에 대해 알려주는 서비스를 만들고자 한다.

## 사용한 Training Data

- 이미지 데이터를 이용하여 강아지 행동 파악을 위한 기계학습 진행
- 파이썬 크롤러를 만들어 google에 있는 이미지를 크롤링함
- 약 9,000장의 이미지 사용

## 프로젝트 진행 내용

Background

- 반려견의 행동을 나타내는 여러가지 태그들 중 학습에 사용할 태그들을 따로 분류하였다.
- Azure Custom Vision에 사용할 태그들을 만들어 각 태그마다 최소 100장 이상의 이미지를 업로드 하였다.
- 기계학습이 제대로 이루어 지기에 적절하지 않은 사진들의 경우 삭제하였으며, 하나의 사진이 여러개의 태그 항목에 속하는 경우 그 이미지에 해당하는 태그들을 모두 추가해 주었다.
- 분류가 완료되면 Training을 시킨 후, 정확도를 확인하고 이 과정을 반복하며 계속하여 학습을 진행하였다.

Try1

![Untitled-3](https://user-images.githubusercontent.com/58431910/92467193-230ff880-f20c-11ea-9480-a69d6372fbdd.png)

- 위 사진의 keyword들을 기준으로 크롤링한 후, 추가적으로 떠오르는 태그들을 즉석해서 추가하였다.
- 이미지 데이터 및 태그들이 균일하지 못하였고, 그림만 보고 판단하다 보니 정확한 기준이 없어 정확도가 현저히 떨어졌다.

Try2

- 강아지의 감정을 분석하는 모델을 만들기 위하여 감정들(ex. happy, sad, angry, ...)을 태그로 하여 이미지 데이터를 정리하였다.
- 사람의 눈으로 강아지 사진만 보고 감정을 분류하기 쉽지 않아 정확도가 떨어졌다.
- 같은 감정이어도 해당하는 행동이 다양하여 학습에 도움이 되지 않았다.

Try3

- 확실한 기준으로 데이터를 분류하기 위해 정확한 pose를 기준으로 태그를 선정하였다. (ex. scratching, belly rub, ...)
- 강아지 사진의 태그들을 input으로 하여 감정을 output으로 뽑아내는 DL 모델이 추가로 필요하다.
- 추후에 영상 데이터에서 keyword들을 뽑아낼 때도 해당 모델을 사용하면 도움이 될 것이다.

## 학습을 위해 사용한 Tags

총 29개의 Tag를 사용하였다.

- [ ]  barking
- [ ]  belly rub
- [ ]  growling
- [ ]  head tilt
- [ ]  howling
- [ ]  lowered ear
- [ ]  lying
- [ ]  mounting
- [ ]  nose lick
- [ ]  peeing
- [ ]  pooping
- [ ]  running
- [ ]  scratching
- [ ]  shake off
- [ ]  sit back
- [ ]  sit down
- [ ]  sit up
- [ ]  sleeping
- [ ]  sleepy eye
- [ ]  smiling
- [ ]  sniff ground
- [ ]  standing
- [ ]  standing up
- [ ]  staring
- [ ]  stretching
- [ ]  tongue out
- [ ]  walking
- [ ]  whale eye
- [ ]  yawn

## AZURE Custom Vision 사용

<img width="775" alt="_2020-09-07__11 55 07" src="https://user-images.githubusercontent.com/58431910/92467252-3ae77c80-f20c-11ea-9505-f39b11256228.png">

- Azure Custom Vision 서비스를 이용하여 위에 정리해둔 키워드들을 tag로 만들어두고 각각의 태그에 해당하는 이미지들을 업로드하여 학습을 진행하였다.
- 각각의 태그 안의 이미지들을 지우거나 다른 태그로 이동시키고, 필요없는 태그라는 판단이 든 경우 태그도 삭제하며 학습을 진행하였다.

## Model Test

<img width="830" alt="_2020-09-08__12 04 23" src="https://user-images.githubusercontent.com/58431910/92467291-4d61b600-f20c-11ea-9688-3078ff421d1a.png">

- 초기, 태그의 개수가 많지 않았을 때(8개)는 다소 높은 정확도를 보여주었다. 하지만 이 경우, 설령 정확도는 높게 나오더라도 다양한 강아지의 행동을 분석하기는 어렵다고 판단하여 태그의 갯수를 늘려보았다.

<img width="816" alt="_2020-09-08__12 06 30" src="https://user-images.githubusercontent.com/58431910/92467325-5c486880-f20c-11ea-8550-efe0153f6bf4.png">

- 그러나 태그의 수를 늘리면서 학습을 진행하였더니 점점 정확도가 감소하였다. 태그 별 정확도를 분석해 보았을 때, 한 태그에 사진의 갯수가 200개 이하인 항목들이 대체로 정확도가 낮은 경향을 보였고, 혹은 사진의 갯수가 많더라도 태그 별 정확도는 낮은 것도 있었다. 그래서 전자의 경우, 크롤링을 추가적으로 진행하여, 사진의 갯수를 늘렸고, 후자의 경우, 선별 작업을 한 번 더 진행하였다.

## TensorFlow Model 응용

- Azure를 통해 학습된 TensorFlow 모델을 내보내 파이썬언어로 Jupyter Notebook에서 모델을 실행하여 이미지를 입력하면 그에 해당하는 상위 5개의 키워드를 뽑아주는 코드를 작성하였다.

<img width="900" alt="스크린샷 2020-09-08 오후 7 56 03" src="https://user-images.githubusercontent.com/58431910/92467987-661e9b80-f20d-11ea-8030-e3a32d477224.png">

- 모델과 코드들이 위치한 파일에 이미지 파일을 저장하고 위와 같이 이미지 파일명을 입력한 뒤 실행시킨다.

![test](https://user-images.githubusercontent.com/58431910/92468808-b4806a00-f20e-11ea-812b-c6b0e187a5e3.jpg)

- 현재 이용한 이미지파일이다.

<img width="816" alt="스크린샷 2020-09-08 오후 7 55 38" src="https://user-images.githubusercontent.com/58431910/92467975-61f27e00-f20d-11ea-8ec6-617b35120c97.png">

- 실행후 위와같이 상위 5개의 tag가 순서대로 뜨는것을 확인할 수 있다.


