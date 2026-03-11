# Fast and Accurate 3D Mask Model for Full-Chip OPC and Verification

## 메타데이터
- **저자**: Tyminski, J. K. et al. (Mentor Graphics)
- **연도**: 2007
- **게재지**: Proc. SPIE 6520, Optical Microlithography XX
- **DOI/URL**: https://doi.org/10.1117/12.712171
- **인용수**: ~90

## 핵심 요약
전체 칩(full-chip) OPC 및 검증에 실용적으로 사용 가능한 빠르고 정확한 3D 마스크 모델 프레임워크를 제시한다. Hopkins 얇은 마스크(Kirchhoff) 근사 외에 비경사 입사 효과(non-Hopkins oblique incidence)와 전자기(EM) 산란 효과를 별도 섭동 항으로 추가하는 방식으로 계산 효율성을 유지하면서 3D 마스크 정확도를 달성한다. 전체 칩 스케일의 적용 가능성을 193nm immersion 리소그래피 예제로 실증한다.

## 주요 기여
1. 전체 칩 OPC/검증에 사용 가능한 컴팩트 M3D 모델 최초 제안
2. Hopkins 모델에 비경사 입사 + EM 산란을 별도 섭동 항으로 추가하는 분리(splitting) 접근법
3. 리고러스 RCWA/FDTD M3D 대비 수천 배 빠른 계산 속도 유지
4. 193nm immersion 리소그래피 full-chip 적용 성능 검증
5. Calibre 3D Mask OPC 구현의 이론적 기반 제공

## 모델 수식/아키텍처

**컴팩트 M3D TCC 분해:**
```
TCC_M3D(f,g; f',g') = TCC_Kirchhoff(f,g; f',g')
                     + ΔTCC_oblique(f,g; f',g')    [비경사 입사 항]
                     + ΔTCC_EMF(f,g; f',g')         [EM 산란 항]
```

**비경사 입사 보정 (Non-Hopkins):**
```
ΔTCC_oblique = ∫∫ J(f₀,g₀)·[H(f+f₀)·H*(f'+f₀) - H_Hopkins(f+f₀)·H*_Hopkins(f'+f₀)] df₀dg₀
```
벡터 회절 방정식에서 경사 입사 각도 의존 항 추출

**EM 산란 컴팩트 모델:**
```
E_scatter(f) = E_Kirchhoff(f) · [1 + Σ_k α_k(pitch,azimuth) · Φ_k(f)]
```
α_k = RCWA 계산으로 미리 구한 산란 계수 룩업 테이블
Φ_k = 피치/방향 의존 기저 함수

**픽셀별 M3D 보정 (OPC 엔진 통합):**
```
I_M3D(x) = I_Kirchhoff(x) + ΔI_M3D(x, pitch_local, azimuth_local)
```
로컬 피치/방향 추출 → 룩업 테이블 보간 → 강도 보정

**계산 속도 비교:**
```
t_RCWA: O(N_harmonics³)   (full-chip 불가)
t_compact_M3D: O(N_mask_pixels)  (full-chip 가능)
```

## 모델 유형
- [x] 광학 모델 (M3D EMF)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc의 M3D 컴팩트 모델 핵심 참조 논문
- 구현 전략: RCWA로 피치/방향별 EM 산란 계수 미리 계산 → OPC 시 보간
- 193nm ArF immersion (NA 1.35): M3D 필수, 특히 HP 40nm 이하
- EUV (NA 0.33/0.55): 흡수체 두께 효과로 M3D 더욱 중요
- 룩업 테이블 크기: pitch × azimuth × polarization × wavelength

## 참고문헌
- Hopkins, H.H., "On the Diffraction Theory of Optical Images" (1953)
- Erdmann, A. et al., "Mask 3D effects on resist model calibration" (2009)
- Rosenbluth, A.E. et al., "Fast TCC algorithm for High NA" (2005)

## 태그
`Model`, `SPIE`, `Mask3D`, `EMF`, `CompactModel`, `FullChip`, `OPC`, `Kirchhoff`, `193nm`, `Immersion`, `2007`
