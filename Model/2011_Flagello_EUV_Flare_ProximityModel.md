# EUV Flare and Proximity Modeling and Model-Based Correction

## 메타데이터
- **저자**: Flagello, D. G. et al. (ASML / Brion Technologies)
- **연도**: 2011
- **게재지**: Proc. SPIE 7969, Optical Microlithography XXIV
- **DOI/URL**: https://doi.org/10.1117/12.879488
- **인용수**: ~70

## 핵심 요약
EUV 리소그래피에서 투영 광학계의 산란광에 의한 플레어(flare)가 보정 없이 수 nm의 온-웨이퍼 치수 변동을 유발함을 정량적으로 분석한다. 플레어와 근접 효과(proximity effects) 모두를 모델 기반으로 보정하는 통합 접근법을 개발하여 EUV OPC 정확도와 모델 신뢰도를 향상시킨다. 플레어 PSF(Point Spread Function)의 멀티-가우시안 분해를 통한 효율적 플레어 보정 모델을 제안한다.

## 주요 기여
1. EUV 플레어의 멀티-가우시안 PSF 모델 정립 및 캘리브레이션 방법론
2. 플레어 + 근접 효과 통합 모델 기반 OPC 보정 프레임워크
3. 보정 전/후 온-웨이퍼 CD 변동 정량 비교 (수 nm → ~0.5nm 수준)
4. EUV 광학계 특성(반사 광학, 멀티레이어 미러)에 의한 플레어 성분 분리
5. 전체 칩 플레어 보정 OPC 구현 가능성 실증

## 모델 수식/아키텍처

**EUV 플레어 모델 (멀티-가우시안 PSF):**
```
I_flare(x,y) = ∫∫ I_ideal(x',y') · PSF_flare(x-x', y-y') dx'dy'
PSF_flare(r) = Σ_k (A_k / (2π σ_k²)) · exp(-r² / (2σ_k²))
```
k = 1..K (K ~ 3~5개 가우시안 성분)
σ_k: 수십 nm ~ 수 mm 범위 (단거리~장거리 산란)
A_k: 각 성분의 플레어 기여 강도

**플레어 레벨 정의:**
```
F_total = ∫∫ PSF_flare(r) dr = Σ_k A_k  [전체 플레어 비율, %)
```
EUV 툴: F_total ~ 5-15% (193nm 대비 훨씬 높음)

**플레어 보정 OPC 목표:**
```
CD_target(x) = f(I_ideal(x) + I_flare(x))
→ mask_bias_flare(x) = g(I_flare(x), ∂I/∂CD)
```

**플레어 보정된 공중상:**
```
I_corrected(x) = I_ideal(x) + I_flare(x)
                ≈ I_ideal(x) · (1 + F_local(x))
F_local(x) = ∫∫ D(x') · PSF_flare(x-x') dx'  [로컬 플레어 레벨]
D(x') = 마스크 패턴 밀도
```

**통합 OPC 모델:**
```
EPE_total = EPE_proximity + EPE_flare(F_local) + EPE_shadowing
```

## 모델 유형
- [x] 광학 모델 (EUV 플레어, 산란)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- EUV OPC 플로우에서 플레어 보정은 별도 전처리 단계로 구현
- skopc/modeling/euv_flare.py: 멀티-가우시안 PSF + 밀도 맵 컨볼루션
- 플레어 PSF 파라미터: ASML 툴별 측정값 또는 공개 데이터 활용
- 전체 칩 플레어 계산: FFT 기반 컨볼루션 O(N log N)
- 장거리 성분(σ ~ mm): 칩 경계 효과(black border effect) 고려 필요

## 참고문헌
- Neureuther, A.R. et al., "EUV OPC modeling requirements" (2014)
- Mack, C.A. et al., "Comprehensive EUV lithography model" (2011)
- ASML EUV flare measurement papers

## 태그
`Model`, `SPIE`, `EUV`, `Flare`, `ScatteringModel`, `PSF`, `OPC`, `Correction`, `MultiGaussian`, `2011`
