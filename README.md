# 한국어 뉴스 토픽 분류

공유 드라이브: https://drive.google.com/drive/u/1/folders/0AGAoF-nvVjYLUk9PVA
마감일: 2022년 2월 5일
상태: 진행 중
팀 노션 페이지: https://www.notion.so/4cf9eb18a70b4e5c925fb094d69496d2

## 목차

## 진행상황

- 전처리 & 형태소 분석 / 불용어 처리
- BERT Model Finetuning
- Hyperparameter tuning with optuna

[Google Colaboratory](https://colab.research.google.com/drive/1gTYv7WJ2txcI2Jm1rKYVPToRFQ-nk83x?usp=sharing)

- [ ]  local로 옮기기
    - [x]  pycharm...git...설치
    - [x]  우분투 비밀번호 재설정 ^^
        
        [https://mycup.tistory.com/286](https://mycup.tistory.com/286)
        
    
    boto3 install
    
    local 설치 한번만 제대로 해보자 ㅠㅠ
    
- [ ]  KoBERT이외의 다른 모델 사용 및 앙상블 시도
    - [ ]  HanBERT, HanElectra : binary classification
- [ ]  hyperparameter tuning : sequence model에서만 주로 진행..  굳이 할 필요 없을 듯
- [ ]  명사만 추출했을 때에 성능 차이 확인해보기
- [ ]  kobert보다 가벼운 모델...???
    
    bert (+ arranged bert 좀 더 가벼운걸로) 시도해보기
    
    DistilKoBERT (kobert 경량화)
    
- [ ]  모델간의 성능비교 목적 → seed 고정하고 돌려보기
- [ ]  시각화 (tensorflow board)

- 파이썬...버전..호환
    
    최신버전에 속하는 3.9를 사용해서 문제가 생긴것같다.
    
    특히 sentencepiece 0.1.83에서 파이썬 3.8 이상 지원을 안해주더라... (—VERSION not exist 오류)
    
    conda에서 downgrade된 가상환경을 생성했다.
    
    `conda create -n downgrade python=3.8 anaconda`
    
    `activate downgrade`
    
- ERROR: torch has an invalid wheel, .dist-info directory not found
    
    해결 방법
    
    > pip install torch===1.7.0 torchvision===0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
    > 
    
    버전은 알아서 수정해준다.
    

아니 근데 requirements 수정해도 겁나 안됨 미친

일단 다시 돌려놓고 하는중..

## 데이터 및 문제 상황

오픈 데이터 세트인 KLUE 데이터세트를 이용하여 다양한 언어 모델의 성능을 비교해 한국어 자연어처리 분야 발전에 기여

⇒ 한국어 뉴스 헤드라인 이용해 뉴스 주제 분류하는 알고리즘 개발

심사 metric : Accuracy

train_data.csv, test_data.csv

- index : 헤드라인 인덱스
- title : 뉴스 헤드라인
- topic_idx : 뉴스 주제 인덱스 값

sample_submission.csv

- index : test 헤드라인 인덱스
- topic_idx : 예측해야 하는 뉴스 토픽 인덱스 값

topic_dict.csv

- topic : 실제 뉴스 토픽
- topic_idx : 뉴스 토픽 인덱스 값

## 진행 방식

구글 드라이브에 

각자 작업한 ipynb 코랩 파일을 업로드할 것

이 때, 간단한 마크다운이나 주석을 달아주시면 너무...좋을 것 같습니다

(어떤 방식을 썼는지...!)

(fast text embedding을 사용했다 or gensim의 word2vec을 사용했다 등등)

### 모델

- seq2seq 안에 rnn / lstm / gru 써보는 것도 좋을 듯

### 시각화

- 토픽이 어떻게 분류가 되었는지 시각화해보는 것도 좋을 듯
- 분류 전 / 후 토픽 시각화

## **참고자료**

각자 공부하면서 알아본 참고 자료도 여기에 업로드 할 것

- 딥러닝을 이용한 자연어처리 : [https://wikidocs.net/30707](https://wikidocs.net/30707)
- [https://wikidocs.net/64517](https://wikidocs.net/64517)

- 베이스라인 (Dense Layer Model) :
    
    [[베이스라인 코드] 리더보드 제출 방법 (Simple Dense Layer Model)](https://dacon.io/competitions/official/235747/codeshare/2883?page=1&dtype=recent)
    
- huggingface
    
    [[Private 2nd] Huggingface를 사용한 베이스라인](https://dacon.io/competitions/official/235747/codeshare/3069?page=1&dtype=recent)
    
- Kobert
    
    [[Private 11위 / Public 0.867 KoBERT] TAVE_NLP팀](https://dacon.io/competitions/official/235747/codeshare/3062?page=2&dtype=recent)
    
    [[Private 24위/ public 0.85826/ KoBert 모델] Teddy팀](https://dacon.io/competitions/official/235747/codeshare/3082?page=1&dtype=recent)
    
- Fast text + Bi-LSTM
    
    [Bi-LSTM 기법을 이용한 한국어 뉴스 토픽 분류[CODE] - I am yumida](https://byumm315.tistory.com/entry/%ED%95%9C%EA%B5%AD%EC%96%B4-%EB%89%B4%EC%8A%A4-%ED%86%A0%ED%94%BD-%EB%B6%84%EB%A5%98-1-I-am-yumida)
    
- Kobert + Mecab
    
    [Private 32위, Public 점수 :0.82873, KoBert + Mecab](https://dacon.io/competitions/official/235747/codeshare/3074?page=1&dtype=recent)
    
- 토픽 모델링을 활용한 한국어 신문의 주제별 자동분류
    
    [토픽 모델링을 활용한 한국어 신문의 주제별 자동분류.pdf](%E1%84%92%E1%85%A1%E1%86%AB%E1%84%80%E1%85%AE%E1%86%A8%E1%84%8B%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%90%E1%85%A9%E1%84%91%E1%85%B5%E1%86%A8%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%85%E1%85%B2%201b87ce0cc9e14bd19e28961fd14eeeac/%ED%86%A0%ED%94%BD_%EB%AA%A8%EB%8D%B8%EB%A7%81%EC%9D%84_%ED%99%9C%EC%9A%A9%ED%95%9C_%ED%95%9C%EA%B5%AD%EC%96%B4_%EC%8B%A0%EB%AC%B8%EC%9D%98_%EC%A3%BC%EC%A0%9C%EB%B3%84_%EC%9E%90%EB%8F%99%EB%B6%84%EB%A5%98.pdf)
    
- 한국어 토픽모델링을 위한 단어 임베딩 활용 가능성 탐색
    
    [한국어 토픽모델링을 위한 단어 임베딩 활용 가능성 탐색.pdf](%E1%84%92%E1%85%A1%E1%86%AB%E1%84%80%E1%85%AE%E1%86%A8%E1%84%8B%E1%85%A5%20%E1%84%82%E1%85%B2%E1%84%89%E1%85%B3%20%E1%84%90%E1%85%A9%E1%84%91%E1%85%B5%E1%86%A8%20%E1%84%87%E1%85%AE%E1%86%AB%E1%84%85%E1%85%B2%201b87ce0cc9e14bd19e28961fd14eeeac/%ED%95%9C%EA%B5%AD%EC%96%B4_%ED%86%A0%ED%94%BD%EB%AA%A8%EB%8D%B8%EB%A7%81%EC%9D%84_%EC%9C%84%ED%95%9C_%EB%8B%A8%EC%96%B4_%EC%9E%84%EB%B2%A0%EB%94%A9_%ED%99%9C%EC%9A%A9_%EA%B0%80%EB%8A%A5%EC%84%B1_%ED%83%90%EC%83%89.pdf)
    
- LDA를 사용한 한글 데이터 토픽 모델링
    
    [LDA를 사용하여 한글 데이터 토픽 모델링하기](https://happy-obok.tistory.com/5)
    
- news title classification
    - use multiple bidirectional GRU/LSTM layers
    
    [https://github.com/andikarachman/News-Title-Classification](https://github.com/andikarachman/News-Title-Classification)