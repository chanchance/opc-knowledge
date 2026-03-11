# Fast Heuristic-Based Source Mask Optimization for EUV Lithography Using Dual Edge Evolution and Partial Sampling

## 메타데이터
- **저자**: Zinan Zhang, Sikun Li, Xiangzhao Wang (외, SIOM/CAS)
- **연도**: 2021
- **게재지/학회**: Optics Express, Vol. 29, No. 14, pp. 22778–22795
- **DOI/URL**: https://doi.org/10.1364/OE.430088
- **인용수**: 다수

## 핵심 요약
EUV 리소그래피 SMO의 계산 효율을 대폭 향상시키기 위해 이중 에지 진화(dual edge evolution)와 부분 샘플링(partial sampling) 전략을 결합한 빠른 휴리스틱 SMO 방법을 제안한다. 이중 에지 진화는 마스크 경계의 두 방향 동시 탐색으로 수렴 속도를 높이고, 부분 샘플링은 매 반복마다 평가할 샘플 수를 선택적으로 줄여 연산 비용을 절감한다. 기존 휴리스틱 SMO 대비 최적화 속도를 크게 향상시키면서 유사한 패턴 오차 성능을 유지한다.

## 주요 기여
- 이중 에지 진화(dual edge evolution) 전략으로 마스크 최적화 수렴 가속
- 부분 샘플링(partial sampling)으로 반복당 계산 비용 절감
- EUV 두꺼운 마스크 모델과 결합한 빠른 휴리스틱 SMO 프레임워크
- 기존 휴리스틱 SMO 대비 속도 향상 실증 (SIOM/CAS)

## 알고리즘/수식
**SMO 목적함수:**
$$\min_{\boldsymbol{\sigma}, m} F(\boldsymbol{\sigma}, m) = \sum_{j \in \Omega_{PS}} EPE_j^2(\boldsymbol{\sigma}, m)$$
부분 샘플링 집합 $\Omega_{PS} \subset \Omega_{all}$에서만 EPE 계산.

**이중 에지 진화 (Dual Edge Evolution):**
마스크 에지 픽셀의 두 방향(확장/수축) 동시 탐색:
$$\Delta m_j^{+} = +1 \text{ (에지 확장)}, \quad \Delta m_j^{-} = -1 \text{ (에지 수축)}$$
각 에지 픽셀에 대해 두 가지 변화를 동시 평가 → 최적 방향 선택.

**부분 샘플링 전략:**
$$\Omega_{PS}^{(t)} \subset \Omega_{all}, \quad |\Omega_{PS}^{(t)}| = r \cdot |\Omega_{all}|, \quad r < 1$$
비율 $r$로 평가점 무작위 선택 → 계산량 $O(r \cdot N)$으로 감소.

**반복 알고리즘:**
```
1. 소스 초기화 σ⁰, 마스크 초기화 m⁰
2. 반복:
   a. 부분 샘플링으로 평가점 Ω_PS 선택
   b. 이중 에지 진화로 마스크 에지 업데이트
   c. PSO/진화 전략으로 소스 업데이트
   d. 수렴 체크
3. 최적 (σ*, m*) 반환
```

**속도 향상:**
부분 샘플링 비율 $r$ 조절로 속도-정확도 트레이드오프 제어.

## OPC 툴 SMO 구현 관련성
- SKOPC 빠른 휴리스틱 SMO 구현 시 이중 에지 진화 및 부분 샘플링 전략 참고
- `skopc/smo/fast_heuristic_smo.py` 구현으로 계산 효율적 EUV SMO 가능
- 부분 샘플링 아이디어는 대규모 레이아웃 SMO에서 클립 샘플링 전략으로 응용 가능
- 이중 에지 진화는 ILT 마스크 경계 업데이트 가속에도 적용 가능

## 참고문헌 (핵심)
- Zhang et al., "EUV SMO SL-PSO thick mask," Optics Express 2021
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Wang et al., "Fast pixelated SMO compressive sensing," IEEE TASE 2020

## 태그
`SMO`, `Optics-Express`, `EUV-lithography`, `dual-edge-evolution`, `partial-sampling`, `heuristic`, `fast-SMO`, `computational-efficiency`, `mask-optimization`, `SIOM`, `CAS`, `gradient-free`
