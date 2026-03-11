# Computational Lithography Solutions to Support EUV High-NA Patterning

## 메타데이터
- **저자**: Rongkuo Zhao, Fan Zhou, Jialei Tang, Jeff Lu, Yunbo Liu, Dezheng Sun, Ming-Chun Tien, Stephen Hsu, Rachit Gupta, Youping Zhang, Joerg Zimmermann
- **연도**: 2023
- **게재지/학회**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950R (28 April 2023)
- **DOI/URL**: https://doi.org/10.1117/12.2660858
- **인용수**: 확인 필요

## 핵심 요약
고-NA EUV 리소그래피 전체 칩 패터닝을 위한 SMO 및 마스크 단독 최적화의 이점을 조사한다. 마스크 3D 효과(M3D)를 광학 모델링에 통합하여 1D 라인/스페이스(L/S) 패턴과 2D 컨택/홀(C/H) 패턴의 공정 마진(PW), 심도(DOF), 정규화 이미지 로그 기울기(NILS) 성능을 평가한다. 고-NA EUV에서의 중심 가림(center obscuration) 영향을 분석하고 SMO와 마스크 최적화의 상대적 이점을 정량화한다.

## 주요 기여
- 고-NA EUV용 SMO vs. 마스크 단독 최적화 성능 비교 분석
- M3D(마스크 3D 효과) 통합 광학 모델을 이용한 고-NA EUV 시뮬레이션
- 중심 가림(center obscuration)이 패터닝 성능에 미치는 영향 정량화
- 1D L/S 및 2D C/H 패턴에 대한 통해 SMO 효과 체계적 검증

## 알고리즘/수식
**고-NA EUV 광학 모델 (M3D 포함):**
$$I(x) = \sum_k \sigma_k |h_k^{M3D}(x) * m_{3D}(x)|^2$$
EUV 반사 마스크의 M3D 효과:
- 그림자 효과(shadowing): 흡수층 두께에 의한 비대칭 회절
- 비텔레센트리시티: chief ray angle ~6° off-axis
- 위상 효과: MoSi 다층막의 복소 반사율

**중심 가림 모델 (Center Obscuration):**
$$H_{high-NA}(f,g) = H_{pupil}(f,g) \cdot [1 - \text{circ}(f/f_{obs}, g/g_{obs})]$$
여기서 $\text{circ}$는 중심 가림 영역.

**NILS (정규화 이미지 로그 기울기):**
$$NILS = CD \cdot \frac{d\ln I}{dx}\bigg|_{CD/2}$$

**SMO 최적화:**
$$\max_{\sigma \in \mathcal{S}} \min_{pattern_i} \{EL_i(\sigma, m^*_i) \times DOF_i(\sigma, m^*_i)\}$$
여기서 $m^*_i$는 각 소스 $\sigma$에 대해 최적화된 마스크.

## OPC 툴 SMO 구현 관련성
- SKOPC 고-NA EUV SMO 구현 시 M3D 효과 모델링 방법 참고
- 중심 가림 효과를 고-NA EUV 시뮬레이션에 반영하는 방법 제시
- NILS를 SMO 성능 지표로 추가하는 구현 참고 (`skopc/smo/metrics.py`)
- 1D/2D 패턴 혼합 클립 라이브러리에서의 SMO 전략 설계 참고

## 참고문헌 (핵심)
- Liu et al., "EUV SMO for 7nm node and beyond," Proc. SPIE 9048, 2014
- Ma et al., "Gradient-based SMO for EUV," IEEE TCI 2019
- Hwang et al., "SMO study for high-NA EUV," Proc. SPIE 12954, 2024

## 태그
`SMO`, `SPIE`, `high-NA-EUV`, `M3D`, `mask-3D-effect`, `center-obscuration`, `NILS`, `computational-lithography`, `full-chip`, `L/S-pattern`, `contact-hole`, `process-window`
