# Fast Source Mask Co-Optimization Method for High-NA EUV Lithography

## 메타데이터
- **저자**: Ziqi Li, Lisong Dong, Xu Ma, Yayi Wei
- **연도**: 2024
- **게재지/학회**: Opto-Electronic Advances, Vol. 7, No. 4, 230235
- **DOI/URL**: https://doi.org/10.29026/oea.2024.230235
- **인용수**: 확인 필요

## 핵심 요약
고-NA EUV 리소그래피(NA=0.55)를 위한 빠른 소스-마스크 동시 최적화(SMO) 방법을 제안한다. 그래디언트 기반 마스크 최적화 알고리즘과 압축 센싱(CS) 기반 소스 최적화 알고리즘을 결합하여 이미지 충실도를 높이고 계산 효율을 유지한다. 최적화된 마스크 패턴을 단순화하는 마스크 규칙 검사(MRC) 프로세스도 통합한다.

## 주요 기여
- 그래디언트 기반 마스크 최적화 + CS 기반 소스 최적화의 하이브리드 SMO
- 고-NA EUV 특유의 anamorphic 광학계 및 M3D 효과를 모델에 통합
- MRC(Mask Rule Check) 프로세스를 통한 최적화 마스크 제조 가능성 향상
- 28nm 이하 기술 노드 고-NA EUV에서 패터닝 오차 대폭 감소 실증

## 알고리즘/수식
**고-NA EUV 이미징 모델:**
$$I(x) = \sum_k \sigma_k |h_k^{0.55NA}(x) * m_{3D}(x)|^2$$

**하이브리드 SMO 흐름:**
```
초기화: σ₀, m₀
반복:
  소스 최적화: σ ← CS-SO(A(m), I_target)  # 압축 센싱 기반
  마스크 최적화: m ← ∇-MO(σ, m)           # 그래디언트 기반
  MRC 후처리: m ← MRC(m)                   # 마스크 규칙 적용
수렴 판정
```

**CS 기반 소스 최적화:**
$$\min_{\sigma \geq 0} \|\mathbf{A}(m)\sigma - I_{target}\|_2^2 + \lambda\|\sigma\|_1$$
→ NNLS 또는 ADMM으로 효율적 풀이.

**그래디언트 기반 마스크 최적화:**
$$m^{(t+1)} = m^{(t)} - \mu \nabla_m F(I(x; \sigma^*, m^{(t)}))$$
$$\nabla_m F = 2\sum_k \sigma_k^* \text{Re}\left[(h_k * m)^* \cdot h_k\right] \cdot \frac{\partial F}{\partial I}$$

**MRC 제약 조건:**
- 최소 피처 크기(MFS): $w_{feature} \geq MFS_{min}$
- 최소 간격: $d_{gap} \geq d_{min}$
- 코너 라운딩 반경: $r \leq r_{max}$

## OPC 툴 SMO 구현 관련성
- SKOPC 고-NA EUV SMO 구현 시 하이브리드 CS+그래디언트 방법의 직접 참고
- `skopc/smo/hybrid_smo.py` 구현 시 CS 소스 최적화와 그래디언트 마스크 최적화 통합 방법 참고
- MRC 통합 방법은 `skopc/modeling/opc/mrc.py`와 SMO 연동 설계에 활용
- 고-NA EUV (0.55 NA) anamorphic 모델 구현 참고

## 참고문헌 (핵심)
- Wang et al., "Fast pixelated SMO based on compressive sensing," IEEE TASE 2020
- Ma et al., "Gradient-based SMO for EUV," IEEE TCI 2019
- Liu et al., "EUV SMO for 7nm node," Proc. SPIE 9048, 2014

## 태그
`SMO`, `high-NA-EUV`, `fast-SMO`, `compressive-sensing`, `gradient-based`, `MRC`, `mask-rule-check`, `hybrid-optimization`, `0.55NA`, `anamorphic`, `Opto-Electronic-Advances`
