# EUV Source-Mask Optimization for 7nm Node and Beyond

## 메타데이터
- **저자**: Xiaofeng Liu, Rafael Howell, Stephen Hsu, Kaiyu Yang, Keith Gronlund, Frank Driessen, Hua-Yu Liu, Steven Hansen, Koen van Ingen Schenau, Thijs Hollink, Paul van Adrichem, Kars Troost, Jörg Zimmermann, Oliver Schumann, Christoph Hennerkes, Paul Gräupner
- **연도**: 2014
- **게재지/학회**: Proc. SPIE 9048, Extreme Ultraviolet (EUV) Lithography V, 90480Q (17 April 2014)
- **DOI/URL**: https://doi.org/10.1117/12.2047584
- **인용수**: 다수

## 핵심 요약
7nm 노드 이하를 위한 EUV 특화 소스-마스크 동시 최적화(SMO) 기법을 제시한다. NXE:33×0 스캐너의 FlexPupil 가변 조명기를 완전히 활용하는 새로운 알고리즘을 개발하였으며, EUV 반사 마스크의 3D 효과(그림자 효과, 비텔레센트리시티)를 정확히 모델링하는 NXE M3D+ 모델을 통합한다. 7nm 로직 컷 마스크에서 CD 균일도 최대 20% 향상 및 패턴 이동(pattern shift) 감소를 실증한다.

## 주요 기여
- NXE:33×0 FlexPupil 조명기를 완전 활용하는 EUV 특화 SMO 알고리즘
- NXE M3D+ 모델: EUV 반사 3D 마스크 효과(그림자, 비텔레센트리시티, 플레어) 정확 예측
- H-V 바이어스, Bossung 기울기, 패턴 이동 완화 전략 내장
- 7nm 로직 컷 마스크: CD 균일도 20% 향상, 최대 패턴 이동 감소

## 알고리즘/수식
**EUV 반사 마스크 3D 효과 모델 (M3D+):**
$$I(x) = \sum_k \sigma_k^{NXE} |h_k^{M3D+}(x) * m_{3D}(x)|^2$$
여기서 $h_k^{M3D+}$는 EUV 반사 마스크 3D 회절을 포함한 시스템 커널.

**비텔레센트리시티 보정:**
EUV 조명은 oblique incidence ($\sim$6° off-axis)로 인한 그림자 효과:
$$\Delta CD_{shadow} \approx \frac{h_{mask} \cdot \sin\theta_{chief}}{\cos\theta_{chief}} \cdot \frac{d}{p}$$
여기서 $h_{mask}$는 마스크 흡수층 두께, $\theta_{chief}$는 chief ray angle.

**FlexPupil 소스 최적화:**
$$\min_{\sigma \in \mathcal{S}_{FlexPupil}} F_{EUV}(\sigma, m)$$
$$F_{EUV} = \sum_j EPE_j^2 + \lambda_{Bossung} \cdot \sum_j \left(\frac{\partial CD_j}{\partial f}\right)^2$$
여기서 Bossung 기울기 페널티 항이 추가됨.

**공정 마진 목적함수:**
$$\text{maximize} \quad \min_j \{EL_j, DOF_j, MEF_j^{-1}\}$$

## OPC 툴 SMO 구현 관련성
- SKOPC EUV SMO 구현 시 3D 마스크 효과 모델링의 직접 참고
- EUV 비텔레센트리시티 보정 수식을 `skopc/smo/euv_corrections.py`에 구현 가능
- Bossung 기울기 페널티를 SMO 목적함수에 추가하는 방법 제시
- NXE 스캐너 조명기 제약 조건 (FlexPupil) 모델링 참고

## 참고문헌 (핵심)
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008
- Ma et al., "Gradient-Based SMO for EUV," IEEE TCI 2019
- Liu et al., "EUV source-mask optimization," Proc. SPIE 2012

## 태그
`SMO`, `SPIE`, `EUV`, `7nm-node`, `FlexPupil`, `NXE-scanner`, `3D-mask-effect`, `shadow-effect`, `non-telecentricity`, `Bossung-tilt`, `M3D+`
