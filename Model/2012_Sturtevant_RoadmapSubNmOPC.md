# Roadmap to Sub-Nanometer OPC Model Accuracy

## 메타데이터
- **저자**: John L. Sturtevant, Edita Tejnil
- **연도**: 2012
- **게재지/학회**: SPIE Proc. 8441, Photomask and Next-Generation Lithography Mask Technology XIX, 84410H
- **DOI/URL**: https://doi.org/10.1117/12.978190
- **인용수**: 60+

## 핵심 요약
OPC 모델 정확도를 서브 나노미터 수준으로 향상시키기 위한 로드맵을 제시한 논문. OPC 모델은 포토마스크, 광학계, 레지스트, 에칭 전체 패터닝 공정을 기술하지만, aerial image가 직접 측정되지 않아 광학 모델 보정이 어렵다는 근본적 한계를 다룬다. 파장, NA, 조명 광원 프로파일, 박막 광학 상수 등 직접 측정 가능한 파라미터와 보정 필요 파라미터를 체계적으로 분류하고, 각 파라미터의 불확실도가 전체 모델 정확도에 미치는 영향을 분석한다.

## 주요 기여
- OPC 모델 정확도 향상을 위한 체계적 로드맵 제시
- 모델 파라미터를 직접 측정 가능/보정 필요로 체계적 분류
- 각 파라미터의 불확실도가 CD 예측 오차에 미치는 영향 정량화
- 서브 나노미터 정확도 달성을 위한 메트롤로지 요건 정의
- OPC 모델 보정 방법론의 한계와 개선 방향 제시

## 모델 아키텍처/수식
**OPC 모델 파라미터 분류:**

직접 측정/알려진 값:
```
- λ: 노광 파장 (193nm ArF, 248nm KrF, 13.5nm EUV)
- NA: 개구수 (측정 가능)
- σ: 부분 간섭 계수 (조명 프로파일)
- 박막 광학 상수 (n, k): 타원계측법으로 측정
- 마스크 패턴 치수: OCD/SEM 측정
```

보정 필요 파라미터:
```
광학 모델:
- 수차(aberration) 계수: Zernike 계수 Z₁, Z₂, ..., Z₃₇
- 광원 형상 세부 사항
- 플레어(flare) 맵

레지스트 모델:
- σ_blur: 레지스트 블러(확산+화학) 파라미터
- T: 현상 임계값
- NILS 의존성: VTR/LPM 파라미터

에칭 모델:
- bias_etch: 에칭 CD 편이
- 이방성 에칭 파라미터
```

**서브 나노미터 정확도 달성 조건:**

광학 파라미터 불확실도 → CD 불확실도:
```
σ_CD,optical ≈ (∂CD/∂NA)·δNA + (∂CD/∂σ_illum)·δσ + Σₙ (∂CD/∂Zₙ)·δZₙ
```

레지스트 파라미터 불확실도:
```
σ_CD,resist ≈ (∂CD/∂σ_blur)·δσ_blur + (∂CD/∂T)·δT
```

전체 CD 불확실도 (RSS):
```
σ_CD,total = √(σ_CD,optical² + σ_CD,resist² + σ_CD,etch² + σ_CD,metrology²)
```

서브 나노미터 목표: σ_CD,total < 1nm

**보정 방법론:**

Step 1: 광학 파라미터 고정 보정
```
최소제곱법: min_{NA, σ, Zₙ} Σᵢ (CD_sim(params)ᵢ - CD_meas,i)²
```
특수 감도 패턴(sensitivity gauge) 사용:
- NA 감도: 고밀도 1D 라인
- σ 감도: 격리/밀집 비율(ISO/dense ratio)
- 수차 감도: 비대칭 패턴

Step 2: 레지스트 모델 보정
```
광학 모델 고정 후: min_{σ_blur, T, VTR_params} Σᵢ (CD_sim,i - CD_meas,i)²
```

**메트롤로지 요건:**
CD-SEM 정확도 요건: < 0.3nm (서브 nm OPC를 위해)
샘플 크기: 최소 500~1000개 측정점
패턴 커버리지: CD 20~200nm, pitch 50~500nm 포함

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [ ] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 모델 보정 워크플로우 설계의 핵심 참조. `skopc/modeling/` 내 calibration 루틴 구현 시 이 논문의 2단계 보정(광학→레지스트) 전략을 따르는 것이 권장됨. 파라미터 민감도 분석으로 보정 우선순위 결정 가능. `recipes/example_arfimm.yaml`의 광학 파라미터(NA=1.35, σ 등)의 불확실도 범위 설정에 이 논문의 수치를 참조. 서브 나노미터 정확도 목표 달성을 위한 CD-SEM 측정 요건도 명시되어 있음.

## 참고문헌 (핵심)
- Hopkins, H.H., "On the diffraction theory of optical images," Proc. R. Soc. London A (1953)
- Mack, C.A., "PROLITH," SPIE 538 (1985)
- Cobb, N. and Zakhor, A., "Variable threshold resist model," SPIE 3679 (1999)
- Adam, K. et al., "Robust mask and source optimization for ArF immersion," SPIE (2009)

## 태그
`Model`, `OPC`, `Calibration`, `ModelAccuracy`, `SubNanometer`, `OpticalModel`, `ResistModel`, `Metrology`, `CDSEM`, `Zernike`, `Aberration`, `ProcessControl`, `SPIE`
