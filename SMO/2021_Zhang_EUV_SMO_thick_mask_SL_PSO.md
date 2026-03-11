# Source Mask Optimization for EUV Lithography Based on Thick Mask Model and Social Learning Particle Swarm Optimization Algorithm

## 메타데이터
- **저자**: Zinan Zhang, Sikun Li, Xiangzhao Wang, Wei Cheng, Yuejing Qi
- **연도**: 2021
- **게재지/학회**: Optics Express, Vol. 29, No. 4, pp. 5448–5465
- **DOI/URL**: https://doi.org/10.1364/OE.418242
- **인용수**: 다수

## 핵심 요약
EUV 리소그래피에서 두꺼운 마스크 모델(thick mask model)과 사회 학습 입자 군집 최적화(Social Learning Particle Swarm Optimization, SL-PSO) 알고리즘을 결합한 SMO 방법을 제안한다. 구조 분해 방법(SDM) 기반 빠른 두꺼운 마스크 모델로 시뮬레이션 정확도를 개선하면서, SL-PSO의 사회 학습 전략으로 최적화 효율을 향상시킨다. 세 가지 패턴에서 패턴 오차 94.7%, 76.9%, 80.6% 감소를 실증한다.

## 주요 기여
- SDM 기반 빠른 두꺼운 마스크 모델과 SL-PSO의 결합으로 EUV SMO 정확도 및 효율 향상
- 사회 학습 전략을 통한 PSO 수렴 속도 개선
- 초기화 파라미터 튜닝으로 최적화 마스크 제조 가능성 향상
- 세 패턴에서 패턴 오차 최대 94.7% 감소 실증 (SIOM/CAS)

## 알고리즘/수식
**SL-PSO 기반 SMO 목적함수:**
$$\min_{\boldsymbol{\sigma}, m} F = \sum_j \left(I(x_j; \boldsymbol{\sigma}, m) - I_{target}(x_j)\right)^2$$
두꺼운 마스크 모델로 계산된 aerial image $I$와 목표 이미지 $I_{target}$ 차이 최소화.

**SL-PSO 속도/위치 업데이트:**
$$v_i^{(t+1)} = w v_i^{(t)} + c_1 r_1 (p_i^{best} - x_i^{(t)}) + c_2 r_2 (g^{best} - x_i^{(t)}) + c_3 r_3 (x_{demo} - x_i^{(t)})$$
사회 학습 항 $c_3 r_3 (x_{demo} - x_i^{(t)})$가 우수 개체의 경험 공유.

$$x_i^{(t+1)} = x_i^{(t)} + v_i^{(t+1)}$$

**두꺼운 마스크 모델 (SDM 기반):**
EUV 마스크의 3D 효과를 구조 분해 방법으로 근사:
$$E_{thick}(f) \approx \sum_k c_k \cdot E_{thin,k}(f)$$
얇은 마스크 모델 $E_{thin,k}$ 조합으로 두꺼운 마스크 회절장 $E_{thick}$ 근사.

**픽셀화 소스 및 마스크 변수:**
$$\boldsymbol{\sigma} = [\sigma_1, \ldots, \sigma_{N_s}] \in [0,1]^{N_s}, \quad m = [m_1, \ldots, m_{N_m}] \in \{0,1\}^{N_m}$$

**패턴 오차 감소율 (실험 결과):**
- 패턴 1: 94.7% 감소
- 패턴 2: 76.9% 감소
- 패턴 3: 80.6% 감소

## OPC 툴 SMO 구현 관련성
- SKOPC EUV SMO에 두꺼운 마스크 모델 기반 SL-PSO 구현 시 핵심 참고
- `skopc/smo/slpso_smo.py` 구현으로 그래디언트 없는 EUV 소스/마스크 전역 최적화 가능
- SDM 기반 빠른 두꺼운 마스크 모델은 `skopc/litho/euv_thick_mask.py`에 참고
- 마스크 제조 가능성을 고려한 PSO 초기화 파라미터 설계 방법 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Ma et al., "Gradient-based EUV SMO," IEEE TCI 2019
- Chen et al., "CMA-ES SMO," Optics Express 2020
- Wang et al., "Adaptive PSO source optimization," 2021

## 태그
`SMO`, `Optics-Express`, `EUV-lithography`, `thick-mask-model`, `SDM`, `SL-PSO`, `social-learning-PSO`, `particle-swarm`, `gradient-free`, `metaheuristic`, `SIOM`, `CAS`, `pixelated-source`, `M3D`
