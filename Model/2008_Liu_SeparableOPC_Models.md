# Separable OPC Models for Computational Lithography

## 메타데이터
- **저자**: Liu, Y. et al. (IBM Research / Synopsys)
- **연도**: 2008
- **게재지**: Proc. SPIE 7028, Photomask and Next-Generation Lithography Mask Technology XV
- **DOI/URL**: https://doi.org/10.1117/12.793039
- **인용수**: ~45

## 핵심 요약
OPC 모델을 광학 성분과 레지스트 성분으로 분리(separable decomposition)할 수 있는 조건과 방법을 분석한다. 광학 모델(TCC/SOCS)과 레지스트 모델(CM1/VTRE)의 분리 가능성을 이론적으로 규명하고, 분리 가능한 OPC 모델이 얻는 계산 효율성과 모델 재사용성(portability) 이점을 실증한다. 광원(source) 변경 후 레지스트 모델 재사용 가능 여부를 분리 가능성 관점에서 평가한다.

## 주요 기여
1. OPC 모델의 광학-레지스트 분리 가능성 이론적 분석
2. 분리 가능 OPC 모델의 계산 효율 및 재사용성 이점 정량화
3. 광원 변경(SMO 후) 시 레지스트 모델 재사용 가능성 평가 프레임워크
4. 분리 가능 모델의 한계: 어떤 조건에서 분리 불가능한지 명확화
5. 전체 칩 스케일 계산 리소그래피에서의 실용적 분리 전략

## 모델 수식/아키텍처

**일반 OPC 모델:**
```
CD = f_OPC(mask, θ_optical, θ_resist)
```

**분리 가능 OPC 모델 조건:**
```
f_OPC(mask, θ) = g_resist(h_optical(mask, θ_optical), θ_resist)
```
h_optical: 순수 광학 계산 (공중상 생성)
g_resist: 순수 레지스트 반응 (공중상 → CD)

**SOCS 기반 분리 가능 형태:**
```
I(x) = Σ_k λ_k |φ_k * mask|²   [광학 단계]
CD = CM1(I, ∂I/∂x, ...)         [레지스트 단계]
```
→ 두 단계가 독립 파라미터 집합 사용 → 분리 가능

**분리 불가능 조건:**
```
레지스트 파라미터가 광학 조건에 의존할 때:
θ_resist = θ_resist(NA, σ, wavelength)
→ 광원 변경 시 레지스트 모델 재캘리브레이션 필요
```

**광원 변경 후 분리 가능성 테스트:**
```
SMO 전: I_before(x) = Σ_k λ_k^before |φ_k^before * mask|²
SMO 후: I_after(x) = Σ_k λ_k^after |φ_k^after * mask|²
레지스트 모델 재사용: CD_after ≈ CM1(I_after, θ_resist^before)?
→ 이미지 특성 분포가 유사하면 재사용 가능
```

## 모델 유형
- [x] 광학 모델
- [x] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc 분리 가능 OPC 모델 구현: 광학 커널 + 레지스트 모델 독립 모듈화
- SMO(광원 최적화) 후 레지스트 모델 재사용 가능성 평가 루틴 추가
- 계산 효율: 광학 커널 1회 계산 후 다양한 레지스트 파라미터 테스트 가능
- 모델 재사용성: 동일 레지스트 공정 + 다른 조명 조건 → 레지스트 재캘리브레이션 최소화
- OPC 모델 아키텍처 설계의 핵심 원칙

## 참고문헌
- Zuniga, C. et al., "CM1 standard process model" (2007)
- Rosenbluth, A.E. et al., "Fast TCC for High NA" (2005)
- Cobb, N. et al., "VTRE universal process modeling" (2002)

## 태그
`Model`, `SPIE`, `SeparableModel`, `OPCModel`, `OpticalModel`, `ResistModel`, `SMO`, `Portability`, `2008`
