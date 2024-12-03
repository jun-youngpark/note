# 랭체인 개념
* LLM 애플리케이션 구축 프레임워크 (Python 기반)
`LangChain` 은 언어 모델을 활용해 다양한 애플리케이션을 개발할 수 있는 프레임워크를 말합니다. 이 프레임워크를 통해 언어 모델은 다음과 같은 기능을 수행할 수 있게 됩니다.

- 문맥을 인식하는 기능: LangChain은 언어 모델을 다양한 문맥 소스와 연결합니다. 여기에는 프롬프트 지시사항(instruction), 소수의 예시(examples), 응답에 근거한 내용(context) 등이 포함됩니다. 이를 통해 언어 모델은 제공된 정보를 기반으로 더 정확하고 관련성 높은 답변을
생성할 수 있습니다.
- 추론하는 기능: 또한, 언어 모델은 주어진 문맥을 바탕으로 어떠한 답변을 제공하거나, 어떤 조치를 취해야 할지를 스스로
추론할 수 있습니다. 이는 언어 모델이 단순히 정보를 재생산하는 것을 넘어서, 주어진 상황을 분석하고 적절한 해결책을 제시할 수
있음을 의미합니다.

LangChain 을 활용하면 **검색 증강 생성(RAG) 어플리케이션 제작**, **구조화된 데이터 분석**, **챗봇** 등을 만들 수 있습니다.
출처 : 위키독스 <랭체인LangChain 노트> - LangChain 한국어 튜토리얼🇰🇷

## 랭체인 사용 방법
* 랭체인 설치 , 랭체인-커뮤니티(3rd-party 도구 연동 기능)
* 

## 랭체인 구성
* 라이브러리, 템플릿
* LangServe (restapi 배ㅗ 라이브러리)
* LangSmith (디버그,테스트,평가,모니터링)
* LangGrapth (여러 계산 단게에서 다중 체인을 순환 방식으로 조정)

## LCEL
```
chain = prompt | model | output_parser
```
* 기호는 unix 파이프 연산자와 유사하며, 서로 다른 구성 요소를 연결하고 한 구성 요소의 출력을 다음 구성 요소의 입력으로 전달합니다.
```
# 주어진 나라에 대하여 수도를 묻는 프롬프트 템플릿을 생성합니다.
prompt = PromptTemplate.from_template("{country}의 수도는 어디인가요?")
# ChatOpenAI 모델을 초기화합니다.
model = ChatOpenAI(model="gpt-3.5-turbo-1106")
# 문자열 출력 파서를 초기화합니다.
output_parser = StrOutputParser()

# 프롬프트, 모델, 출력 파서를 연결하여 처리 체인을 구성합니다.
chain = prompt | model | output_parser

# 완성된 Chain 을 이용하여 country 를 '대한민국'으로 설정하여 실행합니다.
chain.invoke({"country": "대한민국"})
```

## Stremamit
