# 📅 Development Log

## Day 1 - 프로젝트 환경 구축 및 데이터 전처리

**프로젝트명:** PickWise
**목표:** League of Legends 밴픽 추천 시스템 개발을 위한 데이터 이해 및 전처리

---

## 📌 오늘의 목표

* 프로젝트 개발 환경 구축
* Kaggle LoL 데이터셋 구조 파악
* 테이블 간 관계 이해
* 분석을 위한 전처리 수행

---

## 🛠 개발 환경 구축

### 개발 환경 설정

* Python 가상환경(venv) 생성
* VS Code 및 Jupyter Notebook 환경 구성
* 프로젝트 폴더 구조 설계
* GitHub Repository 생성
* Rainbow CSV 확장 프로그램 설치

### 프로젝트 구조

```
PickWise
│
├── data
│   ├── raw
│   └── processed
│
├── notebooks
│   ├── 01_Data_Understanding.ipynb
│   └── 02_Preprocessing.ipynb
│
├── docs
├── src
└── README.md
```

---

# 📊 Data Understanding

League of Legends Kaggle 데이터셋의 구조를 분석하였다.

### 분석한 테이블

#### MatchTbl

경기 자체의 정보를 저장하는 테이블

* Match ID
* Patch
* Queue Type
* Game Duration

#### ChampionTbl

Champion ID와 Champion Name을 매핑하는 테이블

* ChampionId
* ChampionName

#### SummonerMatchTbl

한 플레이어가 한 경기에서 어떤 챔피언을 플레이했는지 저장하는 테이블

* MatchFk
* ChampionFk

#### MatchStatsTbl

플레이어의 경기 기록(스탯)을 저장하는 테이블

주요 컬럼

* Kills
* Deaths
* Assists
* TotalGold
* DmgDealt
* Lane
* Win
* EnemyChampionFk

#### TeamMatchTbl

양 팀의 챔피언 조합 및 경기 결과를 저장하는 테이블

향후 조합 분석 및 밴픽 추천에 활용할 예정이다.

---

# 🔄 데이터 전처리

### Champion 정보 병합

ChampionTbl과 SummonerMatchTbl을 병합하여 Champion ID를 Champion Name으로 변환하였다.

사용 기술

* pandas.merge()

---

### 경기 기록 병합

SummonerMatchTbl과 MatchStatsTbl을 병합하여 플레이어 정보와 경기 기록을 하나의 데이터셋으로 통합하였다.

병합 기준

* SummonerMatchId
* SummonerMatchFk

---

### Enemy Champion 변환

EnemyChampionFk를 ChampionTbl과 다시 병합하여 EnemyChampionName 컬럼을 생성하였다.

이를 통해

```
Ahri vs Zed
```

와 같이 사람이 읽을 수 있는 형태의 데이터를 구축하였다.

---

### Lane 데이터 확인

Lane 컬럼의 결측치를 분석하였다.

확인 결과

* 원본 데이터 자체에 약 177,000개의 결측치가 존재하였다.
* 이는 병합 과정의 문제가 아니라 데이터셋 특성임을 확인하였다.

또한

* SUPPORT → UTILITY 통일
* Lane 분석용 데이터셋(lane_df) 생성

을 수행하였다.

---

### 데이터 저장

전처리된 데이터를 CSV 형태로 저장하였다.

* final_dataset.csv
* lane_dataset.csv

---

# 💡 오늘 배운 내용

* pandas merge를 이용한 테이블 병합
* Primary Key와 Foreign Key의 관계 이해
* 데이터 전처리 과정의 중요성
* 결측치 발생 원인 분석
* 원본 데이터와 분석용 데이터 분리 관리 방법

---

# 🎯 다음 목표

* Exploratory Data Analysis(EDA) 수행
* 챔피언 픽률 분석
* 챔피언 승률 분석
* 라인별 메타 분석
* 챔피언 카운터 관계 분석
* 밴픽 추천 알고리즘 설계

