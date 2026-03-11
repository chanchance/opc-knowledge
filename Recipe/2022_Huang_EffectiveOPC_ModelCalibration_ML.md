# Effective OPC Model Calibration Using Machine Learning

## 메타데이터
- **저자**: Yi-Hao Huang, Shin-Shing Yeh, Yung-Ching Mai, Chia-Chi Lin, Jun-Cheng Lai
- **연도**: 2022
- **게재지**: Proc. SPIE 12052, DTCO and Computational Patterning I
- **DOI/URL**: https://doi.org/10.1117/12.2611337
- **인용수**: ~15

## 핵심 요약
OPC 모델 캘리브레이션을 위한 게이지(gauge) 샘플 선택을 ML로 최적화하는 효율적 캘리브레이션 흐름을 제안한다. 데이터 전처리, 피처 변환, 클러스터링을 통해 캘리브레이션 데이터를 클러스터로 분류하고 소수의 대표 샘플을 선택함으로써, 동등한 모델 품질을 더 적은 계측 데이터로 달성한다. 기존 POR(Plan of Record) 대비 계측 부담을 줄이면서 OPC 모델 캘리브레이션 효율성을 향상시킨다.

## 주요 기여
1. ML 기반 OPC 모델 게이지 샘플 선택 최적화
2. 클러스터링으로 대표 샘플 선택 → 계측 데이터 감소
3. 동등 모델 품질 유지하며 캘리브레이션 TAT 단축
4. 공정 노드 전환 시 신속한 모델 구축 지원

## Recipe/Process Flow 상세

### OPC 모델 캘리브레이션 게이지 선택 문제
```
캘리브레이션 과정:
  1. 테스트 패턴 선택 (게이지)
  2. 테스트 패턴 리소그래피 → SEM 측정
  3. 측정 데이터로 OPC 모델 파라미터 최적화

게이지 선택의 중요성:
  너무 많은 게이지:
    - 계측 시간 증가 (수일~수주)
    - 중복 정보로 모델 개선 효과 제한
  너무 적은 게이지:
    - 특정 패턴 타입 정보 부족
    - 모델 외삽 오차 증가

목표: 최소 게이지로 최고 모델 품질
```

### ML 기반 게이지 선택 알고리즘
```
1단계: 후보 게이지 풀 정의
  전체 테스트 패턴 라이브러리에서 후보 선택
  다양한 패턴 유형: 1D, 2D, 다양한 CD/pitch

2단계: 피처 추출 및 변환
  각 패턴에서 피처 추출:
    - CD, pitch, 공간(space) 폭
    - 패턴 밀도
    - 2D 기하 특성 (코너, 끝단)
  피처 변환:
    - 정규화(normalization)
    - PCA로 차원 축소 (상관 제거)

3단계: 클러스터링
  k-means 또는 계층적 클러스터링
  클러스터 수(k): 목표 게이지 수에 따라 설정
  각 클러스터: 유사한 OPC 거동을 가진 패턴 그룹

4단계: 대표 샘플 선택
  각 클러스터에서 중심에 가장 가까운 패턴 선택
  또는 클러스터 내 다양성 고려한 샘플 선택
  최종: k개 대표 게이지 (전체 후보의 수십 분의 1)

5단계: 모델 캘리브레이션 및 검증
  선택된 k개 게이지로 모델 캘리브레이션
  검증 세트(미선택 패턴)에서 모델 정확도 평가
```

### 기존 LLE 방법과 비교
```
LLE 기반 (Casati, 2014, IBM+ETH):
  비선형 차원 축소 + 다목적 최적화
  장점: 비선형 데이터 구조 보존
  단점: 구현 복잡도 높음

ML 클러스터링 기반 (본 논문):
  PCA + k-means (선형 방법)
  장점: 구현 단순, 해석 가능
  단점: 비선형 구조 완전 포착 어려울 수 있음

두 방법 공통 목표:
  → 최소 게이지로 최대 모델 품질
  → 계측 비용 절감
```

### 성능 결과
```
모델 정확도 (캘리브레이션 RMS EPE):
  POR 전체 게이지 사용: 기준
  ML 선택 게이지 (k << 전체): 동등하거나 근접

게이지 감소율:
  ML 선택: 전체 POR 대비 수십 % 감소
  모델 품질: 동등 유지

TAT 단축:
  계측 시간: 게이지 수 감소 비례 단축
  모델 구축 사이클: 단축
```

## OPC 툴 구현 관련성
- **SKOPC 캘리브레이션 게이지 선택**: `skopc/modeling/` 캘리브레이션 전 ML 게이지 선택 전처리
- **PCA + k-means**: scikit-learn으로 즉시 구현 가능 (PCA + KMeans 파이프라인)
- **게이지 풀 관리**: 패턴 라이브러리에서 후보 게이지 자동 추출 및 관리
- **LLE 대안**: Casati(2014) LLE 방법의 경량 대안으로 빠른 구현 및 적용

## 참고문헌
- Proc. SPIE 12052, DTCO and Computational Patterning I (2022)
- 관련: Automated sample plan selection for OPC modeling (SPIE 9052, 2014 - Casati, IBM+ETH)
- 관련: Roadmap to sub-nanometer OPC model accuracy (SPIE 8441, 2012)
- 관련: OPC model calibration using deep reinforcement learning (SPIE 13425, 2025)

## 태그
`Recipe`, `SPIE`, `OPC-ModelCalibration`, `MachineLearning`, `GaugeSampling`, `Clustering`, `PCA`, `KMeans`, `CalibrationEfficiency`, `TAT`, `2022`
