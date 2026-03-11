# Lithographic Source Optimization Based on Adaptive Projection Compressive Sensing

## 메타데이터
- **저자**: Xu Ma, D. Shi, Zhiqiang Wang, Yanqiu Li, Gonzalo R. Arce
- **연도**: 2017
- **게재지/학회**: Optics Express, Vol. 25, No. 6, pp. 7131–7149
- **DOI/URL**: https://doi.org/10.1364/OE.25.007131
- **인용수**: 다수

## 핵심 요약
목표 레이아웃 패턴의 사전 지식(a-priori knowledge)을 활용하여 데이터 적응형 압축 센싱(Adaptive Projection CS) 방법으로 효율적인 소스 최적화를 수행하는 방법을 제안한다. 마스크 패턴의 회절 특성에 맞춤화된 측정 행렬을 설계하여 기존 랜덤 CS 대비 소스 재구성 정확도와 효율을 향상시킨다.

## 주요 기여
- 레이아웃 패턴 사전 지식으로 데이터 적응형 CS 측정 행렬 설계
- 적응형 투영으로 소스 최적화 정확도 및 효율 향상
- 랜덤 CS 대비 우수한 소스 재구성 성능 실증
- 패턴별 최적화 측정 행렬로 타겟 레이아웃 특성 반영

## 알고리즘/수식
**적응형 투영 CS 소스 최적화:**
$$\min_{\boldsymbol{a}} \|\boldsymbol{a}\|_1 \quad \text{s.t.} \quad \|\Psi_{adap} \Phi \boldsymbol{a} - \boldsymbol{b}_{adap}\|_2^2 \leq \epsilon$$
적응형 측정 행렬 $\Psi_{adap}$으로 소스 계수 $\boldsymbol{a}$ 재구성.

**적응형 측정 행렬 설계:**
$$\Psi_{adap} = T(\text{mask pattern}) \cdot \Phi$$
마스크 패턴의 회절 특성 $T$에 기반하여 측정 투영 방향 선택:
$$[\Psi_{adap}]_{i,k} = \sum_x h_k(x) \cdot \psi_i(x)$$
패턴 관련 투영 벡터 $\psi_i$를 적응적으로 선택.

**CS 재구성 (ISTA/FISTA):**
$$\boldsymbol{a}^{(t+1)} = \text{shrink}\left(\boldsymbol{a}^{(t)} - \frac{1}{L}\Phi^T \Psi_{adap}^T(\Psi_{adap}\Phi\boldsymbol{a}^{(t)} - \boldsymbol{b}_{adap}), \frac{\lambda}{L}\right)$$
FISTA(Fast ISTA) 반복으로 l1 최소화.

**적응형 측정 vs. 랜덤 측정:**
- 랜덤 CS: $\Psi_{random}$ — 패턴 독립적
- 적응형 CS: $\Psi_{adap}$ — 마스크 회절 구조 반영
→ 같은 측정 수에서 적응형이 더 정확한 소스 재구성.

**소스 스파스 표현:**
$$\boldsymbol{\sigma} = \Phi \boldsymbol{a}, \quad \|\boldsymbol{a}\|_0 \ll N_{src}$$

## OPC 툴 SMO 구현 관련성
- SKOPC CS 기반 소스 최적화에서 마스크 패턴 사전 지식을 측정 행렬 설계에 활용 참고
- `skopc/smo/adaptive_cs_source_opt.py`에 적응형 투영 CS 소스 최적화 구현
- Ma et al. 2018 회절 부분공간 방법과 함께 패턴 기반 소스 최적화 계열로 참고
- Song et al. 2014 CS 소스 최적화의 적응형 확장 버전으로 성능 비교 참고

## 참고문헌 (핵심)
- Song et al., "Inverse litho source opt CS," Optics Express 2014
- Ma et al., "Diffraction subspace illumination opt," Optics Express 2018
- Wang et al., "Fast pixelated SMO CS," IEEE TASE 2020

## 태그
`SMO`, `Optics-Express`, `compressive-sensing`, `adaptive-projection`, `source-optimization`, `measurement-matrix`, `a-priori-knowledge`, `FISTA`, `ISTA`, `sparse-source`, `layout-aware`
