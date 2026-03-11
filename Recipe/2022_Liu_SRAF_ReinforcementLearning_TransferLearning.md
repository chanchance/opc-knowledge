# Sub-Resolution Assist Feature Generation with Reinforcement Learning and Transfer Learning

## 메타데이터
- **저자**: G.-T. Liu, W.-C. Tai, Y.-T. Lin, I.H.-R. Jiang, J.P. Shiely, P.-J. Cheng
- **연도**: 2022 (ICCAD 발표), IEEE 문서 10069974
- **게재지**: IEEE/ACM International Conference on Computer-Aided Design (ICCAD 2022)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10069974/
- **인용수**: ~20

## 핵심 요약
SRAF 생성에 강화학습(RL)을 최초로 적용한 연구. 기존 ML 기반 방법들이 SRAF 간 광학 간섭을 무시하고 사후 처리로 마스크 규칙을 맞추는 한계를 극복한다. RL 에이전트가 SRAF 간 간섭을 직접 고려하여 마스크 규칙 준수 결과를 생성하며, 2단계 학습 방식으로 model-based SRAF 스타일을 모방하면서 PV 밴드를 향상시킨다.

## 주요 기여
1. SRAF 생성에 RL 최초 적용 — SRAF 간 광학 간섭 직접 고려
2. 마스크 규칙 준수 SRAF를 사후 처리 없이 직접 생성
3. 2단계 학습: Phase 1(model-based SRAF 모방) + Phase 2(PV 밴드 향상)
4. 상태 정렬(state alignment) + 행동 변환(action transformation)으로 방향 등변성 달성

## Recipe/Process Flow 상세

### RL 기반 SRAF 생성 프레임워크
```
환경 (Environment):
  상태(State): 현재 마스크 레이아웃 + 기존 SRAF 배치 정보
  행동(Action): SRAF 추가/제거/수정
  보상(Reward): 공정 윈도우 지표 (PV 밴드, EPE) + 마스크 규칙 준수

에이전트 (Agent):
  정책 네트워크: 현재 상태 → SRAF 행동 확률
  CNN/U-Net 기반 상태 인코딩
```

### 2단계 학습 전략
```
Phase 1: Model-Based SRAF 모방 학습 (Imitation Learning)
  목표: model-based SRAF 결과를 모방하여 합리적 초기 정책 학습
  방법:
    - model-based SRAF 결과를 전문가 데모로 사용
    - 행동 복제 (Behavior Cloning): 전문가 행동 모방
    - 빠른 초기 정책 수렴
  효과: RL 훈련의 초기화 개선, 탐색 효율 향상

Phase 2: PV 밴드 향상 (RL Fine-tuning)
  목표: 공정 변동 밴드 최대화
  방법:
    - PPO(Proximal Policy Optimization) 또는 유사 알고리즘
    - 보상: PV 밴드 면적 + 마스크 규칙 페널티
    - Phase 1 정책에서 미세 조정
  효과: model-based SRAF 이상의 PV 밴드 달성
```

### 마스크 규칙 준수 메커니즘
```
기존 ML SRAF: 생성 후 사후 처리로 MRC 충족 시도 → 왜곡 가능

RL SRAF:
  - 행동 마스크 (Action Mask): 유효하지 않은 행동 차단
    * MRC 위반 행동 = 확률 0으로 설정
  - 보상 설계: MRC 위반 시 강한 음의 보상
  - 결과: 훈련 과정에서 MRC를 자연스럽게 학습
```

### 방향 등변성 (Orientation Equivariance)
```
문제: 레이아웃 회전/반전 시 동일한 SRAF 규칙 적용되어야 함
해결:
  - 상태 정렬 (State Alignment): 입력 정규화
  - 행동 변환 (Action Transformation): 출력 변환
  - 효과: 훈련 데이터 효율 향상 (4배 데이터 증강 효과)
```

### 성능 결과
```
PV 밴드: model-based SRAF 대비 향상 (RL fine-tuning 효과)
마스크 규칙: 직접 준수 (사후 처리 불필요)
EPE: 동등 또는 개선
런타임 (추론): ML 수준 (훈련 후 빠른 추론)
```

## OPC 툴 구현 관련성
- **SKOPC SRAF + PWO 통합**: RL 에이전트가 SRAF를 배치하는 동시에 공정 윈도우 최적화하는 방식은 `skopc/pwo/`와 `skopc/modeling/sraf_generator.py` 통합에 영감 제공
- **마스크 규칙 내장**: 행동 마스크로 MRC 자동 준수 — SKOPC DRC 통합과 연계 가능
- **2단계 학습**: 전문가 모방 → RL 개선 전략은 적은 데이터로 빠른 적응 가능
- **LARA/RL_OPC 연관**: 이미 수집된 2024_Liang_RL_OPC와 같은 RL-OPC 계열의 SRAF 버전

## 참고문헌
- IEEE ICCAD 2022, Document 10069974
- 관련: GAN-SRAF (IEEE TCAD, 2020)
- 관련: CTM-SRAF (IEEE TCAD, 2023)
- 관련: 2024_Liang_RL_OPC (이미 수집됨)

## 태그
`Recipe`, `IEEE`, `SRAF`, `ReinforcementLearning`, `TransferLearning`, `ImitationLearning`, `MaskRule`, `PVBand`, `OrientationEquivariance`, `ICCAD`, `2022`
