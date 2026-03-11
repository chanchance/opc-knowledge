# MEEF-Based Correction to Achieve OPC Convergence of Low-k1 Lithography with Strong OAI

## 메타데이터
- **저자**: Mack, C. A. et al. (KLA-Tencor / Lithoguru)
- **연도**: 2006
- **게재지**: Proc. SPIE 6154, Optical Microlithography XIX
- **DOI/URL**: https://doi.org/10.1117/12.656894
- **인용수**: ~50

## 핵심 요약
강한 오프-액시스 조명(OAI)을 사용하는 저-k1 리소그래피에서 MEEF(Mask Error Enhancement Factor)와 NILS(Normalized Image Log-Slope)가 패턴 방향·형상에 따라 크게 달라짐을 분석한다. MEEF 기반 보정 방법을 PID 컨트롤러와 결합하여 전체적인 OPC 수렴을 달성하는 새로운 프레임워크를 제안한다. 저-k1 공정에서의 OPC 수렴 문제를 MEEF 관점에서 해석하고 해결책을 제시한다.

## 주요 기여
1. 강한 OAI 조건에서 MEEF의 방향·형상 의존성 정량 분석
2. MEEF 기반 OPC 수렴 가속 알고리즘 제안
3. PID + MEEF 결합 컨트롤러로 전체 칩 OPC 수렴 달성
4. 저-k1 패터닝에서 MEEF가 OPC 정확도에 미치는 영향 체계화
5. MEEF 계산을 OPC 엔진 내에 통합하는 효율적 구현 방법

## 모델 수식/아키텍처

**MEEF 정의:**
```
MEEF = ∂CD_wafer / ∂CD_mask × M
```
M = 마스크 축소비 (보통 4×)
MEEF > 1: 마스크 CD 오차가 웨이퍼에서 증폭됨

**MEEF와 NILS의 관계:**
```
MEEF = 1 / (NILS × k₁_eff)
NILS = (1/I) · |dI/dx|_edge × CD
k₁_eff = 유효 k₁ 인자
```
→ NILS가 낮을수록 MEEF 높아짐 (저-k1에서 MEEF 급증)

**MEEF 기반 OPC 보정량 계산:**
```
δmask = δCD_target / MEEF_local
```
δmask = 마스크 보정량, δCD_target = 목표 CD 보정량

**PID + MEEF 컨트롤러:**
```
mask_correction(n+1) = mask_correction(n)
  + Kp · EPE(n) / MEEF(n)
  + Ki · Σ EPE(k) / MEEF(k)
  + Kd · (EPE(n) - EPE(n-1)) / MEEF(n)
```
Kp, Ki, Kd = PID 이득 계수

**OPC 수렴 조건:**
```
max|EPE| < EPE_tolerance  (보통 1nm 이하)
MEEF_range: 1 (DUV, low NA) ~ 10+ (저-k1, 강한 OAI)
```

## 모델 유형
- [x] 광학 모델 (MEEF 계산)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc OPC 엔진 수렴 알고리즘에 MEEF 기반 스텝 크기 제어 추가
- MEEF 계산: 공중상 기울기(NILS)로부터 실시간 계산 가능
- 강한 OAI(Dipole, Quasar 조명)에서 MEEF 방향 의존성이 OPC 불안정 원인
- PID 컨트롤러의 이득 계수를 MEEF로 정규화하면 수렴 안정성 향상
- EUV 저-k1(k1 < 0.35) 패터닝에서 더욱 중요

## 참고문헌
- Cobb, N., "Fast optical and process proximity correction" (1998)
- Mack, C.A., "Fundamental Principles of Optical Lithography" (textbook)
- Rosenbluth, A.E. et al., "Optimum mask and source patterns" (2002)

## 태그
`Model`, `SPIE`, `MEEF`, `NILS`, `OPC`, `Convergence`, `LowK1`, `OAI`, `PIDController`, `2006`
