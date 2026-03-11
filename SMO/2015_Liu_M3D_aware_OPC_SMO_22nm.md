# Enlarge the Process Window of Patterns in 22nm Node by Using Mask Topography Aware OPC and SMO

## 메타데이터
- **저자**: Yansong Liu, Xiaojing Su, Lisong Dong (외)
- **연도**: 2015
- **게재지/학회**: IEEE Conference Publication (IEEE Xplore document 7153352, March 2015)
- **DOI/URL**: https://ieeexplore.ieee.org/document/7153352/
- **인용수**: 확인 필요

## 핵심 요약
22nm 노드 SRAM 셀 패턴에서 얇은 OMOG(Opaque MoSi on Glass) 마스크의 3D 효과(M3D)를 분석하고, M3D 인식 OPC와 SMO를 결합하여 공정 마진을 확장하는 방법을 제시한다. AttPSM과 OMOG 마스크를 비교하며, M3D 효과를 고려하지 않는 OPC는 공정 마진을 크게 감소시키고, M3D 인식 SMO가 공정 마진을 한 단계 더 향상시킴을 보인다.

## 주요 기여
- OMOG 얇은 마스크의 M3D 효과를 22nm SRAM 패턴에서 정량 분석
- M3D 인식 OPC와 M3D 인식 SMO 결합으로 공정 마진 극대화
- AttPSM vs. OMOG 마스크의 M3D 효과 비교
- M3D 효과 무시 시 공정 마진 손실 정량화

## 알고리즘/수식
**M3D 인식 이미징 모델:**
$$I(x) = \sum_k \sigma_k |h_k^{M3D}(x) * m_{3D}(x)|^2$$
여기서 $m_{3D}(x)$는 OMOG 마스크 흡수층 3D 구조를 RCWA 또는 Domain Decomposition으로 계산한 근전계.

**OMOG 마스크 M3D 효과:**
- 흡수층 두께 ~$40nm$ (MoSi)
- 위상 오차: $\Delta\phi = \frac{2\pi}{\lambda} \cdot \Delta n_{eff} \cdot t_{abs}$
- 진폭 오차: 흡수층 측면 회절에 의한 비대칭 근전계

**M3D 인식 SMO 목적함수:**
$$\min_{\sigma, m} \sum_j EPE_j^2(\sigma, m_{3D}) + \lambda_{PW} \frac{1}{PW(\sigma, m_{3D})}$$
M3D 효과가 포함된 $m_{3D}$로 EPE 및 공정 마진 계산.

**AttPSM vs. OMOG 비교:**
$$PW_{SMO,OMOG} > PW_{OPC,OMOG} \gg PW_{OPC,no-M3D}$$

## OPC 툴 SMO 구현 관련성
- SKOPC의 M3D 인식 SMO 구현 시 OMOG 마스크 M3D 모델 참고
- `skopc/litho/mask3d.py`에서 OMOG 마스크 3D 효과 계산 방법 참고
- AttPSM과 OMOG 마스크 타입별 SMO 설정 방법 비교
- 22nm 노드 SRAM 패턴에서의 SMO 성능 벤치마크 제공

## 참고문헌 (핵심)
- Rosenbluth et al., "Intensive optimization for 22nm," Proc. SPIE 7274, 2009
- Ma et al., "Gradient-based SMO for EUV," IEEE TCI 2019
- Liu et al., "EUV SMO for 7nm node," Proc. SPIE 9048, 2014

## 태그
`SMO`, `IEEE`, `M3D`, `mask-topography`, `OMOG`, `AttPSM`, `22nm-node`, `SRAM`, `process-window`, `OPC`, `thick-mask-effect`
