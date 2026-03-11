# Source Optimization for Anamorphic Magnification High-Numerical Aperture Extreme Ultraviolet Lithography Based on Thick Mask Model

## 메타데이터
- **저자**: (IEEE Xplore document 9972327, 상세 저자 정보 직접 확인 필요)
- **연도**: 2022
- **게재지/학회**: IEEE Conference Publication (IEEE Xplore document 9972327)
- **DOI/URL**: https://ieeexplore.ieee.org/document/9972327/
- **인용수**: 확인 필요

## 핵심 요약
고-NA EUV 리소그래피(NA=0.55, 비대칭 배율 4×8)에서 두꺼운 마스크 모델(thick mask model, M3D)에 기반한 소스 최적화 방법을 제안한다. NA 증가에 따라 급격히 커지는 마스크 3D 효과를 정확히 모델링하고, 이를 소스 최적화 목적함수에 통합한다. 비대칭 배율에 의한 수평/수직 방향 패터닝 성능 차이를 소스 최적화로 보상하는 전략을 제시한다.

## 주요 기여
- 비대칭 배율(4×8) 고-NA EUV용 두꺼운 마스크 모델 기반 소스 최적화 프레임워크
- M3D 효과(그림자, 비텔레센트리시티)를 소스 최적화 목적함수에 직접 통합
- 수평/수직 비대칭 패터닝 성능을 소스 비대칭 조명으로 보상하는 전략
- 고-NA EUV에서의 M3D 영향이 소스 선택에 미치는 정량적 분석

## 알고리즘/수식
**비대칭 배율 고-NA EUV 이미징 모델:**
$$I(x,y) = \sum_k \sigma_k |h_k^{4\times8}(x,y) * m_{3D}(x,y)|^2$$
비대칭 배율에서 수평/수직 방향 공간 주파수 범위 상이:
$$f_{max,H} = \frac{NA}{\lambda \cdot 4}, \quad f_{max,V} = \frac{NA}{\lambda \cdot 8}$$

**두꺼운 마스크 M3D 모델 (RCWA 또는 근사):**
반사 마스크 전기장:
$$E_{mask}(x,y) = r_{0}(x,y) \cdot e^{i\phi_{3D}(x,y)}$$
여기서 $\phi_{3D}$는 마스크 흡수층 3D 구조에 의한 위상 오차.

**소스 최적화 목적함수 (M3D 포함):**
$$\min_{\sigma \geq 0} \sum_j EPE_j^2(\sigma; m_{3D}) + \lambda_{H-V} \cdot |CD_H(\sigma) - CD_V(\sigma)|^2$$
여기서 마지막 항은 수평/수직 CD 차이 페널티.

**그래디언트 계산:**
$$\frac{\partial F}{\partial \sigma_k} = \sum_{x,y} \frac{\partial F}{\partial I(x,y)} \cdot |h_k^{4\times8}(x,y) * m_{3D}(x,y)|^2$$

## OPC 툴 SMO 구현 관련성
- SKOPC 고-NA EUV SMO에서 비대칭 배율 광학계 모델링의 직접 참고
- `skopc/litho/euv_optics.py`에 4×8 비대칭 배율 커널 구현 시 참고
- 두꺼운 마스크 모델과 소스 최적화 결합 방법론 제공
- 수평/수직 CD 균일도를 소스로 최적화하는 페널티 함수 설계 참고

## 참고문헌 (핵심)
- Liu et al., "EUV SMO for 7nm node," Proc. SPIE 9048, 2014
- Ma et al., "Gradient-based SMO for EUV," IEEE TCI 2019
- Zhao et al., "Computational lithography for EUV high-NA," Proc. SPIE 12495, 2023

## 태그
`SMO`, `IEEE`, `high-NA-EUV`, `anamorphic-magnification`, `thick-mask-model`, `M3D`, `source-optimization`, `4x8-magnification`, `H-V-bias`, `0.55NA`
