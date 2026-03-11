# Linearized EUV Mask Optimization Based on the Adjoint Method

## 메타데이터
- **저자**: Pinxuan He, Jiamin Liu, Honggang Gu, Hao Jiang, Shiyuan Liu
- **연도**: 2024
- **게재지/학회**: Optics Express, Vol. 32, pp. 8415–8424
- **DOI/URL**: https://doi.org/10.1364/OE.513416
- **인용수**: 확인 필요

## 핵심 요약
두꺼운 마스크 효과(thick mask effect)로 인한 웨이퍼 패턴 왜곡을 빠르게 보정하기 위해 Adjoint 방법 기반 선형화 EUV 마스크 최적화를 제안한다. Adjoint 방법으로 EUV 마스크 모델의 그래디언트를 계산하고, 선형화 그래디언트로 두꺼운 마스크 효과로 인한 왜곡을 빠르게 보정한다. 거친 최적화(coarse optimization) 단계에서 효율 약 40% 향상을 달성한다.

## 주요 기여
- Adjoint 방법 기반 EUV 마스크 모델 그래디언트 계산
- 선형화 그래디언트로 두꺼운 마스크 효과 왜곡 빠른 보정
- 거친 최적화 단계 효율 40% 향상
- 빠르고 효과적인 EUV 마스크 최적화 방법론

## 알고리즘/수식
**EUV 마스크 최적화 비용함수:**
$$F(m) = \sum_j (I_j(m) - I_{target,j})^2$$

**Adjoint 방법 그래디언트:**
$$\frac{\partial F}{\partial m_p} = 2\text{Re}\left[\boldsymbol{\lambda}^H \frac{\partial \mathbf{A}}{\partial m_p} \mathbf{x}\right]$$
adjoint 변수 $\boldsymbol{\lambda} = \mathbf{A}^{-H}\frac{\partial F}{\partial \mathbf{x}^*}$를 이용한 효율적 그래디언트 계산.

**선형화 EUV 마스크 모델:**
$$M_{3D}(\mathbf{f}; m) \approx M_{3D,0}(\mathbf{f}) + \nabla_{m} M_{3D}\bigg|_{m_0} \cdot (m - m_0)$$
기준 마스크 $m_0$에서의 선형 근사.

**선형화 그래디언트 (1차 근사):**
$$\frac{\partial F_{linear}}{\partial m_p} \approx \frac{\partial F}{\partial M_{3D}} \cdot \frac{\partial M_{3D,linear}}{\partial m_p}$$

**두꺼운 마스크 효과 보정:**
$$I_{corrected}(x) = I_{target}(x) + \Delta I_{3D}(x; m_{OPC})$$
OPC 마스크에서 두꺼운 마스크 효과에 의한 이미지 변화 $\Delta I_{3D}$.

**40% 효율 향상 (거친 최적화):**
$$T_{linear} \approx 0.6 \times T_{full-adjoint}$$

## OPC 툴 SMO 구현 관련성
- SKOPC EUV 마스크 최적화에서 adjoint 방법 기반 그래디언트 계산 구현 시 참고
- `skopc/modeling/euv_mask_adjoint.py`에 Adjoint 기반 EUV 마스크 그래디언트 구현
- `skopc/litho/linearized_3d_mask.py`에 선형화 EUV 마스크 모델 구현
- Coskun et al. 2011 마스크 토포그래피 SMO, Zhang et al. 2024 robust SPO thick mask와 함께 EUV thick mask 최적화 계열 참고

## 참고문헌 (핵심)
- Coskun et al., \"Mask topography SMO advanced nodes,\" SPIE 2011
- Zhang et al., \"EUV SMO thick mask SL-PSO,\" Optics Express 2021
- Ma et al., \"Gradient SMO EUV,\" IEEE TCI 2019

## 태그
`ILT`, `OPC`, `EUV`, `Optics-Express`, `adjoint-method`, `linearized-gradient`, `thick-mask`, `M3D`, `mask-optimization`, `40pct-speedup`, `coarse-optimization`
