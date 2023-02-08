# 📄*줄거리 문맥 파악을 통한 영화 장르 자동 레이블링 시스템*📄
줄거리를 통해 장르를 예측할 수 있다는 가설에 대해서 검증을 진행

## ✔️*기획 배경*

<img width="421" alt="스크린샷 2023-02-09 오전 2 10 50" src="https://user-images.githubusercontent.com/62207156/217602226-49064da6-c66b-43a0-bdcb-be730de87406.png">

→ OTT 플랫폼 간의 경쟁이 치열해지면서 경쟁력을 갖추기 위해 추천시스템의 고도화를 진행함. 이를 위해서 정교한 태깅 작업이 필요하게 되었고, 사람을 고용해 직접 태그를 다는 작업을 함.

→ 영화는 갈 수록 쌓이고, 달아야 할 태그의 가짓수도 늘어날텐데...? 사람이 직접 태그를 다는 것은 인건비와 작업 소요시간에 있어서 비효율적임.

<img width="438" alt="스크린샷 2023-02-09 오전 2 15 31" src="https://user-images.githubusercontent.com/62207156/217603450-d177a036-6a50-4236-880a-7250f09ee8e7.png">

**=> 지금 가지고 있는 태그 데이터와 영화의 텍스트, 이미지, 오디오 등의 데이터를 조합하여 딥러닝에게 맡겨보자!**

## ✔️*데이터 셋*

<img width="348" alt="스크린샷 2023-02-09 오전 2 19 05" src="https://user-images.githubusercontent.com/62207156/217604263-eb8c7362-5311-478d-87a5-5b88492d949a.png">

- 개봉 년도 1901~2017까지 넓은 범위의 영화를 포함

## ✔️*데이터 전처리*

<img width="192" alt="스크린샷 2023-02-09 오전 2 20 42" src="https://user-images.githubusercontent.com/62207156/217604628-9289d68e-cd75-4d6f-a35e-17e3fda6af06.png">

→ 장르와 플롯 컬럼만 추출해 결측치 및 중복치 제거

### 장르 컬럼

<img width="277" alt="스크린샷 2023-02-09 오전 2 21 46" src="https://user-images.githubusercontent.com/62207156/217604907-68661222-355b-4619-95c3-976ce35ef487.png">

→ 2264개나 되는 가짓수를 가지고 있어서 확인해보니, 예시와 같이 나뉘어진 장르가 많아서 최대한 통합시킴. 최종적으로 빈도수 200 이상의 장르 총 17개로 추림.

### 플롯 컬럼

<img width="200" alt="스크린샷 2023-02-09 오전 2 23 50" src="https://user-images.githubusercontent.com/62207156/217605413-1bc55656-25a5-4cb8-874a-7144f2f198a5.png">

- 대문자는 소문자로 변환
- 's, \r\n, 특수문자, 불용어 제거
- 어간 추출 진행

## ✔️*모델 평가*

### 딥러닝에 사용될 모델은 **BERT**를 채택함

→ BERT는 양방향으로 학습을 하기 때문에 문맥 파악에 특히 강점을 가진 모델이므로 선정.

<img width="494" alt="스크린샷 2023-02-09 오전 2 26 39" src="https://user-images.githubusercontent.com/62207156/217606079-b6e64654-cc4b-4cd5-8408-7b175580cec7.png">

→ 전처리를 마친 데이터셋을 토큰화 및 패딩 처리까지 해서 BERT에 학습시킴.

### Chance Level = 1/17 = 0.0588

→ 장르 17개에 대한 분류이므로 찬스레벨은 1/17

<img width="500" alt="image" src="https://user-images.githubusercontent.com/62207156/217606462-0a644501-8d8d-4323-beae-6b82ad40de27.png">

→ 학습 및 검증 결과, 찬스레벨의 약 10배인 0.5의 정확도를 보임

<img width="500" alt="image" src="https://user-images.githubusercontent.com/62207156/217606687-932c0e0b-efdb-49f1-8679-8943c5e7d5c9.png">

→ 평가 데이터셋의 결과도 마찬가지로 0.5 수준을 보임

-----------------------------
`Python` `Google Colab` `EDA` `nltk` `BERT` `Tensorflow` `Keras`
