# OPC Model Building for EUV Lithography

## 메타데이터
- **저자**: Ho, B. C. P., Doebler, J., Niroomand, A. (Synopsys)
- **연도**: 2019
- **게재지**: Proc. SPIE 11147, International Conference on Extreme Ultraviolet Lithography 2019
- **DOI/URL**: https://doi.org/10.1117/12.2531430
- **인용수**: ~40

## 핵심 요약
EUV 리소그래피를 위한 OPC 모델 구축 플로우를 DUV 모델 구축 플로우와 비교하며, EUV 특유의 새로운 현상들(비텔레센트릭 조명 유발 그림자 효과, 슬릿 방향 변동, 광학 플레어, 레티클 블랙 보더 효과)에 대한 OPC 모델 처리 방법을 체계적으로 설명한다. EUV 양산(HVM)을 위한 OPC 모델 구축의 새로운 도전 과제를 식별하고 해결책을 제시한다.

## 주요 기여
1. EUV OPC 모델 구축 플로우 vs. DUV 플로우 체계적 비교
2. EUV 특유 4대 효과(그림자, 슬릿 변동, 플레어, 블랙 보더) OPC 모델 통합 방법론
3. EUV HVM을 위한 모델 구축 요구사항 및 캘리브레이션 데이터 선택 가이드
4. 슬릿 위치 의존 OPC 모델(across-slit model) 구현 전략
5. EUV 마스크 3D 효과와 레지스트 3D 효과 통합 모델 캘리브레이션 절차

## 모델 수식/아키텍처

**EUV OPC 모델 구성 요소:**
```
CD_EUV(x,y) = f(I_optical(x,y)
               + I_flare(x,y)       [플레어 보정]
               + I_shadow(x,y)      [그림자 보정]
               + I_slit_var(x,y))   [슬릿 변동 보정]
```

**슬릿 위치 의존 모델:**
```
TCC_slit(f; y_slit) = TCC_center(f) + ΔTCC_shadow(f; y_slit) + ΔTCC_abberation(f; y_slit)
```
y_slit = 슬릿 위치 (−slit_width/2 ~ +slit_width/2)

**레티클 블랙 보더 효과:**
```
I_border(x,y) = F_border · PSF_flare(x - x_border, y - y_border)
```
x_border, y_border = 레티클 노광 영역 경계까지의 거리

**EUV vs. DUV OPC 모델 차이:**
```
DUV 모델: TCC(NA, σ, aberration) + Resist(CM1/VTRE) + Etch
EUV 모델: TCC + Flare + Shadow(y_slit) + M3D_EUV + Resist_3D + Etch + BlackBorder
```

**EUV 캘리브레이션 데이터 요구사항:**
```
- 1D 라인/스페이스: 다양한 pitch (20-100nm), H/V 방향
- 2D 구조: 코너, T-bar, L-shape
- 슬릿 위치별: center / ±1/4 slit / ±edge
- Focus-Exposure 매트릭스 (FEM)
→ 총 게이지 수: ~2000-5000개 (DUV 대비 2× 이상)
```

## 모델 유형
- [x] 광학 모델 (EUV 전체 광학 모델)
- [x] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc EUV OPC 모델 구축 플로우의 핵심 참조 논문
- EUV OPC 모델 = DUV 모델 + 플레어 + 그림자 + 슬릿 변동 + 블랙 보더
- 슬릿 위치별 TCC 사전 계산 → across-slit 보정 맵 생성
- 캘리브레이션 게이지: 슬릿 위치 다양성 포함 필수
- Synopsys Proteus EUV OPC 구현의 핵심 논문

## 참고문헌
- Flagello, D.G. et al., "EUV flare and proximity modeling" (2011)
- Mack, C.A. et al., "EUV shadowing modeling" (2011)
- Neureuther, A.R. et al., "EUV OPC modeling requirements" (2014)

## 태그
`Model`, `SPIE`, `EUV`, `OPCModelBuilding`, `Shadowing`, `Flare`, `AcrossSlit`, `BlackBorder`, `HVM`, `2019`
