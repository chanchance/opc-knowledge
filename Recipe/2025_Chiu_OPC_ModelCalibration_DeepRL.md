# OPC Model Calibration Using Deep Reinforcement Learning

## 메타데이터
- **저자**: Weilun Chiu, Tony Hu, Terry Hsuan, Elvis Yang, T.H. Yang, K.C. Chen
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV
- **DOI/URL**: https://doi.org/10.1117/12.3049598
- **인용수**: 신규 (2025)

## 핵심 요약
OPC 모델 캘리브레이션 파라미터 탐색 문제를 심층 강화학습(DRL) 프레임워크로 접근하는 방법론을 제시한다. DRL 에이전트가 OPC 파라미터 공간을 탐색하여 캘리브레이션 RMS 오차를 최소화하는 파라미터를 예측한다. VAE, PCA, 커널 PCA로 파라미터 차원을 축소한 후 DRL을 적용하여 수렴 안정성을 높이며, VIA 레이어 실증에서 기존 순차적 캘리브레이션과 동등한 정확도를 달성한다.

## 주요 기여
1. OPC 모델 캘리브레이션에 최초의 심층 강화학습 적용
2. VAE/PCA/커널 PCA 기반 파라미터 차원 축소로 DRL 수렴 안정화
3. 기존 순차적 캘리브레이션 대비 동등 정확도 달성
4. TSMC 양산 공정에서 VIA 레이어 실증

## Recipe/Process Flow 상세

### OPC 모델 캘리브레이션의 파라미터 탐색 문제
```
기존 OPC 캘리브레이션:
  파라미터 수: 수십 ~ 수백 개 (광학 + 레지스트)
  방법: 순차적 최적화
    1. 광학 파라미터 먼저 최적화 (σ, aberration)
    2. 레지스트 파라미터 후 최적화 (diffusion, bias)
  문제:
    - 파라미터 간 의존성으로 로컬 미니마 가능
    - 수동 초기값 설정 필요
    - 전문가 경험 의존

DRL 접근:
  상태(State): 현재 캘리브레이션 오차 메트릭
  행동(Action): OPC 파라미터 조정 방향/크기
  보상(Reward): -RMSE(OPC 모델 캘리브레이션 오차)
  목표: 보상 최대화 = RMSE 최소화
```

### DRL 기반 캘리브레이션 알고리즘
```
방법 1: 직접 파라미터 예측
  DRL 에이전트 입력: 현재 측정 데이터 피처
  DRL 에이전트 출력: 모든 OPC 파라미터 값 직접 예측
  보상: -RMS_EPE(예측 파라미터로 시뮬레이션된 CD 오차)
  알고리즘: PPO(Proximal Policy Optimization) 또는 SAC

방법 2: 차원 축소 후 DRL
  a) 파라미터 임베딩:
     - VAE: OPC 파라미터 → 잠재 벡터 z (4차원)
     - PCA: 주성분 4개로 차원 축소
     - 커널 PCA: 비선형 차원 축소
  b) DRL이 저차원 잠재 공간에서 탐색
     행동: 잠재 벡터 z 조정
     디코딩: z → 실제 OPC 파라미터
  c) 장점: 파라미터 공간 다양체 구조 활용, 수렴 안정

DRL 훈련:
  시뮬레이션 환경: OPC 모델 시뮬레이터
  에피소드: 무작위 초기 파라미터 → 수렴까지
  탐색/활용 균형: ε-greedy 또는 엔트로피 정규화
```

### 보상 함수 설계
```
보상 함수:
  r(t) = -RMSE_t + γ × (RMSE_{t-1} - RMSE_t)

  -RMSE_t: 현재 캘리브레이션 오차 페널티
  γ × 개선량: 오차 감소에 대한 추가 보상
  → 빠른 수렴 유도

조기 종료 조건:
  RMSE < 임계값 → 에피소드 종료 + 추가 보상
```

### VIA 레이어 적용 결과
```
실험 설정:
  - 공정: TSMC 선진 노드
  - 레이어: VIA (비아 홀)
  - 캘리브레이션 게이지: 2D 패턴 다수

성능 비교:
  DRL (직접): 기존 순차적 캘리브레이션과 동등 RMSE
  DRL (VAE 4D): 더 안정적 수렴, 동등 RMSE
  DRL (PCA 4D): 비슷한 성능

  결론:
  - 정확도: 기존 방법 동등 달성
  - 자동화: 수동 파라미터 초기값 설정 불필요
  - 잠재력: 대규모 파라미터 공간에서 더 유리
```

## OPC 툴 구현 관련성
- **SKOPC 자동 캘리브레이션**: `skopc/modeling/` 기존 캘리브레이션 루틴에 DRL 기반 자동 파라미터 탐색 추가
- **VAE 임베딩**: OPC 파라미터 공간의 저차원 표현 학습 모듈
- **환경 설계**: `skopc/core/litho_engine.py`를 DRL 환경으로 래핑하는 gym-compatible 인터페이스
- **TSMC 검증**: TSMC 출신 저자진의 양산 검증, SKOPC의 레퍼런스로 활용 적합

## 참고문헌
- Proc. SPIE 13425, DTCO and Computational Patterning IV (2025)
- 저자 소속: TSMC (Taiwan Semiconductor Manufacturing Company)
- 관련: Automated sample plan for OPC calibration (SPIE 9052, 2014)
- 관련: Effective OPC model calibration using machine learning (SPIE 12052, 2022)
- 관련: Roadmap to sub-nanometer OPC model accuracy (SPIE 8441, 2012)

## 태그
`Recipe`, `SPIE`, `OPC-ModelCalibration`, `DeepReinforcementLearning`, `RL`, `VAE`, `PCA`, `ParameterOptimization`, `TSMC`, `VIA`, `AutoCalibration`, `2025`
