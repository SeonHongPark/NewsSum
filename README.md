# NewsSum
KoBart&amp;ET5를 활용한 뉴스 음성요약 AI스피커 및 웹 서비스

## 기간
2022/05/02 ~ 2022/06/07

## 프로젝트 설명
최근 짧은 시간 내에 정보를 얻고자 하는 서머리 컨텐츠에 대한 수요가 증가함에 따라 시간은 없지만, 주요 뉴스를 알고 싶은 타임푸어족 혹은 직장인을 대상으로 매일 주요 토픽에 대한 뉴스를 선별하고 요약하여 읽어주는 서비스를 구현하기 위한 프로젝트

## 방법
1. Raspberry Pi를 및 STT를 사용해 키워드, 뉴스 주제를 받은 후, 해당 뉴스 요약문을 google TTS 및 스피커로 출력
2. FAST API를 사용하여 뉴스를 요약해주는 웹 페이지 구현

## 상세 과정
1. 라즈베리파이 4에 음성 입력 시 STT를 활용하여 텍스트 입력
2. 뉴스 기사 크롤링
- 연예,스포츠,정치등 6개 분야 네이버 뉴스 메인페이지에 있는 순서로(중복 제거) 6개씩 30분마다 크롤링(beautifulsoup4)
- ‘xxx 키워드 검색‘ 입력 시 xxx를 검색 후 가장 댓글이 많은 관련 뉴스 크롤링(Selenium)
3. 크롤링한 뉴스 기사 전처리 후 Kobart 모델에 입력 및 요약기사 생성
4. 기사 본문, 언론사, 요약 뉴스등 7개의 정보 RDS(mariadb)에 적재
5. FastAPI로 뉴스 주제 음성 입력시 해당 주제 뉴스 기사 요약문 3개 or 검색하고 싶은 키워드 음성 입력시 해당 기사 요약문 1개를 response 하는 api 생성
6. 라즈베리파이 4에 해당 api 호출 함수 생성
7. 요약 뉴스를 Google TTS를 사용해 출력
8. HTML & CSS 활용 FastAPI 웹 페이지 구현

## 인원 및 역할
- 총원: 5명
- 역할: 크롤러 구현 및 DB구축, 모델 평가, 스피커 구현

## 상세 역할
### 1. 네이버 뉴스 크롤링
- 특정 주제(정치, 경제, 스포츠, 연예, 사회, 생활/문화) 및 키워드에 대한 네이버 뉴스를 beautifulsoup4를 활용하여 주기적으로 크롤링
- 크롤링 한 뉴스 기사 원문 데이터 KoBART로 모델링 후 요약문 생성
- 뉴스 원문 + 요약문 RDS에 적재

### 2. 모델링
- 성능 평가 지표 분석 및 확인
- KoBart 및 ET5의 Transfer Learning 후 성능 확인

### 3. 스피커 구현
- FastApi에서 뉴스 주제, 키워드 검색 시 요약문을 반환하는 기능 구현
- Google TTS를 사용하여 Raspberry Pi4에서 만들어진 api 호출 후 response된 요약문을 TTS로 출력하는 함수 생성

### 4. DB구축
- Amazon Aws를 활용하여 MariaDB 환경 구축

## 사용 기술 스택
![image](https://user-images.githubusercontent.com/93495435/216268844-1fc5e08d-6949-4806-8008-183b87c83316.png)

## 아키텍쳐
![image](https://user-images.githubusercontent.com/93495435/216268930-ae664835-c1dd-4be2-a293-df35e8ba8133.png)


## 프로젝트 결과
### AI-Speaker & NewsSum 시연 영상

스피커 시연
https://www.youtube.com/watch?v=i5SYENVIA4M

홈페이지 시연
https://www.youtube.com/watch?v=gvhjLhK6EMc

## 개선사항
- T5 모델 사용 시 주어가 생략되는 문제 해결
- 시간, 날짜 단위 뉴스 출력 서비스 구현
- KoElectra와 같은 다른 요약 모델 성능 측정 및 모델링 구현
- 영문 뉴스 번역 서비스로 확장
- 현재 룰 기반의 키워드 검색을 AI를 활용한 검색 기반으로 고도화
