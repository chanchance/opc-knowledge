# Source and Mask Optimization for Stability of Reticle and Wafer Stages

## 메타데이터
- **저자**: Hao Shen, Libin Zhang, Dinghai Rui, Ge Liu, Yajuan Su, Yayi Wei, Ming Fang
- **연도**: 2024
- **게재지/학회**: Optics Express, Vol. 32, No. 19, pp. 33603–33617
- **DOI/URL**: https://doi.org/10.1364/OE.532914
- **인용수**: 확인 필요

## 핵심 요약
193nm 침지 리소그래피에서 레티클(reticle) 및 웨이퍼 스테이지의 진동 오차를 리소그래피 모델에 통합한 SMO 방법을 제안한다. 40nm 선폭 설계 패턴에 대해 다양한 스테이지 진동 상태에서의 SMO 공동 최적화를 수행하여, 한계 공정(limit process)에서 스테이지 강인성을 향상시킨다. 스테이지 진동을 SMO 비용함수에 직접 반영하는 새로운 강인 SMO 프레임워크를 제시한다.

## 주요 기여
- 스테이지 진동 오차를 리소그래피 이미징 모델에 통합
- 레티클/웨이퍼 스테이지 진동 강인성을 고려한 SMO 비용함수 설계
- 193nm 침지 리소그래피 40nm 선폭 패턴에 대한 진동 강인 SMO 실증
- 한계 공정 조건에서 스테이지 안정성 향상 검증

## 알고리즘/수식
**진동 포함 이미징 모델:**
$$I_{vib}(x) = \int p(\delta) \cdot I(x - \delta; \boldsymbol{\sigma}, m) \, d\delta$$
진동 변위 $\delta$의 확률 분포 $p(\delta)$로 가중 평균한 aerial image.

**가우시안 진동 모델:**
$$p(\delta) = \frac{1}{\sqrt{2\pi}\sigma_{vib}} \exp\left(-\frac{\delta^2}{2\sigma_{vib}^2}\right)$$
진동 표준편차 $\sigma_{vib}$로 스테이지 진동 특성화.

**진동 이미지 근사 (주파수 도메인):**
$$\hat{I}_{vib}(f) = \hat{I}(f) \cdot \exp\left(-2\pi^2 \sigma_{vib}^2 f^2\right)$$
가우시안 진동이 spatial frequency domain에서 저역 통과 필터로 작용.

**강인 SMO 비용함수:**
$$\min_{\boldsymbol{\sigma}, m} F_{robust} = \sum_j EPE_j^2(I_{vib}(x_j; \boldsymbol{\sigma}, m))$$
진동 포함 aerial image 기반 EPE 최소화.

**스테이지 강인성 그래디언트:**
$$\frac{\partial F_{robust}}{\partial \sigma_k} = \sum_j \frac{\partial F}{\partial I_{vib}(x_j)} \cdot \frac{\partial I_{vib}(x_j)}{\partial \sigma_k}$$

**레티클 vs. 웨이퍼 스테이지 진동 구분:**
- 레티클 스테이지: 마스크 패턴 이동 → 마스크 블러링
- 웨이퍼 스테이지: 웨이퍼 이동 → 이미지 블러링
두 진동 효과를 독립적으로 모델링 후 통합.

## OPC 툴 SMO 구현 관련성
- SKOPC 강인 SMO에서 스캐너 스테이지 진동 효과 통합 방법 참고
- `skopc/smo/stage_robust_smo.py`에 진동 포함 aerial image 계산 및 SMO 구현
- 가우시안 진동 저역 통과 필터 모델은 `skopc/litho/vibration_model.py`에 구현 가능
- 스테이지 진동 강인성은 실제 HVM 환경 SMO의 중요 요소로 기존 RSMO에 추가 가능

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Hashimoto et al., "Robust SMO HVM," SPIE 2013
- Jia & Lam, "Pixelated SMO process robustness," Optics Express 2011

## 태그
`SMO`, `Optics-Express`, `stage-vibration`, `robust-SMO`, `reticle-stage`, `wafer-stage`, `193nm`, `immersion-lithography`, `vibration-model`, `process-robustness`, `HVM`
