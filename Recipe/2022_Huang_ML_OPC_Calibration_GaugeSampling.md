# Effective OPC Model Calibration Using Machine Learning

## 메타데이터
- **저자**: Yi-Hao Huang, Shin-Shing Yeh, Yung-Ching Mai, Chia-Chi Lin, Jun-Cheng Lai
- **연도**: 2022
- **게재지**: Proc. SPIE 12052, DTCO and Computational Patterning, 120521C
- **DOI/URL**: https://doi.org/10.1117/12.2611337

## 핵심 요약
OPC 모델 정확도 향상은 더 많은 SEM 계측 데이터를 필요로 하지만, 데이터 수집 시간이 증가하는 트레이드오프가 있다. 본 논문은 머신러닝을 활용한 효율적인 OPC 모델 gauge 샘플링 플로우를 제안하여, 데이터 수집 시간을 줄이면서도 모델 정확도를 향상시키는 방법을 제시한다. 데이터 전처리, 특징 변환, 클러스터링을 통해 대표 샘플 데이터를 선별한다.

## 주요 기여
1. **ML 기반 Gauge 샘플링**: 머신러닝으로 OPC 모델 캘리브레이션에 필요한 최적 측정 위치 선별
2. **데이터 전처리 및 특징 변환**: 레이아웃 특징을 ML 입력에 적합한 형태로 변환
3. **클러스터링 기반 대표 선별**: 전체 gauge 공간을 클러스터로 분할 → 각 클러스터에서 대표 포인트 선택
4. **SEM 데이터 수집 시간 감소**: 동일 정확도를 더 적은 측정으로 달성
5. **OPC 모델 정확도 향상**: 대표성 있는 gauge 선택으로 모델 일반화 성능 개선

## Recipe/Flow 상세
- **ML 기반 OPC 모델 Gauge 샘플링 플로우**:
  1. **후보 Gauge 생성**:
     - OPC 레이아웃에서 측정 가능한 CD 위치 전수 추출
     - 각 gauge의 국소 패턴 특징 계산 (CD, 피치, 밀도, 방향 등)
  2. **데이터 전처리**:
     - 특징 정규화 및 이상치 제거
     - 다차원 특징 공간 구성
  3. **특징 변환**:
     - PCA(주성분 분석) 또는 t-SNE로 차원 축소
     - OPC 모델 민감도가 높은 특징에 가중치 부여
  4. **클러스터링**:
     - K-means 또는 계층적 클러스터링으로 gauge 공간 분할
     - 각 클러스터: 유사한 패턴 환경의 gauge 그룹
  5. **대표 Gauge 선별**:
     - 각 클러스터에서 가장 대표적인 포인트 선택
     - 전체 특징 공간을 균등하게 커버하는 최소 gauge 세트 구성
  6. **OPC 모델 캘리브레이션**: 선별된 gauge로 SEM 측정 → 모델 피팅
- **장점**: 동일 SEM 측정 횟수로 더 높은 모델 정확도, 또는 더 적은 측정으로 동일 정확도
- **적용**: 첨단 노드 OPC 모델 캘리브레이션 효율화

## OPC 툴 구현 관련성
- SKOPC OPC 모델 캘리브레이션 모듈의 gauge 샘플링 전략 개선
- `gauge_sampling.py`: 특징 추출 → PCA/클러스터링 → 대표 gauge 선별
- SEM 계측 비용 최적화를 위한 smart sampling 구현
- OPC 모델 재캘리브레이션 시 최소 데이터로 최대 효율 달성

## 태그
`OPC`, `ModelCalibration`, `MachineLearning`, `GaugeSampling`, `Clustering`, `SEM`, `Efficiency`, `SPIE`, `2022`
