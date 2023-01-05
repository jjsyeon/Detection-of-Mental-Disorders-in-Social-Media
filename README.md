# 소셜미디어 정신질환 게시글 트렌드 분석 및 분류 모델 개발
* Capstone design 2022-1
* 소프트웨어융합학과 2019102130 정세연

## Overview<br>
* Problems<br>
  최근 정신질환을 겪고 있는 사람이 증가함에 따라 정신질환이 우리 사회가 해결해야 할 큰 문제로 이야기되고 있다. 
 현대인 정신질환에 해당하는 공황장애, 우울증, 조현병 이라는 말은 우리에게 더이상 생소한 단어로 느껴지지 않는다. 
 하지만 정신질환을 겪는 대다수의 사람들은 본인들이 정신질환을 갖고 있다는 사실을 인지하지 못하거나 인정하지 못 하는 경우가 많고, 본인이 정신질환을 겪고 있다는 사실을 알더라도 쉽게 치료를 받으러 다니지 못하는 경우가 많다. 주변의 시선으로 인해 쉽게 치료를 받지 못하는 경우가 많은데, 이 문제 상황을 온라인을 적극 활용하면 개선이 가능할 것이라고 생각하였다.
 * Goals<br>
 이번 프로젝트에서는 온라인 SNS상의 게시글을 분석하여 그 특성을 파악하고 여기서 얻은 인사이트를 바탕으로 정신질환 예측 모델을 개발한다. 
 텍스트 내의 감정 지표를 기준으로 점수를 측정하고 해당 데이터의 특성을 분석하고 이를 활용하여 트렌드 분석을 한다. 
 활용되는 감정 지표는 긍부정에 해당하는 Valence값과 흥분정도에 해당하는 Arousal, Emotion Catagory(Anger, Anticipation, Disgust, Fear, Joy, Surprise, Sadness,Trust) 에 대한 Intensity가 있다. 
여러 감정 지표에 대해 분석하여 정신질환 여부를 판단하는데 중요한 지표를 파악한다. 트렌드 분석에서는 주기성을 분석하여 어느 시간대에 어떤 감정 지표 점수가 높은지를 분석한다.
 이를 통해 정신질환 예측 모델을 개발하고 더 나아가 정신질환의 정도, 위험성을 나타내는 지표를 탐색하려 한다.

## Dataset
1. SNS(Reddit) 게시글<br>
    - Mental Disorder dataset
      * Depression subreddit 
      * Bipolar Disorder subreddit
      * Panic Disorder (with Panic Attack) subreddit
      
    - Non-Mental Disorder dataset
      * Covid19 subreddit
      * Teaching subreddit
      * Relationship subreddit
<br>

