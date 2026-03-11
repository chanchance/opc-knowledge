# Spectrum Optimization During SMO: Simultaneous Source-Mask-Laser Spectrum Optimization

## 메타데이터
- **저자**: Evgeny Malankin, Neal Lafferty, Mikhail Silakov, Ekaterina Semenova, Takamitsu Komaki, Kouichi Fujii, Taisuke Miura, Gouta Niimi, Taku Yamazaki
- **연도**: 2022
- **게재지/학회**: Proc. SPIE 12052, Optical Microlithography XXXV, 1205205 (26 May 2022)
- **DOI/URL**: https://doi.org/10.1117/12.2614055
- **인용수**: 확인 필요

## 핵심 요약
기존 SMO(소스-마스크 최적화)를 레이저 스펙트럼 최적화로 확장하여 소스-마스크-레이저 스펙트럼 동시 최적화를 수행한다. 레이저 대역폭 증가에 따른 스페클(speckle) 대비 감소 효과를 분석하며, ArF 이머젼 리소그래피에서 레이저 대역폭 형상 및 비대칭성이 CD에 미치는 영향을 정량화한다. SMO의 세 번째 최적화 변수로 레이저 스펙트럼을 추가함으로써 추가적인 공정 마진 향상을 달성한다.

## 주요 기여
- SMO에 레이저 스펙트럼 최적화 변수 추가 (소스+마스크+스펙트럼 3중 동시 최적화)
- 레이저 대역폭 증가가 스페클 대비 및 CD 균일도에 미치는 정량적 분석
- 대역폭 형상(bandwidth shape) 및 비대칭성(asymmetry)의 CD 영향 모델링
- ArFi 리소그래피에서 스펙트럼 최적화의 추가적 공정 마진 향상 실증

## 알고리즘/수식
**스펙트럼 포함 이미징 모델:**
$$I(x) = \int S(\lambda) \left[\sum_k \sigma_k(\lambda) |h_k(x;\lambda) * m(x)|^2\right] d\lambda$$
여기서 $S(\lambda)$는 레이저 스펙트럼 강도 분포.

**이산화 근사:**
$$I(x) \approx \sum_n w_n \sum_k \sigma_k^{(n)} |h_k^{(n)}(x) * m(x)|^2$$
여기서 $w_n = S(\lambda_n) \Delta\lambda$는 스펙트럼 가중치.

**3중 최적화 문제:**
$$\min_{\sigma, m, S} F(I(\sigma, m, S))$$
subject to: $\sigma \geq 0$, $S \geq 0$, $\int S d\lambda = 1$, 마스크 제약 조건

**스페클 모델 (부분 코히어런스):**
$$\text{Speckle Contrast} = \frac{\sigma_{I}}{\bar{I}} \propto \frac{1}{\sqrt{N_{coherent}}}$$
대역폭 증가 → 시간 코히어런스 감소 → 스페클 대비 감소.

**대역폭-CD 관계:**
$$\Delta CD \approx \alpha \cdot \frac{\partial^2 I}{\partial\lambda^2} \cdot \Delta\lambda^2$$
대역폭 비대칭이 CD 시프트 유발.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 확장 시 레이저 스펙트럼 변수 추가 방법 제공
- ArFi 리소그래피에서 레이저 대역폭을 추가 최적화 변수로 도입 가능
- `skopc/litho/spectral_model.py` 구현 시 다파장 이미징 모델 참고
- 스페클 효과 모델링을 시뮬레이션 엔진에 통합하는 방법 제시

## 참고문헌 (핵심)
- Komaki et al., "Study of image performance improvement by spectral bandwidth for ArFi," Proc. SPIE 2021
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008
- Peng et al., "Gradient-based SMO," IEEE TIP 2011

## 태그
`SMO`, `SPIE`, `laser-spectrum-optimization`, `bandwidth`, `speckle`, `ArF-immersion`, `tri-optimization`, `source-mask-spectrum`, `partial-coherence`, `CD-uniformity`
