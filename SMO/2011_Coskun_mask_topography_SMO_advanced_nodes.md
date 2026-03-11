# Accounting for Mask Topography Effects in Source-Mask Optimization for Advanced Nodes

## 메타데이터
- **저자**: Tamer H. Coskun, Huixiong Dai, Hsu-Ting Huang, Vishnu Kamat, Chris Ngai
- **연도**: 2011
- **게재지/학회**: Proc. SPIE 7973, Optical Microlithography XXIV, 79730P
- **DOI/URL**: https://doi.org/10.1117/12.879704
- **인용수**: 확인 필요

## 핵심 요약
고속 3D 마스크 모델을 소스-마스크 최적화에 적용하여 첨단 노드에서의 마스크 토포그래피 효과를 SMO에 통합하는 방법을 연구한다. 마스크 토포그래피 효과 포함/미포함 소스 최적화 및 SMO 결과를 비교하여 첨단 노드에서 3D 마스크 모델의 SMO 적용 가능성을 종합적으로 분석한다. Cadence Design Systems 및 Applied Materials.

## 주요 기여
- 고속 3D 마스크 모델의 SMO 통합 방법론 연구
- 마스크 토포그래피 효과 포함/미포함 SMO 결과 비교
- 첨단 노드에서 3D 마스크 모델 SMO 적용 가능성 분석
- 마스크 3D 효과를 고려한 소스-마스크 공동 최적화 결과 제시

## 알고리즘/수식
**3D 마스크 모델 포함 이미징:**
$$I(x; \boldsymbol{\sigma}, m) = \sum_k \sigma_k \left|\int M_{3D}(\mathbf{f}; m) H_k(\mathbf{f}) e^{i2\pi \mathbf{f} \cdot x} d\mathbf{f}\right|^2$$
3D 마스크 회절 스펙트럼 $M_{3D}$를 사용하는 이미징 모델.

**고속 3D 마스크 모델 (근사):**
$$M_{3D}(\mathbf{f}) \approx M_{2D}(\mathbf{f}) \cdot T_{3D}(\mathbf{f})$$
2D 마스크 투과율 $M_{2D}$에 3D 보정 필터 $T_{3D}$ 적용.

**마스크 토포그래피 보정항:**
$$T_{3D}(\mathbf{f}) = \exp\left(i\Delta\phi_{3D}(\mathbf{f}) + \Delta A_{3D}(\mathbf{f})\right)$$
주파수 의존 위상 $\Delta\phi_{3D}$와 진폭 보정 $\Delta A_{3D}$.

**3D 포함 SMO 비용함수:**
$$F_{3D-SMO}(\boldsymbol{\sigma}, m) = \sum_j EPE_j^2(\boldsymbol{\sigma}, m; M_{3D})$$
3D 마스크 모델 기반 EPE 비용함수.

**3D vs 2D 소스 최적화 차이:**
$$\Delta\boldsymbol{\sigma} = \boldsymbol{\sigma}^*_{3D} - \boldsymbol{\sigma}^*_{2D}$$
3D/2D 모델 소스 최적화 결과의 차이 분석.

## OPC 툴 SMO 구현 관련성
- SKOPC M3D 포함 SMO 구현 시 고속 3D 마스크 모델 통합 방법 참고
- `skopc/litho/fast_m3d_model.py`에 고속 3D 마스크 보정 필터 구현
- Liu et al. 2015 M3D-aware OPC/SMO와 함께 마스크 토포그래피 SMO 계열 참고
- Zhang et al. 2021 EUV thick mask SL-PSO와 함께 두꺼운 마스크 효과 SMO 계열 참고

## 참고문헌 (핵심)
- Liu et al., \"M3D-aware OPC SMO 22nm,\" SPIE 2015
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011
- Zhang et al., \"EUV SMO thick mask SL-PSO,\" Optics Express 2021

## 태그
`SMO`, `SPIE`, `mask-topography`, `M3D`, `3D-mask-model`, `fast-3D-model`, `advanced-nodes`, `Cadence`, `Applied-Materials`, `source-optimization`, `mask-topography-effects`
