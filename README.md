# 🎮 PickWise

> **League of Legends Draft Pick Recommendation System using Match Data & Machine Learning**

## 📌 Project Overview

PickWise는 **리그 오브 레전드(League of Legends) 밴픽 과정에서 최적의 챔피언을 추천하는 데이터 기반 밴픽 추천 시스템**입니다.

많은 플레이어들이 상대 조합을 보고 적절한 챔피언을 선택하거나 밴하는 데 어려움을 겪습니다. 특히 일반 유저들은 프로 경기처럼 조합이나 카운터 관계를 빠르게 판단하기 어렵습니다.

실제로 롤을 오랜시간 플레이 해왔지만 친구들과 5인 랭크 게임이나 내전을 진행하면서 친구들은 즉시 "이 챔피언을 밴하자", "이 챔피언을 픽하자"라고 판단하지만, 나는 이러한 밴픽에 대한 의사결정을 즉각적으 내리기 어렵다는 문제를 직접 경험하였습니다.

PickWise는 실제 매치 데이터를 분석하여

* 상대 챔피언 카운터 추천
* 아군 조합 시너지 추천
* 승률 기반 추천
* 밴 추천
* 상대 다음 픽 예측

등의 기능을 제공하는 것을 목표로 합니다.

---

# 🎯 Project Goal

* 데이터 기반 챔피언 추천 시스템 구축
* 실시간 Draft Pick 의사결정 지원
* 머신러닝을 활용한 상대 픽 예측
* 누구나 사용할 수 있는 밴픽 추천 웹 서비스 개발

---

# ✨ Main Features

### ✅ Champion Counter Recommendation

상대 챔피언이 선택되면 승률이 높은 카운터 챔피언 추천

---

### ✅ Ban Recommendation

상대 조합을 고려하여 가장 위험한 챔피언 추천

---

### ✅ Team Synergy Recommendation

현재 아군 조합과 시너지가 높은 챔피언 추천

---

### ✅ Pick Win Rate Analysis

라인별 승률 및 픽률을 분석하여 추천

---

### ✅ Opponent Pick Prediction (Planned)

현재까지 공개된 밴픽을 기반으로 상대의 다음 픽을 예측하는 머신러닝 모델 개발

---

# 📂 Project Structure

```
PickWise
│
├── app                 # Web Application
├── backend             # Backend
├── frontend            # Frontend
├── data
│   ├── raw             # Original Dataset (Git Ignore)
│   └── processed       # Preprocessed Dataset (Git Ignore)
│
├── docs
│   └── Development_log.md
│
├── notebooks
│   ├── 01_Data_Understanding.ipynb
│   ├── 02_Preprocessing.ipynb
│   └── 03_EDA.ipynb
│
├── src                 # Python Source Code
├── README.md
├── requirements.txt
└── .gitignore
```

---

# 🛠 Tech Stack

* Python
* Pandas
* NumPy
* Scikit-learn
* Jupyter Notebook
* Matplotlib
* VS Code
* Git / GitHub

---

# 📊 Dataset

* Riot Match Dataset
* Kaggle Match Dataset

> Due to GitHub file size limitations, raw datasets are not included in this repository.

---

# 🚀 Development Roadmap

* [x] Project Setup
* [x] Dataset Understanding
* [x] Data Preprocessing
* [ ] Exploratory Data Analysis (EDA)
* [ ] Champion Counter Analysis
* [ ] Champion Synergy Analysis
* [ ] Pick Win Rate Model
* [ ] Opponent Pick Prediction
* [ ] Recommendation Algorithm
* [ ] Backend API
* [ ] Frontend Development
* [ ] Web Deployment

---

# 📌 Future Work

* 머신러닝 기반 픽 예측 모델 고도화
* 실시간 Draft Pick 추천
* 최신 패치 자동 반영
* 사용자 맞춤 추천 시스템
* Riot API 실시간 연동
