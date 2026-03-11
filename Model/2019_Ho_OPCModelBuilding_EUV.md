# OPC Model Building for EUV Lithography

## 메타데이터
- **저자**: Ho, B. C. P., Doebler, J., Niroomand, A. (Synopsys)
- **연도**: 2019
- **게재지**: Proc. SPIE 11147, International Conference on Extreme Ultraviolet Lithography 2019
- **DOI/URL**: https://doi.org/10.1117/12.2531430
- **인용수**: ~35

## 핵심 요약
EUV 리소그래피를 위한 OPC 모델 빌딩의 실제적 방법론을 제시한다. EUV 특유의 현상인 비텔레센트릭 조명에 의한 그림자 효과(shadowing), 슬릿 위치에 따른 변화(across-slit variation), 광학적 플레어(flare), 레티클 블랙 보더(black border) 효과를 OPC 모델에 통합하는 방법을 구체적으로 기술한다. 실제 NXE 스캐너 데이터 기반의 캘리브레이션 결과를 제시한다.

## 주요 기여
1. EUV OPC 모델의 전체 구성 요소(광학+레지스트+M3D+플레어) 통합 방법론
2. 비텔레센트릭 그림자 효과의 컴팩트 모델 통합
3. Across-slit 변화 보정을 OPC 모델에 내장하는 방법
4. 광학 플레어 모델 캘리브레이션 (장거리 PSF 피팅)
5. 레티클 블랙 보더 효과의 OPC 모델 표현

## 모델 수식/아키텍처

**EUV 비텔레센트릭 그림자 모델:**
```
CD_shadow(x_slit) = CD_nominal + α · x_slit · H_abs · tan(θ_chief) / M_optical
```
x_slit = 슬릿 내 위치, H_abs = 흡수체 높이, M_optical = 광학 축소비

**Across-Slit 변화 모델:**
```
CD(x_slit, pattern) = CD₀(pattern) + Σ_k a_k(pattern) · B_k(x_slit)
```
B_k = 슬릿 방향 기저함수 (다항식 또는 Zernike)

**플레어 모델 (Long-Range PSF):**
```
I_flare(x,y) = (1-F) · I_signal(x,y) + F · [I_signal * PSF_flare](x,y)
PSF_flare(r) = A₁·exp(-r²/σ₁²) + A₂·exp(-r²/σ₂²)   [이중 가우시안]
```
F = 총 플레어 레벨, σ₁ ~ 수십 μm, σ₂ ~ 수 mm

**통합 EUV OPC 모델:**
```
CD_predicted = f_OPC(I_aerial, I_flare, shadow_correction, slit_correction, resist_model)
```

**캘리브레이션 데이터 요구사항:**
- 슬릿 위치 의존성 파악: 슬릿 전체 범위의 게이지 패턴 필요
- H/V 방향 그림자 차이 파악: 수평/수직 라인 모두 포함
- 다양한 피치/CD 범위: 16nm ~ 200nm pitch

## 모델 유형
- [x] 광학 모델 (EUV 광학계, 플레어, 그림자)
- [x] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- EUV OPC 모델 구현 필수 체크리스트:
  1. 비텔레센트릭 그림자 효과 (방향/슬릿 위치 의존)
  2. Across-slit 변화 보정 (다항식 기저함수)
  3. 장거리 플레어 모델 (이중 가우시안 PSF)
  4. 레티클 블랙 보더 효과
  5. EUV 특유의 확률론적 레지스트 효과
- skopc/modeling/euv_model/ 핵심 구현 참조
- NXE:3400/3600 스캐너 기준 파라미터 범위 제공

## 참고문헌
- Neureuther, A.R. et al., "EUV OPC modeling requirements" (2014)
- Gallatin, G.M. et al., "Stochastic EUV resist model calibration" (2012)
- ASML NXE scanner specifications

## 태그
`Model`, `SPIE`, `EUV`, `OPCModel`, `Shadowing`, `AcrossSlit`, `Flare`, `Calibration`, `NXE`, `2019`
