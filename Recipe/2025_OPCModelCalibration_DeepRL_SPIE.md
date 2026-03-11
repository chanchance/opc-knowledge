# OPC Model Calibration Using Deep Reinforcement Learning

## 메타데이터
- **저자**: Weilun Chiu, Tony Hu, Terry Hsuan, Elvis Yang, T. H. Yang, K. C. Chen (Macronix International Co., Ltd.)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134251N (April 2025)
- **DOI/URL**: https://doi.org/10.1117/12.3049598
- **인용수**: ~3

## 핵심 요약
딥 강화학습(Deep RL)을 OPC 모델 캘리브레이션에 적용하는 새로운 방법을 제안한다. OPC 모델 캘리브레이션의 핵심 과제인 최적 OPC 모델 항(term) 조합 선택과 해당 파라미터 회귀를 강화학습 에이전트가 자동으로 수행하여 모델 예측 오차를 최소화한다. 기존 전문가 지식 기반 수동 모델 항 선택의 비효율성을 해결하고 캘리브레이션 사이클을 자동화한다.

## 주요 기여
1. 딥 RL 에이전트로 OPC 모델 항 조합 자동 탐색 및 선택
2. OPC 모델 예측 오차 최소화를 RL 목표로 설정
3. 전문가 기반 수동 모델 선택 대비 자동화된 캘리브레이션 워크플로우
4. Macronix 메모리 디바이스에서의 실제 적용 검증

## Recipe/Process Flow 상세

### OPC 모델 캘리브레이션 문제 정의
```
기존 OPC 모델 캘리브레이션:
  입력: SEM 측정 게이지 데이터 (CD vs. 레이아웃 패턴)
  목표: 리소그래피 + 에칭 물리 현상을 모사하는 컴팩트 모델 파라미터 찾기

컴팩트 모델 구조:
  모델 항 (Model Terms):
    - 광학 항: 초점, 노광량, 수차 의존성
    - 레지스트 항: 확산, 임계 값, 비선형성
    - 에칭 항: 마이크로로딩, 등방/이방성 에칭
    - 고차 항: 2D 패턴 보정, 코너 라운딩
  → 항 조합: 수십~수백 가지 가능한 조합

기존 방법의 한계:
  전문가 수동 선택:
    - 특정 공정/노드에 맞는 모델 항 경험 기반 선택
    - 시간 소요: 모델러 전문 지식 필요
    - 비최적: 국소 최적해에 수렴 가능
  그리드 탐색:
    - 항 조합 공간 지수적 증가 → 계산 불가
```

### 딥 RL 프레임워크
```
MDP (Markov Decision Process) 정의:
  상태 (State):
    - 현재 선택된 모델 항 집합
    - 각 항의 현재 파라미터 값
    - 현재 모델 RMS EPE (예측 오차)
    - 캘리브레이션 이터레이션 수

  액션 (Action):
    - 모델 항 추가/제거/수정
    - 회귀 파라미터 업데이트
    - 다음 탐색 방향 선택

  보상 (Reward):
    r = -RMS_EPE_after + w × complexity_penalty
    - RMS EPE 감소 → 양의 보상
    - 모델 복잡도 (항 수) → 패널티 (오버피팅 방지)

  정책 네트워크:
    - DNN: 현재 상태 → 다음 액션 확률
    - Actor-Critic (PPO): 안정적 정책 학습
```

### 캘리브레이션 워크플로우
```
1. 초기화:
   게이지 데이터 로드: SEM 측정 CD 값
   기본 모델 항: 최소한의 항으로 시작

2. RL 탐색:
   에피소드: 한 번의 캘리브레이션 시도
   각 스텝:
     - 현재 상태 인코딩
     - 정책 네트워크 → 다음 액션 선택
     - 액션 실행: 모델 항 변경
     - 리소그래피 시뮬: 변경된 모델로 CD 예측
     - 보상: RMS EPE 계산

3. 정책 업데이트:
   다수 에피소드 경험 수집
   PPO 업데이트: 보상 기반 정책 개선

4. 수렴:
   최적 모델 항 조합 발견
   최종 파라미터 미세 조정 회귀

5. 검증:
   독립 검증 게이지로 모델 성능 확인
   OPC 런 → 실제 칩 패턴 검증
```

### 성능 결과
```
모델 정확도:
  Deep RL 캘리브레이션:
    - RMS EPE: 전문가 수동 선택 대비 개선
    - 모델 항 조합: 자동으로 최적 조합 발견

효율성:
  캘리브레이션 시간: 자동화로 인력 투입 감소
  탐색 공간: RL이 지능적 탐색 → 그리드 탐색 대비 효율

실용성:
  Macronix 메모리 공정 적용 검증
  실제 제조 게이지 데이터로 훈련/검증
```

## OPC 툴 구현 관련성
- **SKOPC 모델 캘리브레이션**: RL 기반 자동 모델 항 선택으로 SKOPC 캘리브레이션 자동화
- **모델 복잡도 제어**: RL 보상의 복잡도 패널티로 오버피팅 없는 최적 모델 선택
- **캘리브레이션 가속**: RL 에이전트 재사용으로 유사 공정 캘리브레이션 빠른 초기화
- **Macronix 사례**: 메모리 디바이스 OPC 모델 캘리브레이션 실용 사례

## 참고문헌
- Proc. SPIE 13425, DTCO and Computational Patterning IV, 134251N (February 2025)
- 저자 소속: Macronix International Co., Ltd.
- 관련: Effective OPC model calibration using ML (SPIE 12052, 2022)
- 관련: Massive metrology e-beam OPC model accuracy (SPIE 10585, 2018)
- 관련: CAMO RL-based OPC (DAC 2024)

## 태그
`Recipe`, `SPIE`, `OPCModel`, `ModelCalibration`, `ReinforcementLearning`, `DeepLearning`, `GaugeSampling`, `Macronix`, `Memory`, `AutomatedCalibration`, `2025`
