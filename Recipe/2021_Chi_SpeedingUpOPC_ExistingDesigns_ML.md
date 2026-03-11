# Speeding Up OPC by Leveraging Existing Designs with Machine Learning

## 메타데이터
- **저자**: Cheng Chi, Julian Dolby, Jeffery C. Shearer, Derren Dunn, Sean Burns
- **연도**: 2021
- **게재지**: Proc. SPIE 11614, Design-Process-Technology Co-optimization for Manufacturability XV
- **DOI/URL**: https://doi.org/10.1117/12.2584621
- **인용수**: ~20

## 핵심 요약
기존 OPC 완료 설계 데이터를 ML로 활용하여 새로운 레이아웃의 OPC를 빠르게 수행하는 방법론을 제시한다. 비슷한 패턴 구조를 가진 기존 설계의 OPC 결과를 학습하여, 신규 레이아웃의 OPC 계산 자원을 절감한다. IBM Research 제안으로, 전이학습(transfer learning) 개념을 OPC 가속에 적용한다.

## 주요 기여
1. 기존 설계의 OPC 결과를 ML 훈련 데이터로 재활용하는 전략
2. 설계 간 패턴 유사성을 활용한 OPC 계산 자원 절감
3. 전이학습 기반의 신규 레이아웃 OPC 초기화
4. 실용적 ML-OPC 파이프라인의 데이터 효율성 향상

## Recipe/Process Flow 상세

### 기존 설계 활용의 동기
```
OPC 반복 실행의 비효율:
  동일 공정 노드의 연속 테이프아웃:
    - 레이아웃 A: OPC 완료 (대용량 데이터)
    - 레이아웃 B: OPC 실행 예정
    - 레이아웃 A와 B는 많은 공통 패턴 포함

  기존 방법: 레이아웃 B에서 완전히 새로 OPC 계산
  낭비: 레이아웃 A의 OPC 지식 미활용

ML 활용 아이디어:
  레이아웃 A의 (패턴 피처, 최적 마스크 바이어스) 쌍 → ML 훈련
  레이아웃 B의 유사 패턴 → ML 예측 → OPC 초기화
  → B의 OPC 이터레이션 수 감소
```

### 패턴 유사성 기반 전이학습
```
패턴 유사성 측정:
  두 레이아웃의 패턴 피처 분포 비교:
    - 피처 공간에서 거리(KL divergence, histogram 비교)
    - 유사도 높을수록 → 전이학습 효과 크림

전이학습 전략:
  1. 소스 설계(A)에서 ML 모델 훈련
     훈련 데이터: (패턴 피처, 최적 마스크 바이어스)
     모델: Gradient Boosting, Neural Network 등

  2. 타겟 설계(B)에 모델 적용
     a) 직접 전이 (Zero-shot): A 모델을 B에 그대로 사용
        → B와 A가 매우 유사한 경우 효과적
     b) 미세 조정 (Fine-tuning): B의 일부 데이터로 재훈련
        → 더 나은 정확도, 추가 데이터 필요
     c) 도메인 적응: A 모델을 B 분포에 맞게 조정

  3. ML 예측으로 B의 OPC 초기화
     → B의 OPC 이터레이션 수 감소
```

### ML-OPC 파이프라인
```
전체 파이프라인:

오프라인 단계 (설계 A에서):
  1. OPC 실행 (표준 MB-OPC)
  2. 수렴된 마스크 바이어스 추출
  3. 패턴 피처 추출
  4. ML 모델 훈련 및 저장

온라인 단계 (설계 B 처리 시):
  1. 패턴 피처 추출
  2. 저장된 ML 모델로 초기 마스크 바이어스 예측
  3. ML 예측을 초기값으로 OPC 실행 (이터레이션 수 감소)
  4. 수렴된 바이어스로 B의 ML 모델 업데이트 (점진적 학습)

계산 절감:
  ML 추론: 수 분 (전체 칩)
  OPC 이터레이션 수: 10-15 → 3-5
  전체 TAT: 유의미한 단축
```

### 데이터 효율성 및 샘플링
```
훈련 데이터 최소화:
  전체 설계 A의 모든 세그먼트 사용 vs. 선택적 샘플링

  효율적 샘플링 전략:
    - 커버리지 기반: 피처 공간 전체 커버
    - 어려운 패턴 우선: 핫스팟 주변 세그먼트 강화
    - 중복 제거: 유사 패턴 중 대표 샘플만 선택

  결과: 전체 데이터의 10-20%로 동등한 모델 성능

점진적 학습 (Continual Learning):
  새로운 설계 OPC 완료 시 모델 업데이트
  → 데이터 축적으로 시간이 지날수록 모델 개선
  → 노드 성숙기에 최고 성능 달성
```

### 성능 결과 (IBM Research 검증)
```
테스트 설계: 유사한 두 레이아웃 (동일 공정 노드)

ML-OPC 적용 결과:
  OPC 이터레이션 감소: 유의미한 감소
  최종 EPE: 표준 OPC 동등
  런타임: 절감 (ML 추론 + 감소된 이터레이션)

전이 효율:
  패턴 유사도 높은 설계 쌍: 더 큰 이터레이션 감소
  패턴 유사도 낮은 쌍: 직접 전이 효과 제한 → 미세조정 필요
```

## OPC 툴 구현 관련성
- **SKOPC 설계 간 ML 재활용**: `skopc/modeling/` 설계 A의 OPC 결과로 훈련된 모델을 설계 B 초기화에 활용
- **모델 저장소**: 공정 노드별 ML-OPC 모델 저장 디렉토리 (`skopc/models/`)
- **점진적 학습**: OPC 완료 후 자동으로 모델 업데이트하는 온라인 학습 루프
- **유사도 측정**: 설계 피처 분포 비교 후 전이학습 효과 예측 도구

## 참고문헌
- Proc. SPIE 11614, Design-Process-Technology Co-optimization XV (2021)
- 저자 소속: IBM Research
- 관련: Implementing ML OPC on product layouts (SPIE 11328, 2020)
- 관련: Effective data sampling techniques for ML-OPC (SPIE 11613, 2021)
- 관련: Optimization of ML-guided OPC: PFT+RFR (IEEE 8623985, 2019)

## 태그
`Recipe`, `SPIE`, `ML-OPC`, `TransferLearning`, `ExistingDesigns`, `OPC-Acceleration`, `TAT`, `IBM`, `DataEfficiency`, `ContinualLearning`, `2021`