2. Arousal-Valence Lexicon / motion Category Intensity lexicon<br>
    - Tweet Emotion Dynamics: Emotion Word Usage in Tweets from US and Canada(https://arxiv.org/abs/2204.04862)
    - 사전 데이터셋의 신뢰성 검증을 위해 Emotion Valence-Arousal Space를 그리고 이론에 부합하는지 확인
    <br>에서 제공하는 Emotion word Dataset 활용.
    <br>![무제](https://user-images.githubusercontent.com/65614582/174294352-9e881386-4301-4f33-91c6-1192b6e0824e.png)![무제](https://user-images.githubusercontent.com/65614582/174294377-e6bb28f5-0e37-4ad9-bbf9-498a2143ec1c.png)
<br>

## Emotion Scoring Algorithm<br>
* V-A Lexicon Scoring Algorithm<br>
    - 기존 감정 점수 Scoring Algorithm 개선
    - 부정, 강조 등의 문맥적 요소 고려
    - 가장 유사도가 높은 단어로 매칭
  
  <p align="center"><img width="705" alt="무제 2" src="https://user-images.githubusercontent.com/65614582/174298698-84c0bc38-098b-43c5-afb0-f7efdceebf9e.png">
  
    - 평균 감정 점수 아닌 긍/부정 독립적 처리
  <p align="center"><img width="707" alt="무제 2" src="https://user-images.githubusercontent.com/65614582/174299225-6d8942d4-bcf9-4f95-a1d6-1aeecb3f287d.png">


*  Emotion Category Intensity Scoring Alorithm<br>
    - 텍스트 내의 Emotion Category 별 Intensity 측정
    - 코로나 19 데이터셋 기준으로 정신질환 비정신질환이 반대의 특성을 보인 Frear, Trust
    
    <p align="center"><img width="493" alt="무제 2" src="https://user-images.githubusercontent.com/65614582/174300202-32db4a4b-7298-4a23-9606-07a2734695a2.png">

      
## Trend Analysis <br>
> 정신질환에 대한 코로나19 영향 분석. 다음과 같이 기간을 나누어 분석.<br>
> 1. pre - pandemic (2018.3~2019.12)
> 2. mid - pandemic (2020.1~2021.7)
> 3. post - pandemic (2021.8~2022.3)
<br>

* 게시글 수 분석 시기 별 비교 <br>
    - 코로나19 게시글 수 비율이 증가하는 추세임
    - 코로나 관련 게시글 수는 r/covid뿐만 아니라 r/mental에서도 크게 증가
    
  <p align="center"><img width="700" alt="image" src="https://user-images.githubusercontent.com/65614582/210776224-b45a2b95-eac4-45d0-b9d9-913b126aa192.png">


* 감정 점수 및 주제 분석 결과 시기 별 비교<br>
    - mid-pandemic 시기에 정신질환 게시글의 변화가 큼
    - mid-pandemic : 패닉, 외로움, 음모에 대한 변화량이 높음
    - post-pandemic : 건강 전반에 관련된 주제 (r/healthanxiety, r/fitness)에 대한 변화량이 높음
    
  <p align="center"><img width="700" alt="image" src="https://user-images.githubusercontent.com/65614582/210776590-5405762b-1c68-41af-bae3-8f60689695f7.png">

## Mental Disorder Detection Model<br>

1. 모델의 종류
    - 점수 학습 모델
        * SVM
        * 감정 단어 개수, 감정 점수 (Low Valence/Arousal Score, Fear/Trust Intensity Score), 토픽 점수 학습
          
    - 문장 학습 모델
        * Bi-LSTM 모델
        * 게시글 문장 데이터 학습
    
    - 점수 및 문장 학습 모델 
        * 점수 학습 모델(3-Dense Layer)와 문장 학습 모델(Bi-LSTM) 병합한 모델
        * 게시글 문장 데이터, 점수 데이터(감정 단어 개수, 감정 점수 :Low Valence/Arousal Score & Fear/Trust Intensity Score, 토픽 점수) 학습
    
   <p align="center"><img width="500" alt="image" src="https://user-images.githubusercontent.com/65614582/210784347-e81a4b06-81f4-44e0-a604-15d7c50abdb2.png">
     
2. 성능 평가
     - Binary Classification Model
          * 일반 데이터셋에서 특정 하나의 정신질환 subreddit을 ‘mental’ class로 분류
          * 8개의 정신 질환 subreddit 각각에 대한 분류 모델
     
     - Multi-class Classification Model
          * 8가지의 정신질환 게시글 각각에 대해 모두 분류하는 다중 분류
          * non-mental class를 포함하여 총 9가지 class로 분류

  <p align="center"><img width="423" alt="image" src="https://user-images.githubusercontent.com/65614582/210791703-3c8fdcd2-305e-4732-a1e9-6d7f48c2bccb.png">


 ## Conclusion<br>
 코로나19를 기준으로 소셜미디어 상의 정신질환 게시글 트렌드 분석하고 이를 통해 정신질환 검출 모델 성능 개선함.<br>
 본 연구를 바탕으로 정신건강에 영향을 미칠 수 있는 사회 현상을 기준으로 정신질환 게시글의 특성을 파악하여 적합한 정신건강 검출 모델을 개발할 수 있을 것이라 생각함.
    
    
