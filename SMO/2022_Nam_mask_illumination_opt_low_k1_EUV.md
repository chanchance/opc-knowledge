# Mask and Illumination Optimization for Low-k1 EUV Lithography

## 메타데이터
- **저자**: Dong-Seok Nam, Jung-Hoon Ser, Nakgeuon Seong, Xiaoyang Li, Stephen Hsu, Anthony Yen (ASML)
- **연도**: 2022
- **게재지/학회**: Proc. SPIE 12325, Photomask Japan 2022: XXVIII Symposium on Photomask and Next-Generation Lithography Mask Technology, 1232502 (15 September 2022)
- **DOI/URL**: https://doi.org/10.1117/12.2651194
- **인용수**: 확인 필요

## 핵심 요약
0.55NA 고-NA EUV에서 허니콤 홀 어레이(honeycomb hole array)의 DOF와 NILS를 최대화하기 위한 소스-마스크 최적화 및 EUV 마스크 구조 최적화 방법을 제안한다. NILS 성능(peak-NILS, NILS-DOF, NILS-MEEF)의 좋고 안정적인 마스크 구조 조건 최적화 플로우를 제시하며, EUV 이진 흡수체와 PSM 흡수체 재료를 24-28nm 허니콤 홀 어레이에서 비교 평가한다.

## 주요 기여
- 0.55NA EUV용 마스크 구조 + 조명 동시 최적화 플로우 제안
- NILS 지표(peak-NILS, NILS-DOF, NILS-MEEF) 기반 마스크 흡수체 두께 및 CD 최적화
- EUV 이진 흡수체(high-n/mid-k, low-n/high-k) vs. EUV PSM 흡수체(low-n/low-k, 고반사율) 성능 비교
- 24/26/28nm 허니콤 홀 어레이에서 최적 마스크 재료 및 SMO 조건 결정

## 알고리즘/수식
**NILS (정규화 이미지 로그 기울기):**
$$NILS = CD \cdot \frac{\partial \ln I}{\partial x}\bigg|_{edge}$$

**DOF-NILS 최적화 목적함수:**
$$\max_{\sigma, m_{struct}} \min_f NILS(\sigma, m_{struct}; f)$$
여기서 $m_{struct}$는 마스크 구조 파라미터(흡수체 두께 $t$, 마스크 CD $w$, 재료 광학 상수 $n+ik$).

**NILS-MEEF 트레이드오프:**
$$MEEF = \frac{\partial CD_{wafer}}{\partial CD_{mask}} \cdot M$$
흡수체 두께/CD와 NILS-MEEF 간 트레이드오프 정량화.

**EUV 마스크 구조 모델 (M3D):**
$$r(x) = r_0(n, k, t, w) \cdot e^{i\phi_{3D}(x)}$$
흡수체 재료 $(n,k)$, 두께 $t$, CD $w$에 따른 반사율/위상 변화.

**조명-마스크 공동 최적화:**
$$[\sigma^*, t^*, w^*, mat^*] = \arg\max F_{NILS-DOF}(\sigma, t, w, mat)$$

## OPC 툴 SMO 구현 관련성
- SKOPC EUV SMO에서 마스크 구조 파라미터를 추가 최적화 변수로 도입 방법 참고
- `skopc/smo/euv_mask_structure_opt.py` 구현 시 흡수체 두께/재료 최적화 참고
- NILS를 SMO 성능 지표로 활용하는 구현 방법 제시 (`skopc/smo/metrics.py`)
- 고-NA EUV 허니콤 홀 패턴의 SMO 벤치마크 제공

## 참고문헌 (핵심)
- Liu et al., "EUV SMO for 7nm node," Proc. SPIE 9048, 2014
- Hwang et al., "SMO for high-NA EUV," Proc. SPIE 12954, 2024
- Zhao et al., "Computational lithography for EUV high-NA," Proc. SPIE 12495, 2023

## 태그
`SMO`, `SPIE`, `EUV`, `low-k1`, `0.55NA`, `high-NA`, `mask-structure-optimization`, `NILS`, `MEEF`, `absorber-material`, `honeycomb-hole`, `PSM`, `DOF`
