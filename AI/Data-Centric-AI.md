# Model-Centric AI, Data-Centric AI

## Model-Centric AI와 Data-Centric AI의 차이점

![Image](https://github.com/user-attachments/assets/3d394f15-1c3a-4b66-8a23-b3fac06769f5)

## Model-Centric AI

- 정의 : AI 시스템 개발에서 **모델을 중심으로 접근**하는 방법론
- 데이터를 일정 수준 고정 혹은 제한하고 **모델 자체의 설계와 최적화**에 집중
- 과거부터 지금까지 주로 사용되는 AI 시스템 개발의 주 접근 방식
- BERT, GPT, ResNet 등이 Model-Centric AI의 산물이라 볼 수 있음.

### 주요 목적

- 모델 설계
    - 다양한 딥러닝 모델 (CNN, RNN, Transformer 등)의 구조를 연구하고 새로운 아키텍처 개발
    - 모델이 주어진 문제를 해결할 수 있도록 설계
- Hyperparameter 최적화
    - 학습 속도, Batch Size, Dropout 비율 등을 조절하여 성능 향상을 이끌어냄
- 모델 훈련 알고리즘 개선
    - SGD, Adam 등의 최적화 알고리즘 개선 및 새로운 방법론 적용
- 성능 평가 및 튜닝
    - 모델 성능 테스트 후 과적합 및 과소적합 방지를 위한 모델 수정

### 한계 및 사례

- 한계
    - 정교한 모델이라 하더라도 데이터의 품질이 떨어지면 결국 좋은 성능이 나오기는 어려움
    - 투입한 시간과 노력에 비해 모델의 성능이 극적으로 향상되는 경우는 드물다.
- 사례 - Steel 제조업에서 개발한 불량품 탐지 AI 시스템
    - 초기 탐지 정확도는 76.2%
    - Model-Centric AI 접근법으로는 목표 정확도인 90%에 도달할 수 없었음

### 다른 방법론의 필요성

- 과거 연구의 트랜드 : Task에 맞는 데이터를 대량으로 집어 넣고 **노이즈를 잘 걸러내는 모델**을 만드는 것 (BERT 등)
- **최근 연구**의 트렌드 : 사전 학습 모델에 **소량의 고품질 데이터**를 확보하여 Fine-Tuning하는 것
- AI 시스템에서 데이터가 차지하는 비율이 80%
    
    ![Image](https://github.com/user-attachments/assets/238d5f2c-dd6c-4292-b7a8-8f9ecf5b33a1)
    

## Data-Centric AI

- AI 시스템 개발에서 **데이터를 중심으로 접근**하는 방법론
- 데이터가 AI 성능의 핵심이라는 인식에서 출발
- 모델의 구조를 고정 혹은 최소한의 조정 후 데이터 품질에 노력을 기울임
- 2020년대에 들어 주목받기 시작한 접근 방식
    
    ### ※ 필요성
    
    - 모델 성능을 종합적으로 평가할 수 있는 데이터셋이 필요
    - 실전에서는 소량의 데이터가 반복적으로 생성되므로 좋은 데이터셋을 생성하는 알고리즘 필요

## Data-Centric AI의 3가지 주요 목표

![Image](https://github.com/user-attachments/assets/2e103e7a-ac26-4998-81c5-54aeb1895dee)

### 1. Training Data Development

- 훈련 데이터는 모델 학습의 기초로, 고품질의 데이터를 구성하는 것이 중요
    
    ### ※ 종류
    
    - Data Collection : 새로운 데이터 구축 또는 기존 데이터셋 통합
    - Data Labeling : 수집한 데이터들에 라벨을 부여하여 학습 가능한 형태로 만든다.
    - Data Preparation : 데이터 정제, 특징 추출, 표준화 및 정규화를 통해 학습 준비
    - Data Reduction : 특징 선택, 차원 축소 등을 통해 데이터의 크기와 복잡성 감소
    - Data Augmentation : 데이터를 더 수집하지 않고 다양성을 높임

### 2. Inference Data Development

- 추론 데이터는 모델의 성능 평가를 위한 테스트와 검증 데이터로 사용됨
    
    ### ※ 종류
    
    - In Distribution Evaluation : training 데이터와 **같은 분포를 가진 데이터셋**으로 모델 성능 평가
    - Out of Distribution Evaluation : **다른 분포를 가진 데이터셋**으로 성능 평가

### 3. Data Maintenance

- AI 시스템 운영 환경에서는 데이터가 지속적으로 변화하며, 데이터 유지 관리가 필수
    
    ### ※ 종류
    
    - Data Understanding : 데이터의 특성을 전반적으로 이해할 수 있는 알고리즘
    - Data Quality Assurance : 데이터의 퀄리티를 평가할 수 있는 Metric을 개발
    - Data Storage & Retrieval : 데이터를 효율적으로 저장하고 빠르게 검색할 수 있도록 관리

## Model-Centric AI와 Data-Centric AI의 비교

![Image](https://github.com/user-attachments/assets/8341abfd-1497-425b-b9cb-6fd239902938)

- AI 시스템 개발에서 데이터와 모델 모두 최적화하는 것이 보완적
- 적은 양의 데이터를 활용할 수 있는 Model-Centric AI도 중요함
- Data-Centric AI의 중요도에 비해 연구가 부족한 상황
