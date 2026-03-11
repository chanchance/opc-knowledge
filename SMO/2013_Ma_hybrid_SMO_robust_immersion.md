# Hybrid Source Mask Optimization for Robust Immersion Lithography

## 메타데이터
- **저자**: Xu Ma, Chunying Han, Yanqiu Li, Bingliang Wu, Zhiyang Song, Lisong Dong, Gonzalo R. Arce
- **연도**: 2013
- **게재지/학회**: Applied Optics, Vol. 52, No. 18, pp. 4200–4211
- **DOI/URL**: https://doi.org/10.1364/AO.52.004200
- **인용수**: 다수

## 핵심 요약
침지 리소그래피(immersion lithography)의 도즈·포커스 변동에 대한 강인성을 향상시키기 위해 벡터 이미징 모델 기반 하이브리드 SMO(HSMO) 알고리즘을 제안한다. 1단계에서 개별 소스 최적화(SO)로 비용함수를 신속히 감소시키고, 2단계에서 소스·마스크 동시 최적화(SISMO)로 공정 강인성을 추가 향상시키는 2단계 하이브리드 전략을 채택한다. 켤레 그래디언트(conjugate gradient) 방법으로 소스/마스크 픽셀을 업데이트한다.

## 주요 기여
- 벡터 이미징 모델 기반 강인성 향상 HSMO 알고리즘 제안
- 1단계 SO + 2단계 SISMO의 2단계 하이브리드 전략으로 수렴 가속 및 성능 향상
- 켤레 그래디언트 방법 기반 소스/마스크 업데이트
- 도즈·포커스 변동에 대한 공정 강인성 최적화 실증

## 알고리즘/수식
**강인성 SMO 목적함수:**
$$\min_{\boldsymbol{\sigma}, m} F_{robust} = F_{nominal} + \lambda_d F_{dose} + \lambda_f F_{defocus}$$
공칭 비용함수에 도즈·포커스 변동 항 추가.

**벡터 이미징 모델 (침지 리소그래피):**
$$I(x) = \sum_k \sigma_k \left(\left|h_k^x * m\right|^2 + \left|h_k^y * m\right|^2 + \left|h_k^z * m\right|^2\right)$$
x, y, z 편광 성분의 coherent system 합.

**하이브리드 SMO 2단계 알고리즘:**
```
단계 1: 개별 소스 최적화 (SO)
  - 마스크 m 고정
  - 켤레 그래디언트로 σ 최적화 → 빠른 비용함수 감소

단계 2: 동시 SMO (SISMO)
  - σ와 m 동시 업데이트
  - 켤레 그래디언트로 공동 최적화 → 공정 강인성 향상
```

**켤레 그래디언트 업데이트:**
$$d^{(t)} = -\nabla F^{(t)} + \beta^{(t)} d^{(t-1)}, \quad \beta^{(t)} = \frac{||\nabla F^{(t)}||^2}{||\nabla F^{(t-1)}||^2} \text{ (Fletcher-Reeves)}$$
$$\sigma^{(t+1)} = \sigma^{(t)} + \alpha^{(t)} d^{(t)}$$

**소스 그래디언트:**
$$\frac{\partial F_{robust}}{\partial \sigma_k} = \frac{\partial F_{nominal}}{\partial \sigma_k} + \lambda_d \frac{\partial F_{dose}}{\partial \sigma_k} + \lambda_f \frac{\partial F_{defocus}}{\partial \sigma_k}$$

## OPC 툴 SMO 구현 관련성
- SKOPC 강인 SMO 구현 시 2단계 하이브리드 전략(SO 선행 + SISMO 정밀화) 참고
- 켤레 그래디언트 방법은 `skopc/smo/gradient_smo.py`의 최적화 루프에 활용
- 벡터 이미징 모델 기반 강인성 비용함수 설계 참고
- 도즈·포커스 강인성 최적화는 `skopc/smo/robust_smo.py` 구현에 활용

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Ma et al., "Gradient SPMO," JM3 2015
- Hashimoto et al., "Robust SMO," SPIE 2013
- Jia & Lam, "Pixelated SMO process robustness," Optics Express 2011

## 태그
`SMO`, `Applied-Optics`, `hybrid-SMO`, `robust-SMO`, `immersion-lithography`, `conjugate-gradient`, `vector-imaging`, `dose-robustness`, `defocus-robustness`, `two-stage`, `process-window`
