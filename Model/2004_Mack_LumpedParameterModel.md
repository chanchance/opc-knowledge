# Lumped Parameter Model for Chemically Amplified Resists

## 메타데이터
- **저자**: Chris A. Mack
- **연도**: 2004
- **게재지/학회**: SPIE Optical Microlithography XVII, Vol. 5377
- **DOI/URL**: https://doi.org/10.1117/12.537583
- **인용수**: 150+

## 핵심 요약
화학 증폭형 레지스트(CAR: Chemically Amplified Resist)를 위한 Lumped Parameter Model (LPM)을 체계화한 논문. 복잡한 반응-확산 방정식 대신 이미지 강도의 가우시안 근사를 통해 해석적 표현식을 유도, 계산 속도를 크게 향상시킨다. LPM은 노광 후 베이크(PEB) 확산 및 현상(development) 효과를 경험적 파라미터로 통합(lumping)하여 단일 보정 과정에서 처리한다. 산업계 full-chip OPC 모델에서 가장 광범위하게 채택된 레지스트 모델 클래스이다.

## 주요 기여
- CAR용 Lumped Parameter Model 수학적 정식화
- 가우시안 근사를 이용한 LPM 해석적 적분 공식 유도
- PEB 확산 길이, 현상 파라미터를 단일 lumped 파라미터로 통합
- 기존 복잡 모델 대비 10~100배 계산 속도 향상 입증
- OPC 보정 패턴 커버리지와 모델 수렴 관계 분석

## 모델 아키텍처/수식
LPM의 핵심 수식 (가우시안 근사):

이미지 강도를 엣지 근방에서 가우시안으로 근사:
```
I(x) ≈ I₀ · exp[-(x - x_edge)² / (2σ²)]
```

LPM 적분 (현상 임계값 T에서의 CD):
```
CD = 2 · σ · √(2 · ln(I₀/T))
```

PEB 확산 포함 시:
```
I_peb(x) = I(x) ⊗ G(x; σ_peb)
```
여기서 G는 확산 길이 σ_peb를 가진 가우시안 커널.

통합 Lumped 파라미터:
```
σ_eff² = σ_optical² + σ_peb²
```

보정 파라미터 세트: {T, σ_peb, 선형 보정계수}
- T: 현상 임계 농도 (normalized)
- σ_peb: PEB 확산 길이
- 비선형 보정을 위한 추가 다항식 항

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [ ] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC `skopc/modeling/` 내 `LithoEngine` 및 레지스트 모델 구현에 직접 활용. TorchResist의 내부 convolution 기반 레지스트 시뮬레이션과 개념적으로 동일하며, LPM은 TorchResist 없이도 numpy만으로 구현 가능한 경량 fallback 모델로 사용할 수 있다. 특히 calibration 루틴에서 scipy.optimize로 {T, σ_peb} 파라미터를 CD-SEM 데이터에 fitting할 때 이 수식을 참조.

## 참고문헌 (핵심)
- Mack, C.A., "Analytical expression for the standing wave intensity in photoresist," Appl. Opt. 25(12), 1986
- Mack, C.A., "PROLITH: A comprehensive optical lithography model," SPIE 538 (1985)
- Cobb, N. and Zakhor, A., "Variable threshold resist model for lithography simulation," SPIE 3679 (1999)
- Brunner, T.A., "Approximate models for resist processing effects," SPIE 2726 (1996)
- Mack, C.A., "Process sensitivity and optimization with full and simplified resist models," SPIE 5040 (2003)

## 태그
`Model`, `OPC`, `ResistModel`, `LPM`, `LumpedParameter`, `CAR`, `PEB`, `Diffusion`, `Calibration`, `CompactModel`, `FullChip`