---

## 📈 진행 현황

* [x] 프로젝트 환경 구축
* [x] 데이터 이해(Data Understanding)
* [x] 데이터 병합
* [x] 데이터 전처리
* [ ] 탐색적 데이터 분석(EDA)
* [ ] 추천 알고리즘 개발
* [ ] 머신러닝 모델 구축
* [ ] FastAPI 서버 개발
* [ ] 웹 서비스 구현


## 2026-07-01

### 오늘 한 일

- 챔피언 픽률 분석
- 승률 분석
- 카운터 분석

### 배운 점

- value_counts()를 이용하여 픽률을 계산하였다.
- groupby()를 이용하여 승률을 계산하였다.

### 다음 목표

- 추천 알고리즘 설계

# PickWise Development Log

---

## 2026-07-01

### 🎯 목표

- EDA 마무리
- 추천 시스템을 위한 Feature Engineering 진행

---

### ✅ EDA 완료

#### 데이터 탐색

- 데이터 구조 확인 (`head()`, `info()`, `describe()`)
- 결측치 확인
- 챔피언 픽률 분석
- 라인별 픽률 분석
- 챔피언 승률 분석

#### 데이터 검증

추천 시스템 개발 전 데이터의 신뢰성을 검증하였다.

`EnemyChampionName` 컬럼은 실제 라인 상대 챔피언이 아님을 확인하였다.

또한 라인별 승률 분석 과정에서 비정상적인 라인 조합이 존재하여 해당 데이터를 추천 알고리즘의 핵심 Feature로 사용하기 어렵다고 판단하였다.

이에 따라 추천 알고리즘은 `TeamMatchTbl` 기반으로 재설계하였다.

---

### ✅ Feature Engineering

#### TeamMatchTbl 활용

- Champion ID → Champion Name 변환
- Blue Team / Red Team 데이터 생성
- Team Dataset 생성

---

#### 추천 알고리즘 설계 변경

초기에는 동일한 **5인 팀 조합**을 분석하려 하였으나,

동일한 조합의 재등장 빈도가 매우 낮아 추천 데이터로 활용하기 어렵다는 점을 확인하였다.

이에 따라 추천 시스템의 방향을 **2인 챔피언 시너지 기반 추천**으로 변경하였다.

---

#### Champion Pair 생성

각 팀에서 가능한 모든 2인 챔피언 조합을 생성하였다.

생성된 Pair를 기반으로

- 경기 수(Games)
- 승률(WinRate)

을 계산하였다.

신뢰성을 위해 **100경기 이상 등장한 조합만 분석 대상으로 사용**하였다.

---

#### Main Lane 생성

`lane_dataset`을 이용하여 각 챔피언의 주 라인(Main Lane)을 계산하였다.

예시

- Ahri → MIDDLE
- Vi → JUNGLE
- Nautilus → UTILITY

---

#### Pair Feature 확장

Champion Pair 데이터에

- Lane1
- Lane2
- SameLane

Feature를 추가하였다.

같은 라인 조합(Lucian-Senna, Ashe-Senna 등)도 실제 메타에서 활용되는 사례가 존재하므로 데이터를 제거하지 않고 유지하였다.

추천 알고리즘 단계에서 활용 여부를 판단하도록 설계하였다.

---

### 📂 생성 데이터

```
data/interim/

main_lane.csv
pair_stats.csv
```

---

### 💡 설계 변경

기존

```
5인 조합 기반 추천
```

↓

변경

```
2인 챔피언 시너지 추천
```

변경 이유

- 동일한 5인 조합 데이터가 매우 적음
- 실제 밴픽에서는 2인 시너지 활용도가 높음
- 추천 품질 향상을 위해 설계 변경

---

### 🚀 다음 목표

- Recommendation 모듈 개발
- 챔피언 선택 시 시너지 추천 기능 구현
- 추천 점수 계산 로직 설계
- PickWise 추천 알고리즘 1차 구현