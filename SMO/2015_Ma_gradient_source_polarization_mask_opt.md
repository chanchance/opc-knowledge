# Gradient-Based Joint Source Polarization Mask Optimization for Optical Lithography

## 메타데이터
- **저자**: Xu Ma, Lisong Dong, Chunying Han, Jie Gao, Yanqiu Li, Gonzalo R. Arce
- **연도**: 2015
- **게재지/학회**: Journal of Micro/Nanolithography, MEMS, and MOEMS (JM3), Vol. 14, No. 2, 023504
- **DOI/URL**: https://doi.org/10.1117/1.JMM.14.2.023504
- **인용수**: 다수

## 핵심 요약
기존 SMO가 편광 상태를 고정하는 한계를 극복하여, 소스 편광 상태를 추가 최적화 변수로 도입한 소스-편광-마스크 동시 최적화(SPMO) 프레임워크를 제안한다. 벡터 이미징 모델을 해석적으로 공식화하고, 동시 SPMO(SISPMO)와 순차 SPMO(SESPMO) 두 가지 최적화 방법을 그래디언트 기반 알고리즘으로 구현한다. 편광 자유도 추가로 SMO 해 공간이 확장되어 공정 마진이 향상된다.

## 주요 기여
- 소스 편광 상태를 추가 최적화 변수로 포함하는 SPMO 프레임워크 최초 제안
- 벡터 이미징 모델 기반 해석적 SPMO 공식화 (TM/TE 편광 분리)
- 동시(SISPMO)와 순차(SESPMO) 두 가지 최적화 전략 비교
- 기존 SMO(편광 고정) 대비 공정 마진 추가 향상 실증

## 알고리즘/수식
**벡터 이미징 모델 (편광 포함):**
$$I(x) = \sum_{k} \left[\sigma_k^{TE} |h_k^{TE}(x) * m(x)|^2 + \sigma_k^{TM} |h_k^{TM}(x) * m(x)|^2\right]$$
여기서 $\sigma_k^{TE}$, $\sigma_k^{TM}$은 각 소스 픽셀의 TE/TM 편광 강도.

**편광 최적화 변수:**
각 소스 픽셀 $k$에 대해:
$$\sigma_k^{TE} = \sigma_k \cdot \cos^2(\phi_k), \quad \sigma_k^{TM} = \sigma_k \cdot \sin^2(\phi_k)$$
여기서 $\phi_k$는 편광각 (0~π/2).

**SPMO 목적함수:**
$$\min_{\{\sigma_k, \phi_k\}, m} F = \sum_j EPE_j^2 + \lambda_s R_s + \lambda_m R_m$$

**그래디언트 도출:**
$$\frac{\partial F}{\partial \phi_k} = \sum_x \frac{\partial F}{\partial I(x)} \cdot 2\sigma_k\left(-\sin\phi_k\cos\phi_k |h_k^{TE}*m|^2 + \cos\phi_k\sin\phi_k|h_k^{TM}*m|^2\right)$$

**SISPMO (동시 최적화):**
$$[\sigma^*, \phi^*, m^*] = \arg\min F(\sigma, \phi, m)$$
세 변수를 동시에 업데이트.

**SESPMO (순차 최적화):**
1. $(\sigma, \phi)$ 고정 → $m$ 최적화
2. $m$ 고정 → $(\sigma, \phi)$ 최적화
3. 수렴까지 반복

## OPC 툴 SMO 구현 관련성
- SKOPC SMO를 편광 최적화로 확장할 때 직접 참조
- 고-NA EUV 또는 편광 조명이 중요한 ArF 이머젼 공정에 적용 가능
- `skopc/smo/polarization_optimizer.py` 구현 시 벡터 이미징 모델 및 그래디언트 공식 활용
- 편광각 $\phi_k$를 소스 픽셀 파라미터로 추가하는 방법 제시

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO in optical lithography," IEEE TIP 2011
- Ma & Arce, "Generalized inverse lithography methods," Optics Express 2007
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008

## 태그
`SMO`, `SPIE`, `JM3`, `polarization-optimization`, `SPMO`, `vector-imaging-model`, `TE-TM-polarization`, `gradient-based`, `source-polarization-mask`, `high-NA`
