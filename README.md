# GoSummary
Summarize the articles about keyword using various graphs

### 2018.01.16 프로젝트 모임

### 기술 스택

1. 스파크

2. ELK 엘라스틱서치, 로그스태쉬, 키바나

3. 서버

4. 도커

5. mariaDB, mysqlDB

6. zeppelin

### 아이디어

어떤 키워드 검색 시에, 전체 언론사 데이터를 기반으로 특정 년월일에 급증하는 단어, 비중 각 언론사별로 그래프 표시. 단어 선택시 링크 제공

기업 검색인 경우 다트 사이트 링크 제공

전체 데이터 일자 내에서 급증하는 시점, 그 단어 제공

각 언론사별로 그 키워드와 함께 어떤 단어를 많이 사용하였는지 분석

- 한 줄 정리 : 검색 시에 먼저 볼 수 있는 요약페이지 생성 효과

- 네이버 연관검색어와의 차이점 : 어떤 키워드에 대한 관련 검색어는 볼 수 있지만, 구체적인 시점은 알 수 없고, 사전에 기간을 알고 있어서 기간 설정을 하고 검색하지 않으면 너무 데이터가 많이 나와 요약해서 보기 힘들다

- 구글트렌드(네이버 데이터랩)와의 차이점 : 어떤 키워드가 얼마나 많이 검색되었는가만 보여줌.

- 개발 목표 : 어떤 키워드에 대해서 먼저 한 눈에 볼 수 있는 요약 정보 페이지를 목표로 한다.

### 프로젝트 제목

미정

### 기술 적용

- 개발환경 구축 : Docker를 활용하여 Spark, Elastic Search, MariaDB, Zeppelin 환경구축

- 수집 : Crawling by Java or Python

- 저장 : Elastic Search로 담기

- 분석 : Spark로 형태소분석 ( https://github.com/uosdmlab/spark-nkp )

- 서버 : AWS- DB   : 분석 결과를 MariaDB에 저장

- 시각화 : Zeppelin

- 서비스 : 카카오톡API or Application

### 추가논의
1. 블록체인의 추가 적용은 추후 논의

### 2018.01.17
### 진행상황 - 개발환경구축
1. Docker image 생성 및 배포
 - ubuntu:16.04 version을 기반으로 Spark v2.2.0 설치완료.
 
 “`
  docker pull ubuntu:16.04
  “`
  
  “`
  root@8bb26156f9cd:/#apt-get update
  “`
  
  “`
  root@8bb26156f9cd:/#apt-get install -y wget
  “`
  
  “`
  root@8bb26156f9cd:/#wget http://apache.mirror.cdnetworks.com/spark/spark-2.2.0/spark-2.2.0-bin-hadoop2.7.tgz 
  “`
  “`
  root@8bb26156f9cd:/#tar xvzf spark-2.2.0-bin-hadoop2.7.tgz
  “`

  “`
  docker commit 00dfba2b0327 goSummary
   “`

   “`
   docker tag gosummary ssyth19/gosummary:01
  “`
 
   “`
   docker push ssyth19/gosummary:01
   “`
 - 위와같은 과정을 통해 이미지 업로드 완료
2. Docker image를 다운받기 위해선 다음과 같은 명령어를 사용
 
  “`
   docker pull ssyth19/gosummary:01
   “`
 - 다운받은 이미지를 실행한다.

  “`
   docker run -i -t ssyth19/gosummary:01 /bin/bash
   “`
   
3. Docker내에 엘라스틱서치 설치완료

 - 추후 나머지 환경들도 구축완료할 예정
