# Fast Source Mask Optimization Adopting Mask Prediction and Feedback Method with Similarity Penalty

## 메타데이터
- **저자**: Weichen Huang, Yanqiu Li, Miao Yuan, Zhaoxuan Li, He Yang, Zhen Li
- **연도**: 2025
- **게재지/학회**: Applied Optics, Vol. 64, No. 1, pp. 40–49
- **DOI/URL**: https://doi.org/10.1364/AO.542256
- **인용수**: 확인 필요

## 핵심 요약
마스크 예측 피드백(Mask Prediction Feedback, MPF) 방법과 유사도 패널티(similarity penalty) 항을 결합하여 SMO 수렴 속도를 가속하는 방법을 제안한다. MPF 방법은 이전 반복에서의 마스크와 그래디언트 정보를 활용하여 더 효율적인 마스크 업데이트를 수행하고, 유사도 패널티 항은 최적화 경로를 안정화한다. Adam 최적화 대비 30% 이상의 실행 시간 감소를 달성한다.

## 주요 기여
- 마스크 예측 피드백(MPF) 방법으로 이전 반복 정보를 활용한 마스크 업데이트 가속
- 손실 함수에 유사도 패널티 항 추가로 최적화 경로 안정화
- Adam 대비 30% 이상 실행 시간 감소 달성
- 절제 실험으로 MPF 및 유사도 패널티의 개별/결합 효과 정량화

## 알고리즘/수식
**유사도 패널티 포함 SMO 비용함수:**
$$\min_{\boldsymbol{\sigma}, m} F_{total} = F_{SMO}(\boldsymbol{\sigma}, m) + \lambda_{sim} F_{sim}(m^{(t)}, m^{(t-1)})$$

**유사도 패널티 항:**
$$F_{sim}(m^{(t)}, m^{(t-1)}) = 1 - \frac{\langle m^{(t)}, m^{(t-1)} \rangle}{\|m^{(t)}\| \cdot \|m^{(t-1)}\|}$$
코사인 유사도 기반 연속 반복 간 마스크 변화 제어.

**마스크 예측 피드백 (MPF):**
$$\tilde{m}^{(t)} = m^{(t-1)} + \gamma \Delta m^{(t-1)}$$
이전 반복의 마스크 변화량 $\Delta m^{(t-1)}$을 이용한 예측값 $\tilde{m}^{(t)}$ 생성.

마스크 업데이트 시 예측값 피드백:
$$m^{(t+1)} = m^{(t)} - \eta_m \nabla_m F_{total} + \beta(\tilde{m}^{(t)} - m^{(t)})$$

**Adam 기반 소스 업데이트:**
$$\sigma^{(t+1)} \leftarrow \text{Adam}(\sigma^{(t)}, \nabla_\sigma F_{total})$$

**속도 향상:**
Adam 단독 대비 실행 시간 30% 이상 감소.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 수렴 속도 개선 시 MPF 방법 및 유사도 패널티 적용 참고
- `skopc/smo/fast_smo_mpf.py`에 마스크 예측 피드백 기반 가속 SMO 구현
- 유사도 패널티는 마스크 급격한 변화 억제로 MRC(Mask Rule Check) 친화적 최적화에 활용
- Adam 기반 SMO의 수렴 안정성 향상 방법으로 기존 구현에 추가 가능

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Shen et al., "Adaptive gradient SMO process awareness," Chinese Optics Letters 2019
- Ma et al., "Gradient EUV SMO," IEEE TCI 2019

## 태그
`SMO`, `Applied-Optics`, `mask-prediction-feedback`, `MPF`, `similarity-penalty`, `fast-SMO`, `Adam`, `convergence-acceleration`, `mask-optimization`, `cosine-similarity`
