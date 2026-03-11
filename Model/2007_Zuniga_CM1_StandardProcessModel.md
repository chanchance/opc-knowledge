# Toward Standard Process Models for OPC

## 메타데이터
- **저자**: Zuniga, C. et al. (Mentor Graphics)
- **연도**: 2007
- **게재지**: Proc. SPIE 6520, Optical Microlithography XX
- **DOI/URL**: https://doi.org/10.1117/12.712229
- **인용수**: ~80

## 핵심 요약
OPC 및 OPC 검증을 위한 표준 컴팩트 레지스트 모델인 Compact Model 1(CM1)의 수식과 캘리브레이션 방법론을 체계적으로 기술한다. CM1은 모델 계수에 대해 선형(linear in parameters)이어서 캘리브레이션이 용이하고, 장거리 로딩 효과(long-range loading)를 포함하는 항을 내장한다. 실험 데이터와의 비교를 통해 모델 예측 정확도를 검증한다.

## 주요 기여
1. Calibre CM1 레지스트 모델의 공식 수식 정의 및 문서화
2. 모델이 파라미터에 대해 선형 → 최소자승(least-squares) 캘리브레이션 가능
3. 장거리 로딩 보정 항(long-range loading term) 내장
4. CM0 대비 캘리브레이션 속도 대폭 향상
5. OPC 검증 루프에서의 표준 모델로 채택 가이드라인 제시

## 모델 수식/아키텍처

**CM1 Edge Placement 예측:**
```
EPE = Σ_k [ c_k · f_k(I, ∂I/∂n, ∂²I/∂n², ...) ]
```
여기서:
- EPE = Edge Placement Error (레지스트 엣지 위치 오차)
- c_k = 캘리브레이션 계수 (선형)
- f_k = 공중상(aerial image) 기반 특징 함수들
- I = 공중상 강도
- ∂I/∂n = 노말 방향 강도 기울기

**주요 특징 함수들:**
```
f_1 = I(edge)              # 엣지에서의 광강도
f_2 = (∂I/∂n)|_edge       # 강도 기울기 (image slope)
f_3 = ∫ I(x) dx            # 장거리 로딩 (Gaussian 가중 적분)
f_4 = I_peak               # 피크 강도
f_5 = (∂²I/∂n²)|_edge     # 2차 미분 (curvature)
```

**캘리브레이션 (선형 최소자승):**
```
min_{c} ||EPE_meas - Σ_k c_k · f_k||²
```

**장거리 로딩 항:**
```
f_load = ∫∫ I(x',y') · G_σ(x-x', y-y') dx'dy'
```
G_σ = σ ~ 수백 nm 범위의 가우시안 커널

## 모델 유형
- [x] 광학 모델 (공중상 특징 기반)
- [x] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- CM1은 Calibre OPC의 기본 컴팩트 레지스트 모델 → skopc의 핵심 구현 대상
- 선형 파라미터 구조 덕분에 캘리브레이션 속도 빠름 (수천 개 게이지 포인트 처리 가능)
- 공중상 계산(TCC/SOCS) + CM1 예측 파이프라인이 현대 OPC 툴의 표준
- skopc/modeling/compact_model/cm1.py 구현 시 직접 참조
- 파라미터: 광학 파라미터(NA, σ, 수차) + CM1 계수 c_k + 로딩 σ

## 참고문헌
- Mack, C.A., "Lumped Parameter Model for Optical Lithography" (2004)
- Cobb, N., "Variable Threshold Resist Model" (1999)
- Mentor Graphics Calibre documentation

## 태그
`Model`, `SPIE`, `ResistModel`, `CM1`, `CompactModel`, `OPC`, `Calibration`, `LinearModel`, `2007`
