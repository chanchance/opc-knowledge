# Lithographic Source and Mask Optimization with Narrow-Band Level-Set Method

## 메타데이터
- **저자**: Yijiang Shen
- **연도**: 2018
- **게재지/학회**: Optics Express, Vol. 26, No. 8, pp. 10065–10078
- **DOI/URL**: https://doi.org/10.1364/OE.26.010065
- **인용수**: 다수

## 핵심 요약
22nm 이하 기술 노드를 위한 SMO에서 거리 레벨 셋 정규화(distance level-set regularization)를 적용한 협대역(narrow-band) SMO 방법을 제안한다. 원하는 부호 거리(signed distance) 특성을 유지하여 안정적인 곡선 진화를 보장하고, 협대역 구현으로 컨볼루션 연산 및 메모리 요구사항을 줄이면서 수렴 속도를 향상시킨다.

## 주요 기여
- 레벨 셋 SMO에 거리 정규화 도입으로 안정적 곡선 진화 보장
- 협대역(narrow-band) 구현으로 컨볼루션 계산량 및 메모리 요구 대폭 절감
- 레벨 셋 마스크와 픽셀화 소스의 동시 최적화 통합
- 22nm 이하 노드에서 기존 레벨 셋 SMO 대비 수렴 속도 향상

## 알고리즘/수식
**레벨 셋 마스크 표현:**
$$m(x) = H(\phi(x)), \quad \phi(x) = 0 \text{ (마스크 윤곽선)}$$

**부호 거리 정규화 (distance level-set):**
레벨 셋 함수가 부호 거리 함수(SDF) 특성을 유지하도록 정규화:
$$\frac{\partial \phi}{\partial t} = \text{sign}(\phi^{(0)})(1 - |\nabla \phi|) \quad \text{(재초기화)}$$

**좁은 대역 (Narrow-Band) 구현:**
레벨 셋 함수 업데이트를 $|\phi| < \epsilon_{band}$인 좁은 대역 내에서만 수행:
$$\Omega_{NB} = \{x : |\phi(x)| < \epsilon_{band}\}$$
전체 도메인 대신 좁은 대역에서만 컨볼루션 계산 → 계산 비용 대폭 절감.

**레벨 셋 속도 함수:**
$$\frac{\partial \phi}{\partial t} = -F_{mask}(x) |\nabla \phi|$$
$$F_{mask}(x) = -\frac{\delta F_{SMO}}{\delta m} \bigg|_{m=H(\phi)} \cdot \delta(\phi)$$

**소스 그래디언트 (픽셀 기반):**
$$\frac{\partial F_{SMO}}{\partial \sigma_k} = \sum_{x \in \Omega_{NB}} \frac{\partial F}{\partial I} \cdot |h_k * m|^2$$

## OPC 툴 SMO 구현 관련성
- SKOPC ILT+SMO 통합 구현 시 레벨 셋 기반 마스크 최적화의 효율적 구현 참고
- 협대역 구현으로 `skopc/modeling/opc/ilt.py`의 레벨 셋 ILT 가속화 방법 제공
- 거리 정규화를 통한 안정적 마스크 윤곽 최적화 방법 제시
- 소스+레벨 셋 마스크 동시 최적화 플로우 설계 참고

## 참고문헌 (핵심)
- Tolani et al., "SMO using level set methods," Proc. SPIE 7488, 2009
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Osher & Sethian, "Level set methods," JCP 1988

## 태그
`SMO`, `level-set`, `narrow-band`, `signed-distance-function`, `mask-synthesis`, `variational`, `computational-efficiency`, `22nm`, `Optics-Express`, `curve-evolution`
