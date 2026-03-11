# Inverse Lithography Physics-Informed Deep Neural Level Set for Mask Optimization

## 메타데이터
- **저자**: Xing-Yu Ma, Hao Yang, et al.
- **연도**: 2023
- **게재지**: Applied Optics, Vol. 62, pp. 8769–8779 (2023); arXiv:2308.12299
- **DOI/URL**: https://opg.optica.org/ao/abstract.cfm?uri=ao-62-33-8769
- **인용수**: ~20

## 핵심 요약
레벨셋 기반 ILT와 물리 정보 기반 딥러닝을 결합한 ILDLS(Inverse Lithography physics-informed Deep neural Level Set) 마스크 최적화 방법을 제안한다. ILT를 딥러닝 프레임워크 내의 레이어로 통합하여 마스크 예측과 보정을 반복 수행함으로써, 순수 딥러닝 또는 ILT 단독 대비 인쇄 가능성과 공정 윈도우를 크게 향상시킨다. ILT 대비 수 자릿수의 계산 시간 감소를 달성한다.

## 주요 기여
1. ILT 레벨셋 최적화를 딥러닝 레이어로 통합하는 물리 정보 기반 프레임워크
2. 마스크 예측-보정 반복 구조로 인쇄 가능성과 공정 윈도우 동시 향상
3. ILT 대비 수 자릿수 계산 시간 감소
4. 순수 DL + ILT 혼합으로 두 방법의 장점 결합

## Recipe/Process Flow 상세

### 기존 ILT와 DL 방법의 한계
```
레벨셋 ILT:
  마스크 M을 레벨셋 함수 φ(x)의 부호로 표현:
    M(x) = H(φ(x))  (H: 헤비사이드 함수)
  최적화: ∂φ/∂t = -∇_φ L_litho(H(φ))
  장점: 위상학적으로 유연한 마스크 형상
  단점: 느림 (수천~수만 이터레이션), 국소 최적 위험

순수 DL (Neural-ILT 계열):
  훈련 후 단일 순방향 패스 → 빠름
  단점:
    일반화: 훈련 분포 밖 패턴에서 품질 저하
    ILT 동역학 무시: 수렴 마스크 아닌 근사 마스크

ILDLS 목표:
  ILT 최적화 구조 내재화 + DL 가속 결합
```

### ILDLS 아키텍처
```
물리 정보 기반 딥러닝 구조:

1단계 - 신경망 마스크 초기화:
  입력: 타겟 레이아웃 이미지
  U-Net → 레벨셋 초기값 φ_0(x) 생성
  목적: ILT 수렴에 유리한 초기값 제공

2단계 - 내장 ILT 레벨셋 최적화 (물리 레이어):
  φ_0 → [ILT 레벨셋 이터레이션] → φ_T
  ILT 스텝을 미분 가능 레이어로 구현:
    φ_{t+1} = φ_t - η × ∇_φ L_litho(H(φ_t))
  반복 횟수 T: 10~50 스텝 (완전 ILT의 수백 분의 1)

3단계 - 출력:
  M* = H(φ_T)  → 최적화된 이진 마스크
  반복적 예측-보정: DL 초기화 → ILT 수렴 → DL 재조정

손실 함수:
  L_ILDLS = L_EPE + λ_PW × L_PW + λ_MRC × L_MRC
  L_PW: 다양한 (Focus, Dose) 조건의 공정 윈도우 손실
```

### 미분 가능 리소그래피 모델
```
Hopkins 광학 모델 (PyTorch):
  항공 이미지 I(M) = Σ_k |TCC_k| × |FT(M)|²
  완전 미분 가능 → φ에 대한 기울기 계산 가능

레벨셋 미분 근사:
  ∂H(φ)/∂φ ≈ δ(φ) (디락 델타 → 부드러운 근사)
  실제: δ_ε(φ) = ε/(π(φ² + ε²))

VLIM (변동 리소그래피 모델) 통합:
  공정 변동 (Focus, Dose) 하의 이미지 계산
  L_PW = Σ_{(F,D)∈PW} ||I(M, F, D) - I_target||²
```

### 성능 결과
```
EPE (인쇄 가능성):
  ILDLS: 순수 DL 대비 15~25% EPE 감소
  ILDLS: ILT 대비 동등하거나 근접

공정 윈도우 (DOF × EL):
  ILDLS: 순수 DL 대비 확장
  ILDLS: ILT 대비 동등하거나 우수

계산 시간:
  완전 ILT: 수초~수분/클립
  ILDLS: 수십 ms/클립 (수십~수백 배 빠름)
  T=10 스텝: ILT 품질의 90%+, 100× 빠름
```

## OPC 툴 구현 관련성
- **SKOPC ILDLS**: `skopc/modeling/openilt_adapter.py`에 ILDLS 레벨셋 물리 레이어 추가
- **미분 가능 시뮬레이터**: TorchLitho로 ILDLS 내장 ILT 이터레이션 구현
- **레벨셋 표현**: SKOPC ILT 백엔드에 레벨셋 마스크 표현 추가
- **공정 윈도우 손실**: L_PW 구현으로 ILDLS 공정 윈도우 직접 최적화

## 참고문헌
- Applied Optics, Vol. 62, pp. 8769–8779 (2023); arXiv:2308.12299
- 관련: DevelSet - Deep Neural Level Set (ICCAD 2021 / TCAD 2023)
- 관련: Neural-ILT (ICCAD 2020 / TCAD 2022)
- 관련: Level set ILT (Granik, SPIE, 2004)
- 관련: VLIM process variation (SPIE, DAC 2006)

## 태그
`Recipe`, `AppliedOptics`, `ILT`, `LevelSet`, `PhysicsInformed`, `NeuralNetwork`, `MaskOptimization`, `ProcessWindow`, `EPE`, `DifferentiableSimulation`, `2023`
