# [데이터마이닝] 재난문자 유형별 분류 프로젝트
## 1. 배경 및 필요성

과도한 양의 재난문자로 인해 시민들의 피로도가 증가하고, 재난문자에 대한 신뢰도가 하락했다. 일부 시민들은 아예 재난문자 수신 기능을 해제해 놓기도 한다. 
  
## 2. 분석 목적

  수신자가 원하는 유형의 재난문자만 받아볼 수 있게 하기 위해, 재난문자를 각 유형별로 분류하는 것을 목적으로 한다. 
 
## 3. 사용 데이터 및 획득 방법

  행정안전부에서 제공하는 서울시 구청 재난문자 발송 현황 데이터를 활용했다. 공공데이터포털에서 획득했으며, 2020년 1월 ~ 2021년 1월 데이터, 2021년 2월 ~ 2021년 12월 데이터, 2022년 1월 ~ 2023년 8월 데이터 3개의 파일을 합쳐서 하나의 데이터프레임으로 만들었다.

## 4. 분석 과정
### 4.1 DBSCAN을 통한 클러스터링 진행 
- hyperparameter: eps는 0.01~10, min_samples는 5~60까지 바꾸면서 클러스터링을 진행했다.

Number of clusters: 6
merged_cluster
-1    7405
 1     572
 3     509
 0     447
 4     187
 2     147
 5      81

**클러스터명 | 내용**
0 일반적인 정보 나타냄 ('홈페이지', '블로그', '발생', '내용', '확인', '구청', '상세' )

1 역학 조사 클러스터 ('홈페이지', '블로그', '역학', '조사', '방역', '참조', '완료', '세부')

2 코로나 관련 공지 클러스터 ('발생', '바라다', '블로그', '코로나', '내용', '상세', '참조', '안내', '강서', '강서구')

3 이동 경로 및 일정 공지 클러스터 ('공개', '동선', '예정', '사항' )

4 방역 조치 및 마스크 클러스터  ('역학', '코로나', '조사', '방역', '준수', '마스크')

5 사적 모임 자제 클러스터 ('사고', '중구청', '접종', '모임', '사적')

DBSCAN은 많은 데이터들을 -1, 즉 noise로 처리함을 확인했으며,
적절치 않은 clustering 결과를 확인했다

### 4.2. 클러스터링을 통한 데이터 라벨링
- 계층적 클러스터링을 통해 데이터를 다음 8종류의 라벨로 라벨링했다.
 
**클러스터명 | 내용**

0   확진자 발생안내

1   기상 관련

2   백신, 교통, 확진자발생

3   전염병 임시선별소 관련

4   확진자 발생, 기상 관련

5   역학조사

6   전염병 검사 권장

7   방역 관련

 2번, 4번 클러스터의 경우 유형이 완벽하게 나누어지지 않는 문제가 있었다. 

### 4.2. 재난문자 유형별 분류
#### 4.2.1. 사용 모델
 분류 모델은 SVM, XGBoost, Random Forest, Catboost, 나이브베이즈를 사용했다.
 
##### 4.2.2. SVM
##### 4.2.3. XGBoost
##### 4.2.4. Random Forest
##### 4.2.5. Catboost
##### 4.2.6. 나이브베이즈
##### 4.2.7. 최적 모델 선정


