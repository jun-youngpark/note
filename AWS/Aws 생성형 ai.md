# 생성형 AI Application 구현을 위한 5가지 패턴

## 프롬프트 엔지니어링
* 커스텀 불가
* 대규모 언어 모델(Large Language Models, LLMs)과 시각-언어 모델(Vision-Language Models, VLMs)의 출력을 최적화하기 위해 입력 프롬프트를 설계하고 구조화하는 기술이다.
* 모델 파라미터를 수정하지 않고도 특정 작업에 대한 모델의 성능을 향상시키는 것을 목표로 한다.


## 검색 증강 생성 (RAG)
* 커스텀 가능
* 대형 언어 모델의 성능을 데이터베이스를 검색하여 개선하는 기술이다. 정보 검색 프로세스의 한 유형이다.
* Native Rag : Query -> semantic search -> response
* Advanced Rag : query -> semantic search(유사도 검색) , lexical search(키워드 검색) -> Rank-Fusion - > Reraker ->chunk 1,23, -> Parent Cunk1,2 -> Response
* 

## 에이전트 (Agent)
* 외부시스템과 상호작용한 시스템  
* 추론 + 액션(명령)까지 진행
  

## 모델 파인 튜닝
* 파인튜닝(정확도 올리기 , 소수의 라벨링을 샘플 데이터를 가지고 특정 작업 정확도 극대화)
* Pre 트레이닝(사전에 학습)

## 베이스 모델 훈련
* 모델을 구축
