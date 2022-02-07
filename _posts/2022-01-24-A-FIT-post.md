---
layout : post
title : A FIT 프로젝트
subtitle : Project
gh-repo: junhong625/A_FIT
gh-badge: [star, fork, follow]
tags : [Project]
comments: true
---

# 내 손 안의 헬스트레이너(A FIT)

##### 인공지능을 활용한 운동자세 교정

>A FIT은 언택트 시대에 사용자들이 인공지능을 활용해 비대면으로 자세 교정을 받고 안전하게 운동할 수 있도록 도와주는 어플리케이션입니다.

* * *

## A FIT의 특징
- 나만의 공간에서 언제든 쉽게 올바른 자세인지 확인이 가능(피드백 제공)
- 포즈 디텍션(Pose Dectection) 기술을 활용한 운동자세 분류 기능
- 다양한 운동 자세들을 주요 관절 부위별로 분석
- 사용자가 올바른 자세로 운동할 수 있도록 피드백을 제공 -> 부상 예방↑

* * *

## 사용 방법

**1. 로그인**
* 구글 로그인 또는 회원가입을 진행 가능
<p align="left">
<img src = "https://user-images.githubusercontent.com/83000975/150528018-38bfd573-7838-425e-929a-4698495f2040.png" width="200" height="400" />
  </p>

* * *


**2. 메인화면**
* 자세 분석, 운동자세 학습, 로그아웃의 기능이 있습니다.
<p align="left">
<img src = "https://user-images.githubusercontent.com/83000975/150529056-0bfef46e-dc69-4156-bd9b-5e26bf8ccdb0.png" width="200" height="400" />
  </p>

* * *

**3. 자세분석**
* 사용자가 본인의 운동자세에 대한 피드백을 받을 수 있습니다.(스쿼트와 플랭크 자세 분석 가능)
<p align="left">
<img src = "https://user-images.githubusercontent.com/83000975/150529354-bbda87e9-411f-4ec2-81ea-09d68906ffa7.png" width="200" height="400" />
<img src = "https://user-images.githubusercontent.com/83000975/150529388-2d59493f-8c91-48fd-89e2-4fcca19e9597.png" width="200" height="400" />
  </p>

* * *

**4. 운동 자세 학습 기능**
* 각 운동자세마다 올바른 운동 방법에 대해 학습할 수 있습니다.
<p align="left">
<img src = "https://user-images.githubusercontent.com/83000975/150529996-e5885097-2557-4633-b822-29c672713632.png" width="200" height="400" />
<img src = "https://user-images.githubusercontent.com/83000975/150529997-0ea6fb1b-6b68-4712-9fc2-c1e65d42ad28.png" width="200" height="400" />
  </p>

* * *

## Project Sturcture
* Android Studio + Xcode + Django(Rest API Server) + Data Processing & AI modeling(MediaPipe&CNN)구조로개발했으며, 저는 Data Processing&AI modeling 을 담당했습니다. 
* Jupyter Notebook을 사용하여 진행했고 제가 사용한 기술스택은 다음과 같습니다.

- Python
- Mediapipe<img src="https://user-images.githubusercontent.com/83000975/150539318-897a4b2d-494c-4543-b6ad-2b0f35f45551.jpg" width="100" height="20">
- Tensorflow(CNN)<img src="https://user-images.githubusercontent.com/83000975/150538372-02d09225-934c-4984-a80b-09e7f7ae9cc1.jpg" width="100" height="20">
- AWS(EC2)
- Ubuntu(20.04 LTS)
- Matplotlib
- Image Generator
- OpenCV
- Pandas
- Numpy
- PIL

**■ 프로젝트에서는 Data Processing&AI modeling / 기획 / 설계 / 일정관리 등을 담당했습니다.**

* * *

## MediaPipe
* 인공지능 학습에 사용할 skeleton 이미지 데이터를 생성하기 위해 MediaPipe의 Pose 기능을 이용하였습니다. 
* 이 기능을 이용하여 주요관절 부위의 좌표값을 얻어냈습니다.


- **손목(WRIST), 팔꿈치(ELBOW), 엉덩이(HIP), 어깨(SHOULDER), 무릎(KNEE), 발목(ANKLE), 뒤꿈치(HEEL), 발(FOOT)**
<img src="https://user-images.githubusercontent.com/83000975/150537216-6ec9ccb2-9781-488c-be7f-400422432ea9.png">

* MediaPipe를 이용하여 얻은 주요 관절 부위의 좌표값을 matplotlib을 이용하여 아래와 같이 skeleton 이미지로 변환하였습니다.


<img src="https://user-images.githubusercontent.com/83000975/150537494-13740fe4-ab6a-4516-96ff-583e07746694.png">


[**MediaPipe를 활용한 이미지 데이터 생성 코드** -> [Link](https://github.com/junhong625/A_FIT/blob/%EC%95%88%EB%8D%95%EA%B5%AC/Data%20processing%26AI/Data%20processing/image_skeletonize.py)]

* * *

## Tensorflow(CNN)


* <img src="https://user-images.githubusercontent.com/83000975/150538372-02d09225-934c-4984-a80b-09e7f7ae9cc1.jpg" width="100" height="20">를 이용하여 CNN학습을 진행했습니다.


```
model=Sequential()
model.add(Conv2D(filters=50,kernel_size=3,padding='same',activation='LeakyReLU',input_shape=(600,600,3)))
model.add(Conv2D(filters=40,kernel_size=3,padding='same',activation='LeakyReLU'))
model.add(MaxPool2D(pool_size=(4,4)))
model.add(Conv2D(filters=40,kernel_size=3,padding='same',activation='LeakyReLU'))
model.add(Conv2D(filters=30,kernel_size=3,padding='same',activation='LeakyReLU'))
model.add(Conv2D(filters=20,kernel_size=3,padding='same',activation='LeakyReLU'))
model.add(Conv2D(filters=10,kernel_size=3,padding='same',activation='LeakyReLU'))
model.add(MaxPool2D(pool_size=(4,4)))
model.add(Flatten())
model.add(Dense(50,activation='LeakyReLU'))
model.add(Dense(20,activation='LeakyReLU'))
model.add(Dense(10,activation='LeakyReLU'))
model.add(Dropout(0.5))
model.add(Dense(3,activation='softmax'))
model.compile(optimizer='adam', 
             loss='categorical_crossentropy',
             metrics=['acc'])
model.summary()

history=model.fit(lst_im,lst_label,epochs=20,
                 batch_size=64,
                 validation_data=(x_val,y_val))
```

* **99%의 정확도를 가진 자세 분류 모델을 생성했습니다.**


[**CNN학습 코드** -> [Link](https://github.com/junhong625/A_FIT/blob/%EC%95%88%EB%8D%95%EA%B5%AC/Data%20processing&AI/AI/CNN.py)]

* * *

## AWS EC2(Ubuntu 20.04 LTS)
*  GPU를 사용한 빠른 학습을 위해 AWS EC2(Ubuntu 20.04 LTS) 환경에서 학습을 진행
- 인스턴스 : g3.4xlarge
- GPU : M60
- 사용 라이브러리 : tensorflow-gpu
