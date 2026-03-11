# Pixelated Source and Mask Optimization for Immersion Lithography

## 메타데이터
- **저자**: Xu Ma, Chunying Han, Yanqiu Li, Lisong Dong, Gonzalo R. Arce
- **연도**: 2013
- **게재지/학회**: Journal of the Optical Society of America A (JOSAA), Vol. 30, No. 1, pp. 112–123
- **DOI/URL**: https://doi.org/10.1364/JOSAA.30.000112
- **인용수**: 다수

## 핵심 요약
침지 리소그래피에 특화된 벡터 이미징 모델 기반 픽셀화 SMO 알고리즘을 체계적으로 개발한다. 동시 SMO(SISMO), 순차 SMO(SESMO), 하이브리드 SMO(HSMO)의 세 가지 프레임워크를 통합 분석하고 비교한다. 벡터 이미징 모델의 닫힌 형태 그래디언트를 유도하여 개별 소스 최적화(SO), 개별 마스크 최적화(MO), SISMO, SESMO, HSMO의 성능을 정량적으로 비교한다.

## 주요 기여
- 침지 리소그래피 벡터 이미징 모델 기반 픽셀화 SMO 통합 프레임워크 제시
- SISMO, SESMO, HSMO 세 가지 SMO 전략 체계적 비교 분석
- 벡터 이미징 모델 닫힌 형태 그래디언트 유도
- 하이브리드 HSMO가 최우수 성능을 달성함을 실증

## 알고리즘/수식
**벡터 이미징 모델 (침지 리소그래피):**
$$I(x) = \sum_{p \in \{x,y,z\}} \sum_k \sigma_k |h_k^p * m|^2(x)$$
세 편광 성분 $p \in \{x, y, z\}$를 포함하는 완전한 벡터 aerial image.

**SMO 비용함수:**
$$F(\boldsymbol{\sigma}, m) = \sum_j \left(I(x_j; \boldsymbol{\sigma}, m) - I_{target}(x_j)\right)^2$$

**소스 그래디언트 (벡터 이미징):**
$$\frac{\partial F}{\partial \sigma_k} = \sum_{p} \sum_j \frac{\partial F}{\partial I(x_j)} \cdot |h_k^p * m|^2(x_j)$$

**마스크 그래디언트 (벡터 이미징):**
$$\frac{\partial F}{\partial m(x')} = \sum_p \sum_k \sigma_k \cdot 2\text{Re}\left[\overline{(h_k^p * m)(x)} \cdot h_k^p(x - x')\right] \frac{\partial F}{\partial I(x)}$$

**세 SMO 전략 비교:**
1. **SISMO (동시):** $\sigma$와 $m$ 동시 그래디언트 업데이트
2. **SESMO (순차):** SO → MO 반복 순환
3. **HSMO (하이브리드):** SO 선행(단계 1) → SISMO 정밀화(단계 2)

**수렴 비교 결론:**
HSMO > SISMO ≈ SESMO > SO > MO (공정 마진 기준)

## OPC 툴 SMO 구현 관련성
- SKOPC 침지 리소그래피 벡터 SMO 구현의 기본 참고문헌
- `skopc/smo/vector_smo.py`에 TE/TM/z 편광 포함 벡터 이미징 그래디언트 구현
- SISMO/SESMO/HSMO 전략 비교 분석으로 최적 SMO 플로우 선택 기준 제공
- 침지 리소그래피(193nm) SMO 알고리즘 설계의 핵심 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Ma et al., "Hybrid SMO robust immersion," Applied Optics 2013
- Ma et al., "Gradient SPMO," JM3 2015

## 태그
`SMO`, `JOSAA`, `pixelated-SMO`, `vector-imaging`, `immersion-lithography`, `SISMO`, `SESMO`, `HSMO`, `conjugate-gradient`, `193nm`, `polarization`, `closed-form-gradient`, `comparative-study`
