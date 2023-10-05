# AI를 통한 Cocktail Service

## 제공하는 서비스


1. 마음에 들었던, 칵테일 이름 입력시, 유사한 칵테일이 무엇인가?
2. 칵테일의 재료를 입력을 할 경우, 만들 수 있는 칵테일은 무엇인가?
3. 칵테일 사진 업로드시, 이 칵테일이 무엇인가를 알려준다.
4. 마찬가지로 이미지를 이용해서, GAN을 이용한 화풍 변경.

사용한 기술
filebeat, logstash, elasticSearch, kibana, python

## 프로젝트 아키텍쳐

![architecture](Architecture_Font.pdf)


### 1. 왜 엘라스틱을 사용을 했나?
실시간 수집에 최적화가 되어있다고 판단을 했다.


### 웹 수집의 이유
빅데이터 프로젝트를 진행을 하면서, 가장 어려웠던 점은 데이터 수집입니다. 좋은 아이디어는 개인정보가 포함되어 있거나, 회사가 서비스를 운영을 하면서, 축적을 해온 데이터인 경우가 많았습니다.

그래서, 프로젝트를 진행을 할 경우 개인적으로 수집 할 수 있는 파이프라인을 구축하고 싶었습니다.

### 웹 수집 방법
웹으로 접속을 하는 것은 nginx에서 listen하고 있는 80번 포트로 접속을 한다는 것을 의미합니다.
nginx는 접속을 하는 클라이언트의 기본정보를 access.log로 저장을 하게 됩니다.

filebeat로 해당 로그가 발생을 하는 위치를 특징 짓고 logstash와 통신을 하고 logstash는 elasticSearch로 데이터를 전송합니다.

이런 식으로 가지고 싶었던 개인적인 데이터를 수집할 수 있게 했습니다.

### 정확도를 계산하는 독특한 방식
엘라스틱에서는 관계형 DB와 다르게 정확도를 계산해서 결과를 출력합니다. 그렇기에 편리한 경우도 있을 듯 해서, 선택을 했습니다.

### 파이썬과의 호환성
엘라스틱과 파이선과의 호환성을 도와주는 Python Elasticsearch Client 모듈을 활용해서, 서비스를 구축을 하는데 편리할 듯 하여 선택을 했습니다.




