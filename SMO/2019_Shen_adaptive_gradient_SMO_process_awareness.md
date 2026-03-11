# Adaptive Gradient-Based Source and Mask Co-Optimization with Process Awareness

## 메타데이터
- **저자**: Yijiang Shen, Fei Peng, Xiaoyan Huang, Zhenrong Zhang
- **연도**: 2019
- **게재지/학회**: Chinese Optics Letters, Vol. 17, Article 121102
- **DOI/URL**: https://doi.org/10.3788/COL201917.121102
- **인용수**: 다수

## 핵심 요약
EPE(Edge Placement Error)와 PV Band(공정 변동성 대역)를 동시에 최소화하는 공정 인식(process-aware) 적응형 그래디언트 SMO 방법을 제안한다. 벡터 이미징 모델 기반의 닫힌 형태(closed-form) 그래디언트를 유도하고, 소스 업데이트에 AdaGrad, 마스크 업데이트에 Adam을 각각 적용하는 이중 적응형 학습률 전략으로 패턴 충실도와 공정 마진을 동시에 향상시킨다.

## 주요 기여
- EPE와 PV Band를 동시에 고려하는 공정 인식 SMO 비용함수 설계
- 벡터 이미징 모델 기반 EPE/PV Band 닫힌 형태 그래디언트 유도
- 소스에 AdaGrad, 마스크에 Adam 적용하는 이중 적응형 학습률 전략
- 기존 그래디언트 SMO 대비 공정 마진 및 초기 조건 안정성 향상

## 알고리즘/수식
**공정 인식 SMO 목적함수:**
$$\min_{\boldsymbol{\sigma}, m} F = F_{EPE}(\boldsymbol{\sigma}, m) + \lambda_{PV} F_{PV}(\boldsymbol{\sigma}, m)$$

**EPE 비용함수:**
$$F_{EPE} = \sum_j \left(EPE_j(\boldsymbol{\sigma}, m)\right)^2 = \sum_j \left(\frac{I(x_j) - I_{th}}{|\nabla I(x_j)|}\right)^2$$

**PV Band 비용함수:**
$$F_{PV} = \sum_j \left(EPE_j^{max} - EPE_j^{min}\right)^2$$
도즈·포커스 변동 범위 내 최대/최소 EPE 차이의 제곱합.

**소스 업데이트 (AdaGrad):**
$$G_k^{(t)} = G_k^{(t-1)} + \left(\frac{\partial F}{\partial \sigma_k}\right)^2$$
$$\sigma_k^{(t+1)} = \sigma_k^{(t)} - \frac{\eta}{\sqrt{G_k^{(t)} + \epsilon}} \frac{\partial F}{\partial \sigma_k}$$
누적 제곱 그래디언트로 학습률 자동 조정.

**마스크 업데이트 (Adam):**
$$\hat{v}_{j}^{(t)} = \frac{\beta_1 v_j^{(t-1)} + (1-\beta_1)\frac{\partial F}{\partial m_j}}{1-\beta_1^t}$$
$$\hat{s}_{j}^{(t)} = \frac{\beta_2 s_j^{(t-1)} + (1-\beta_2)\left(\frac{\partial F}{\partial m_j}\right)^2}{1-\beta_2^t}$$
$$m_j^{(t+1)} = m_j^{(t)} - \frac{\eta}{\sqrt{\hat{s}_j^{(t)}} + \epsilon} \hat{v}_j^{(t)}$$

**벡터 이미징 모델:**
$$I(x) = \sum_k \sigma_k \left|h_k^{TE} * m\right|^2 + \sum_k \sigma_k \left|h_k^{TM} * m\right|^2$$
TE/TM 편광 성분을 모두 포함하는 벡터 aerial image.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에 AdaGrad/Adam 이중 학습률 전략 적용 시 핵심 참고
- `skopc/smo/adaptive_smo.py`에 공정 인식 EPE+PV Band 비용함수 구현 참고
- PV Band 기반 공정 마진 최적화는 `skopc/smo/process_window_smo.py`에 활용
- 소스/마스크에 서로 다른 적응형 최적화 알고리즘 적용하는 이중 전략 설계 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Jia & Lam, "Pixelated SMO process robustness," Optics Express 2011
- Shen, "Narrow-band level-set SMO," Optics Express 2018

## 태그
`SMO`, `Chinese-Optics-Letters`, `adaptive-gradient`, `AdaGrad`, `Adam`, `process-awareness`, `PV-Band`, `EPE`, `vector-imaging`, `immersion-lithography`, `process-window`, `closed-form-gradient`
