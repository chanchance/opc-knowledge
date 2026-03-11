# Improving EUV Sub-40nm via Single Patterning Using Wavefront and Pupil Co-Optimization

## 메타데이터
- **저자**: Soojung Kim, No Young Chung, Kwangseok Maeng, Hyunjae Cho, Jerry Lim, Hyungrok Jang, Jae Hyoung Kim, Insung Kim, Eelco van Setten, Hidde Keizers, Ajinkya Patil, Steven Beekmans, Jungtae Lee, Ki-Seok Kim, James Lee, Sung-Woon Park, Jialei Tang, Stephen Hsu, Youping Zhang, Paul Derks
- **연도**: 2024
- **게재지/학회**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 1295306 (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3009878
- **인용수**: 확인 필요

## 핵심 요약
0.33NA EUV에서 sub-40nm 피치 컨택 단일 패터닝의 주요 과제인 확률론적 결함(stochastic defect)을 동공/마스크/파면 동시 최적화(Pupil/Mask/Wavefront co-optimization)로 해결한다. EUV 확률론적 결함이 이미지 대비와 강하게 상관함을 밝히고, Mask3D 유도 대비 감소(contrast fading)를 완화하는 최적화 전략을 제시한다. sub-40nm 피치 컨택 홀 어레이의 이미지 대비 향상을 실증한다.

## 주요 기여
- EUV 확률론적 결함과 이미지 대비의 강한 상관관계 정량화
- Mask3D 유도 대비 감소 완화를 위한 동공/마스크/파면 동시 최적화
- 0.33NA EUV sub-40nm 피치 컨택 홀 어레이 단일 패터닝 가능성 실증
- 파면 조작(wavefront manipulation)을 SMO에 통합하는 새로운 접근법

## 알고리즘/수식
**EUV 확률론적 결함 모델:**
$$P_{fail} \propto \exp\left(-\frac{NILS^2}{2\sigma_{stoch}^2}\right)$$
높은 NILS → 낮은 확률론적 결함률.

**Mask3D 대비 감소:**
EUV 반사 마스크 3D 효과로 인한 이미지 대비 손실:
$$NILS_{actual} = NILS_{ideal} \cdot (1 - \eta_{M3D})$$
여기서 $\eta_{M3D}$는 M3D 유도 대비 감소율.

**동공/마스크/파면 동시 최적화 (PMW co-opt):**
$$\max_{\sigma, m, W} NILS(\sigma, m, W) \cdot DOF(\sigma, m, W)$$
여기서 $W(f)$는 Zernike 파면 함수.

**이미지 대비 향상:**
$$NILS_{PMW} = \max_{\sigma, m, W} \left[\frac{I_{max} - I_{min}}{I_{max} + I_{min}}\right] \cdot \frac{CD}{2}$$

**최적화 플로우:**
1. SMO로 초기 소스/마스크 최적화
2. Mask3D 효과 분석 및 대비 감소 정량화
3. 파면 보정 $W(f)$ 최적화로 M3D 대비 감소 보상
4. PMW 동시 최적화로 최종 수렴

## OPC 툴 SMO 구현 관련성
- SKOPC EUV SMO를 파면 최적화로 확장할 때 직접 참고
- 확률론적 결함률을 SMO 목적함수에 통합하는 방법 제시
- `skopc/smo/wavefront_coopt.py` 구현 시 동공/마스크/파면 동시 최적화 참고
- sub-40nm 피치 EUV 컨택 홀 패턴의 SMO 벤치마크 제공

## 참고문헌 (핵심)
- Liu et al., "EUV SMO for 7nm node," Proc. SPIE 9048, 2014
- Li & Lam, "Joint optimization of source, mask, and pupil," Proc. SPIE 9052, 2014
- Nam et al., "Mask and illumination optimization for low-k1 EUV," Proc. SPIE 12325, 2022

## 태그
`SMO`, `SPIE`, `EUV`, `0.33NA`, `sub-40nm`, `stochastic-defect`, `wavefront-optimization`, `pupil-mask-wavefront`, `M3D`, `contrast-fading`, `contact-hole`, `single-patterning`
