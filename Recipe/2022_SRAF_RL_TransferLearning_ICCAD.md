# Sub-Resolution Assist Feature Generation with Reinforcement Learning and Transfer Learning

## 메타데이터
- **저자**: (IEEE ICCAD 2022)
- **연도**: 2022
- **게재지**: 2022 IEEE/ACM International Conference on Computer-Aided Design (ICCAD)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10069974
- **인용수**: ~25

## 핵심 요약
강화 학습(RL)과 전이 학습(Transfer Learning)을 결합하여 SRAF(Sub-Resolution Assist Feature) 배치를 자동화하는 방법을 제안한다. RL 에이전트가 SRAF 삽입 정책을 학습하고, 전이 학습으로 훈련된 정책을 새로운 패턴이나 공정 조건에 빠르게 적응시킨다. 리소그래피 공정 윈도우(PV Band, DOF, EL)를 RL 보상으로 직접 최적화하여 공정 윈도우 인식 SRAF 배치를 달성한다.

## 주요 기여
1. RL 에이전트로 SRAF 삽입 정책 직접 학습 (공정 윈도우 보상)
2. 전이 학습으로 새 패턴/공정 조건에 빠른 정책 적응
3. 공정 윈도우(PV Band, DOF, EL)를 RL 보상으로 직접 최적화
4. 기존 Rule-based + Model-based SRAF 대비 공정 마진 개선

## Recipe/Process Flow 상세

### RL 기반 SRAF 배치의 설계
```
기존 SRAF 방법의 한계:
  Rule-based: 빠름, 복잡한 2D 패턴 처리 부족
  Model-based: 정확, 매우 느림 (수 시간/전체 칩)
  GAN 기반: 빠름, 훈련 데이터 의존, 새 패턴 일반화 어려움

RL 적용 동기:
  SRAF 배치 = 순차적 의사결정 문제:
    어디에 SRAF를 놓을지 (위치)
    얼마나 크게 놓을지 (크기)
    몇 개 놓을지 (수량)
  보상: 리소그래피 공정 윈도우 직접 최대화
  → 목적 함수와 최적화 목표 일치

전이 학습 동기:
  각 새 패턴에 RL 처음부터 훈련: 비효율
  훈련된 정책 → 새 패턴에 전이: 빠른 적응
  공정 노드 변경 시: 물리적 유사성 활용 전이
```

### RL 환경 설계
```
상태 (State):
  현재 레이아웃 + 기존 SRAF 배치 이미지
  항공 이미지 I(현재 마스크)
  리소그래피 메트릭: 현재 PV Band, EPE
  → 에이전트가 현재 상태 인식

액션 (Action):
  이산 액션:
    위치: (x, y) 격자 좌표에 SRAF 추가/제거
    크기: SRAF 폭/길이 선택 (설계 규칙 내 이산값)
    방향: H 또는 V
  연속 액션 (일부 구현): 위치/크기 연속값

보상 (Reward):
  r = w_PVB × ΔPVB + w_EPE × ΔEPE + w_MRC × ΔMRC
  ΔPVB: PV Band 감소 → 양의 보상
  ΔEPE: EPE 감소 → 양의 보상
  ΔMRC: MRC 위반 → 음의 보상 (페널티)
  → 공정 윈도우 직접 최대화

종료 조건:
  최대 SRAF 수 도달
  PV Band 목표 달성
  MRC 위반 발생
```

### 정책 네트워크
```
에이전트 구조:
  CNN 인코더: 레이아웃 + SRAF 이미지 → 특징
  LSTM: 순차적 SRAF 삽입 이력 기억
  Actor: 다음 SRAF 위치/크기 정책
  Critic: 현재 상태 가치 평가 (PPO용)

알고리즘: PPO (Proximal Policy Optimization)
  안정적 정책 업데이트
  클리핑: 정책 급변 방지
  병렬 환경: 다수 클립 동시 훈련
```

### 전이 학습 전략
```
사전 훈련:
  다양한 1D/2D 패턴으로 기본 SRAF 정책 훈련
  일반적인 SRAF 배치 규칙 학습

전이 대상:
  새 패턴 유형 (복잡한 2D, 비정형)
  새 공정 노드 (다른 λ, NA)
  새 설계 규칙 (MRC 변경)

전이 방법:
  파인 튜닝: 사전 훈련 가중치에서 소수 에피소드 학습
  피처 전이: CNN 인코더 고정, Actor/Critic만 재훈련
  효과: 처음부터 훈련 대비 수배 빠른 수렴
```

### 성능 결과
```
공정 윈도우:
  RL + 전이 학습 SRAF: Rule-based 대비 개선
  Model-based SRAF와 유사하거나 근접

런타임:
  훈련 후 추론: Rule-based와 유사한 속도
  전이 학습: 새 패턴 빠른 적응 (Model-based 대비 수십 배 빠름)

일반화:
  전이 학습: 새 패턴 유형에서도 합리적 SRAF 배치
  RL 보상: 실제 공정 윈도우 목표와 직접 일치
```

## OPC 툴 구현 관련성
- **SKOPC RL-SRAF**: `skopc/modeling/sraf_generator.py`에 RL 기반 SRAF 삽입 정책 추가
- **공정 윈도우 보상**: TorchLitho 시뮬로 PV Band 보상 계산 → RL 훈련
- **전이 학습**: 기본 노드 RL 정책 → 신규 노드 빠른 SRAF 정책 전이
- **PPO 구현**: PyTorch PPO로 SKOPC SRAF RL 에이전트 구현

## 참고문헌
- ICCAD 2022; IEEE Xplore: https://ieeexplore.ieee.org/document/10069974
- 관련: GAN SRAF placement (SPIE 11613, 2021)
- 관련: CTM-SRAF (TCAD 2023)
- 관련: LLM-SRAF (DATE 2025)
- 관련: A2-ILT RL (DAC 2022)

## 태그
`Recipe`, `ICCAD`, `SRAF`, `ReinforcementLearning`, `TransferLearning`, `PPO`, `ProcessWindow`, `PVBand`, `RL`, `PolicyGradient`, `2022`
