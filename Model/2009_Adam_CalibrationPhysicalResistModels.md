# Calibration of Physical Resist Models: Methods, Usability, and Predictive Power

## 메타데이터
- **저자**: Adam, K. et al. (Mentor Graphics)
- **연도**: 2009
- **게재지**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 8, No. 3
- **DOI/URL**: https://doi.org/10.1117/1.3224949
- **인용수**: ~85

## 핵심 요약
리고러스 리소그래피 시뮬레이터용 물리 기반 레지스트 모델(PROLITH/S-Litho 류)의 캘리브레이션 방법론을 OPC 데이터셋을 활용하여 체계적으로 분석한다. 45nm half-pitch 기술 노드의 immersion 리소그래피를 대상으로 물리 모델 파라미터(Dill 상수, PEB 확산계수, 현상 속도 파라미터)의 최적 추정 절차와 예측력(predictive power)을 평가한다.

## 주요 기여
1. 물리 레지스트 모델 캘리브레이션을 위한 단계별 방법론 확립
2. OPC 캘리브레이션 데이터셋(대규모 1D/2D 게이지)에 물리 모델 적용
3. 물리 모델 파라미터의 sensitivity 분석: 어떤 파라미터가 CD 예측에 가장 중요한지
4. 물리 모델 vs. 컴팩트 모델(CM1/VTRE) 예측력 비교
5. 공정 윈도우 이식성(process window portability) 정량 평가

## 모델 수식/아키텍처

**Dill 노광 모델 (Dill ABC):**
```
∂M/∂t = -(A·M + B) · I(x,y,z,t)
dI/dz = -(A·M + B) · I   [Beer-Lambert]
```
A = bleachable 흡광계수, B = non-bleachable, C = 감광 반응 속도

**PEB 확산-반응 모델:**
```
∂[H]/∂t = D_H · ∇²[H] - k_q · [Q] · [H]
∂[Q]/∂t = -k_q · [Q] · [H]
```
[H] = 산 농도, [Q] = 염기(quencher) 농도, D_H = 산 확산계수

**현상 속도 (Mack 4파라미터):**
```
R(m) = R_max · (a+1)(1-m)^n / [a + (1-m)^n] + R_min
a = (n+1)/(n-1) · (1-m_th)^n
```
R_max, R_min, n, m_th = 4개 캘리브레이션 파라미터

**캘리브레이션 절차:**
```
Step 1: 광학 파라미터 고정 (NA, σ, aberration)
Step 2: Dill ABC 파라미터 추정 (박막 측정)
Step 3: PEB 파라미터 (D_H, k_q) 피팅 (Focus-Exposure Matrix)
Step 4: 현상 파라미터 (R_max, n, m_th) 피팅 (CD-SEM)
Step 5: 전체 파라미터 동시 최적화 (Levenberg-Marquardt)
```

**파라미터 Sensitivity 분석:**
```
S_i = (∂CD/∂p_i) · (p_i / CD)  [무차원 sensitivity]
```

## 모델 유형
- [x] 광학 모델 (Dill 노광)
- [x] 레지스트 모델 (물리 기반 PEB + 현상)
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- 물리 레지스트 모델은 OPC 컴팩트 모델 캘리브레이션의 기준(ground truth)으로 활용
- skopc 리고러스 시뮬레이터 구현 시 핵심 참조
- Dill ABC → PEB → 현상 순차 파이프라인 구현
- 컴팩트 모델(CM1)과의 연계: 리고러스 시뮬레이션 데이터로 컴팩트 모델 캘리브레이션

## 참고문헌
- Mack, C.A., "PROLITH: A Comprehensive Optical Lithography Model" (1985)
- Dill, F.H. et al., "Characterization of positive photoresist" (1975)
- Mack, C.A., "Analytical expression for the standing wave intensity in photoresist" (1986)

## 태그
`Model`, `SPIE-JMM`, `PhysicalModel`, `ResistCalibration`, `Dill`, `PEB`, `Development`, `PROLITH`, `45nm`, `Immersion`, `2009`
