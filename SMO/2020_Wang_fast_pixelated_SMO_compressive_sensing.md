# Fast Pixelated Lithographic Source and Mask Joint Optimization Based on Compressive Sensing

## 메타데이터
- **저자**: Zhiqiang Wang, Xu Ma, Rui Chen, Shengen Zhang, Gonzalo R. Arce
- **연도**: 2020
- **게재지/학회**: IEEE Transactions on Automation Science and Engineering, Vol. 17, No. 2, pp. 981–992
- **DOI/URL**: https://doi.org/10.1109/TASE.2019.2942245 (IEEE document 9108556)
- **인용수**: 다수

## 핵심 요약
압축 센싱(Compressive Sensing, CS)을 활용하여 픽셀화 소스-마스크 동시 최적화의 계산 복잡도를 획기적으로 줄이는 방법을 제안한다. 소스 최적화는 비음수 제약이 있는 선형 CS 복원 문제로 변환하고, 마스크 최적화는 희소성(sparsity)과 저랭크(low-rank) 정규화를 적용한 비선형 CS 방법으로 해결한다. 기존 그래디언트 기반 SMO 대비 수 배의 속도 향상과 함께 이미지 충실도 및 마스크 제조 가능성을 개선한다.

## 주요 기여
- 소스 최적화를 비음수 제약 선형 CS 문제로 재공식화 → 계산 효율 대폭 향상
- 마스크 최적화에 희소성 + 저랭크 정규화 적용한 비선형 CS 방법 개발
- 순차적 교번 최적화(소스↔마스크)로 전체 SMO 프레임워크 구성
- 기존 그래디언트 기반 SMO 대비 수 배 속도 향상 실증

## 알고리즘/수식
**소스 최적화 (선형 CS 문제로 변환):**
SOCS 분해 하에서:
$$I(x) = \sum_k \sigma_k |h_k * m(x)|^2 = \mathbf{A}(m) \cdot \boldsymbol{\sigma}$$
여기서 $\mathbf{A}(m)_{x,k} = |h_k * m(x)|^2$는 마스크 고정 시 선형 시스템.

소스 최적화:
$$\min_{\boldsymbol{\sigma}} \|I_{target} - \mathbf{A}(m)\boldsymbol{\sigma}\|_2^2 + \lambda_s \|\boldsymbol{\sigma}\|_1 \quad \text{s.t.} \quad \boldsymbol{\sigma} \geq 0$$
→ 비음수 제약 LASSO 문제 (NNLS 또는 ADMM으로 효율적 풀이)

**마스크 최적화 (비선형 CS):**
$$\min_{m} F(I(x;m)) + \lambda_{sp} \|m\|_1 + \lambda_{lr} \|M\|_*$$
여기서 $M$은 마스크 행렬, $\|\cdot\|_*$는 핵 노름(nuclear norm, 저랭크 정규화).

**Newton-IHT(Iterative Hard Thresholding) 기반 마스크 업데이트:**
$$m^{(t+1)} = \mathcal{H}_s\left(m^{(t)} - \mu \nabla_m F\right)$$
여기서 $\mathcal{H}_s$는 상위 $s$개 요소만 유지하는 하드 임계화 연산자.

**SMO 교번 최적화:**
```
초기화: σ₀, m₀
반복:
  σ ← NNLS(A(m), I_target)   # 소스 최적화 (선형 CS)
  m ← Newton-IHT(F(σ), m)    # 마스크 최적화 (비선형 CS)
수렴 판정
```

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 가속화 구현 시 CS 기반 소스 최적화 직접 적용 가능
- `skopc/smo/source_optimizer.py`에서 NNLS 솔버 활용 (scipy.optimize.nnls)
- 마스크 희소성 정규화는 `skopc/modeling/opc/` 마스크 이진화 품질 향상에 활용
- 저랭크 정규화는 마스크 제조 가능성(MRC) 개선과 연계 가능

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO in optical lithography," IEEE TIP 2011
- Ma & Arce, "Compressive lithography source optimization," Optics Express 2014
- Wang et al., "Fast nonlinear CS SMO using Newton-IHTs," Optics Express 2019

## 태그
`SMO`, `IEEE`, `compressive-sensing`, `fast-SMO`, `NNLS`, `sparse-regularization`, `low-rank`, `Newton-IHT`, `pixelated-source`, `mask-manufacturability`
