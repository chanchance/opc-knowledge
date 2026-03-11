# Accurate Etch Modeling with Massive Metrology and Deep-Learning Technology

## 메타데이터
- **저자**: (SPIE 11327 - 2020 SPIE Advanced Lithography)
- **연도**: 2020
- **게재지**: Proc. SPIE 11327, Optical Microlithography XXXIII
- **DOI/URL**: https://doi.org/10.1117/12.2551747
- **인용수**: ~25

## 핵심 요약
대규모 계측 데이터(massive metrology)와 딥러닝을 결합하여 OPC 흐름에서 식각 모델의 정확도를 획기적으로 개선하는 방법론을 제안한다. 기존 해석적 식각 모델의 한계를 딥러닝 기반 데이터 구동 모델로 극복하며, 수만 개의 측정 포인트로 훈련된 모델이 다양한 패턴 유형에서 우수한 식각 바이어스 예측 정확도를 달성한다.

## 주요 기여
1. 대규모 계측 데이터 기반 딥러닝 식각 모델 구축
2. 기존 해석적 식각 모델 대비 예측 정확도 향상
3. 다양한 패턴 유형(1D/2D, 다양한 피치/CD)에 대한 범용 모델
4. OPC 흐름 통합을 위한 실용적 식각 모델 캘리브레이션 워크플로우

## Recipe/Process Flow 상세

### 대규모 계측 데이터 수집
```
계측 전략:
  - 다양한 테스트 패턴 설계:
      1D 라인/스페이스: 다양한 CD, pitch, duty cycle
      2D 패턴: 끝단(line-end), 코너, T-junction
      밀도 변화: sparse → dense 그래디언트

  - 측정 포인트: 수만 개 (massive metrology)
  - 측정 방법:
      리소그래피 후: 인라인 SEM 또는 OCD
      식각 후: 인라인 SEM 또는 TEM 단면

  - 데이터 쌍: (리소그래피 CD, 식각 CD) × 패턴 피처
```

### 딥러닝 식각 바이어스 모델
```
모델 구조:
  입력: 패턴 피처 벡터
    - 로컬 CD (선폭, 공간 폭)
    - 주변 패턴 밀도 (여러 반경: 0.5μm, 1μm, 2μm, 5μm)
    - 피치, 주기성
    - 2D 기하 피처 (코너 각도, 끝단 거리 등)

  딥러닝 아키텍처:
    - 완전연결 신경망 (Fully Connected Network)
    - 또는 컨볼루션 기반 (패턴 이미지 입력)
    - 은닉층: 다층 구조, ReLU 활성함수
    - 출력: 식각 바이어스 (ΔCD_etch)

  훈련:
    - 손실함수: MSE(측정 식각 바이어스, 예측 식각 바이어스)
    - 최적화: Adam 또는 SGD
    - 정규화: Dropout, L2 regularization
    - 검증: k-fold cross-validation

대규모 데이터의 이점:
  - 희귀 패턴 유형의 식각 거동도 학습 가능
  - 해석적 모델이 놓치는 고차(high-order) 상호작용 포착
  - 노드 간 전이학습(transfer learning) 가능
```

### OPC 통합 식각 모델 캘리브레이션
```
캘리브레이션 워크플로우:
  1. 계측 데이터 수집 (리소그래피 후 + 식각 후)
  2. 딥러닝 모델 훈련
  3. 검증 세트에서 정확도 평가
  4. OPC 타겟 보정에 모델 통합:
       Silicon target → etch model → adjusted litho target → OPC

전체 OPC 흐름:
  설계 → [EPC 타겟 조정] → OPC → 리소그래피 시뮬 → [식각 시뮬] → 최종 검증

정확도 지표:
  식각 바이어스 예측 RMS 오차: 서브 nm 수준 목표
  패턴 유형별 성능: 1D 및 2D 패턴 모두
```

### 성능 결과
```
딥러닝 모델 vs 기존 해석적 모델:
  식각 바이어스 예측 정확도: 딥러닝 모델 우세
  특히 2D 복잡 패턴에서 차이 두드러짐
  대규모 데이터 활용으로 일반화 성능 향상

OPC 최종 CD 정확도:
  EPC 통합 시 최종 CD 오차 감소
  공정 윈도우 확보에 기여
```

## OPC 툴 구현 관련성
- **SKOPC 식각 모델**: `skopc/modeling/` 식각 바이어스 예측기를 딥러닝 모델로 구현, OPC 타겟 보정 전처리 추가
- **대규모 계측 통합**: 외부 SEM/OCD 측정 데이터를 읽어 모델 훈련하는 캘리브레이션 모듈
- **TorchResist 연동**: 기존 리소그래피 시뮬 후단에 식각 시뮬 레이어 추가 가능
- **전이학습**: 유사 공정 노드의 식각 모델을 신규 노드 초기화에 활용

## 참고문헌
- Proc. SPIE 11327, Optical Microlithography XXXIII (2020)
- 관련: Etch proximity correction through ML-driven etch bias model (SPIE 9782, 2016)
- 관련: Using machine learning etch models in OPC and ILT correction (SPIE 11614, 2021)
- 관련: OPC accuracy improvement through deep-learning based etch model (SPIE 12056, 2022)

## 태그
`Recipe`, `SPIE`, `EtchModel`, `DeepLearning`, `MassiveMetrology`, `EtchBias`, `EPC`, `OPC-Integration`, `DataDriven`, `2020`
