# Subresolution Assist Feature Generation With Supervised Data Learning

## 메타데이터
- **저자**: X. Xu et al.
- **연도**: 2018
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems, Vol. 37, No. 6, pp. 1225–1236
- **DOI/URL**: https://ieeexplore.ieee.org/document/8023813/
- **인용수**: ~100

## 핵심 요약
기계학습 기반 SRAF 생성의 선구적 연구. 상용 Calibre 툴 대비 10배 속도 향상과 동등한 EPE/PV 밴드 성능을 달성하는 최초의 ML 기반 SRAF 생성 프레임워크를 제안한다. 강건한 피처 추출, 피처 압축, SRAF 분류 및 예측 모델 훈련, 최종 SRAF 생성으로 구성된 4단계 파이프라인을 제시한다.

## 주요 기여
1. 최초의 ML 기반 SRAF 생성 프레임워크
2. 강건한 피처 추출 방법론 (레이아웃 기하학 정보 인코딩)
3. 피처 압축(compaction) 기법으로 고차원 입력 처리
4. Calibre 대비 10X 속도 향상, 동등한 EPE/PV 밴드 성능

## Recipe/Process Flow 상세

### ML 기반 SRAF 생성 파이프라인
```
1. 피처 추출 (Feature Extraction)
   - 레이아웃의 각 후보 SRAF 위치에 대해 피처 계산
   - 기하학적 피처: 주변 패턴 CD, 간격, 밀도
   - 광학적 피처: 이미지 강도, NILS(Normalized Image Log Slope)
   - 컨텍스트 피처: 이웃 패턴 정보
   - 강건성: 노이즈, 회전, 반사에 불변하는 피처 설계

2. 피처 압축 (Feature Compaction)
   - PCA(Principal Component Analysis) 또는 오토인코더
   - 고차원 피처 → 저차원 대표 피처 변환
   - 불필요한 피처 제거로 과적합 방지

3. 모델 훈련 (Model Training)
   - SRAF 분류 모델: 후보 위치에 SRAF 삽입 여부 결정
   - SRAF 크기 예측 모델: SRAF 폭, 길이 회귀
   - 훈련 데이터: Calibre 기반 model-based SRAF 결과
   - SVM, Random Forest, 또는 신경망 사용

4. SRAF 생성 (SRAF Generation)
   - 전체 칩 레이아웃에 학습된 모델 적용
   - 분류 결과로 SRAF 위치 결정
   - 크기 예측으로 SRAF 형상 결정
   - DRC 후처리로 규칙 위반 제거
```

### 성능 비교 (Calibre 대비)
```
속도:     10X 향상 (병렬화 및 ML 추론 속도)
EPE:      동등 (< ±3nm RMS)
PV Band:  동등 (공정 윈도우 면적 유사)
SRAF 품질: 비교 가능한 NILS 및 DOF
```

### 훈련 데이터 구성
- Calibre model-based SRAF 결과를 Ground Truth로 사용
- 다양한 피치, CD, 밀도 조합 포함
- 1D 라인-스페이스 및 2D contact/via 패턴 포함
- 훈련/테스트 분리로 일반화 성능 검증

## OPC 툴 구현 관련성
- **SKOPC ML 모듈**: 레이아웃 피처 기반 SRAF 예측기 구현의 직접적 참조
- **피처 추출**: NILS, 이미지 강도, 기하학적 지표는 `skopc/core/litho_engine.py`에서 계산 가능
- **속도**: 전체 칩 SRAF 생성의 병목을 ML 추론으로 대체
- **GAN-SRAF의 전신**: 이 논문 → GAN-SRAF(2020) → CTM-SRAF(2023)의 발전 계보

## 참고문헌
- IEEE TCAD Vol. 37, No. 6, June 2018
- 관련: GAN-SRAF: Subresolution Assist Feature Generation Using GANs (IEEE TCAD, 2020)
- 관련: CTM-SRAF (IEEE TCAD, 2023)
- 관련: SRAF Insertion via Supervised Dictionary Learning (IEEE, 2019)

## 태그
`Recipe`, `IEEE`, `TCAD`, `SRAF`, `MachineLearning`, `SupervisedLearning`, `FeatureExtraction`, `Calibre`, `SpeedUp`, `PVBand`
