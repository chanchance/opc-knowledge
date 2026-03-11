# High Accuracy OPC Modeling for New EUV Low-K1 Mask Technology Options

## 메타데이터
- **저자**: Sakr, E., DeLancey, R., Hoppe, W., Levinson, Z., Iwanow, R., Chen, R., Yang, D., Lucas, K. (Synopsys)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II
- **DOI/URL**: https://doi.org/10.1117/12.2658720
- **인용수**: ~14

## 핵심 요약
EUV 저-k1 리소그래피를 위한 새로운 마스크 기술 옵션(위상 이동 마스크, low-n 마스크, 고-k 마스크)의 고정밀 OPC 모델링 방법론을 연구한다. 각 마스크 기술 옵션별로 마스크 3D EM 효과의 크기와 OPC 모델 정확도에 미치는 영향을 분석하고, 새로운 마스크 스택에 맞는 OPC 모델 캘리브레이션 전략을 제시한다.

## 주요 기여
1. EUV PSM(위상 이동), low-n, 고-k 마스크 각각의 OPC 모델링 요구사항 비교 분석
2. 마스크 스택 변화에 따른 M3D EM 효과 크기 정량화
3. 새로운 마스크 기술별 SOCS 커널 업데이트 전략
4. 위상 이동 마스크의 복소(complex) TCC 처리 방법
5. 저-k1 EUV OPC 모델의 정확도 달성 경로 제시

## 모델 수식/아키텍처

**EUV 마스크 기술 옵션:**
```
Option 1: Standard TaN absorber (기준)
  - TaN 두께: ~56-84nm
  - 반사율: ~2% (dark field 기준)

Option 2: Low-n (low refractive index) mask
  - 더 얇은 흡수체로 M3D 효과 감소
  - 광학 대비(NILS) 향상

Option 3: Attenuated PSM (위상 이동)
  - t_PSM(f) = √T_att · exp(iπ)  [반전 위상]
  - 부분 투과 → NILS 향상, MEEF 감소

Option 4: High-k absorber
  - 흡수율 높은 재료 → 더 얇은 흡수체
  - M3D 효과 감소
```

**복소 TCC (위상 이동 마스크):**
```
TCC_PSM(f,g; f',g') = ∫∫ J(f₀,g₀)
  · H_EUV(f+f₀,g+g₀) · H*_EUV(f'+f₀,g'+g₀) df₀dg₀
```
마스크 투과 함수가 복소수 → TCC 및 SOCS 커널 업데이트 필요

**M3D 효과 크기 비교:**
```
ΔBF_TaN: ~5-10nm (두꺼운 흡수체)
ΔBF_low-n: ~2-4nm (얇은 흡수체)
ΔBF_PSM: ~1-3nm (위상 위주)
→ 마스크 기술에 따라 M3D 보정 크기 상이
```

**OPC 정확도 비교 (28nm HP 메탈):**
```
RMS_TaN: ~1.8nm
RMS_low-n: ~1.2nm  (33% 향상)
RMS_PSM: ~1.0nm   (44% 향상)
```

## 모델 유형
- [x] 광학 모델 (EUV 마스크 모델, M3D)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc EUV 마스크 모델 모듈: 마스크 기술 옵션별 파라미터 지원
- PSM 처리: 복소 마스크 투과 함수 → 복소 SOCS 커널
- Low-n 마스크: 기존 TaN M3D 룩업 테이블 교체 필요
- 마스크 기술 전환 시 전체 OPC 모델 재캘리브레이션 또는 델타 캘리브레이션
- 7nm 이하 EUV 노드에서 고-k/low-n/PSM 마스크 도입 가속

## 참고문헌
- Sakr, E. et al., "High accuracy OPC EM full-chip modeling for curvilinear" (2024)
- Neureuther, A.R. et al., "EUV OPC modeling requirements" (2014)
- Ho, B.C.P. et al., "OPC model building for EUV" (2019)

## 태그
`Model`, `SPIE`, `EUV`, `LowK1`, `PSM`, `LowN`, `HighK`, `Mask3D`, `OPCModel`, `Calibration`, `2023`
