# Parametric Source-Mask-Numerical Aperture Co-Optimization for Immersion Lithography

## 메타데이터
- **저자**: Xuejia Guo, Yanqiu Li, Lisong Dong
- **연도**: 2014
- **게재지/학회**: Journal of Micro/Nanolithography, MEMS, and MOEMS (JM3), Vol. 13, No. 4, Article 043013
- **DOI/URL**: https://doi.org/10.1117/1.JMM.13.4.043013
- **인용수**: 다수

## 핵심 요약
침지 리소그래피에서 소스(Source), 마스크(Mask), 개구수(Numerical Aperture, NA)를 동시에 파라미터화하여 공동 최적화하는 SMNO(Source-Mask-NA Co-Optimization) 방법을 제안한다. 파라미터화된 소스 형상과 마스크 레이아웃이 극도로 단순한 분포를 가져 제조 비용을 효과적으로 절감하면서, 큰 DOF 내에서 높은 패턴 충실도를 유지한다.

## 주요 기여
- 소스, 마스크, NA를 동시에 파라미터화하는 3-변수 SMNO 방법 제안
- 파라미터화된 소스 형상으로 제조 가능한 단순 조명 분포 달성
- 큰 DOF 내 높은 패턴 충실도 유지 실증
- NA 최적화를 통한 추가 공정 마진 향상

## 알고리즘/수식
**SMNO 목적함수:**
$$\min_{\boldsymbol{\theta}_s, m, NA} F(\boldsymbol{\theta}_s, m, NA) = \sum_j EPE_j^2(\boldsymbol{\theta}_s, m, NA)$$
소스 파라미터 $\boldsymbol{\theta}_s$, 마스크 $m$, NA를 동시에 최적화.

**파라미터화된 소스 표현:**
$$\sigma(f,g; \boldsymbol{\theta}_s) = \mathcal{S}(\boldsymbol{\theta}_s; f,g)$$
도넛형, 쿼드루폴, 다이폴 등 기하학적 파라미터 $\boldsymbol{\theta}_s$로 소스 정의.

**NA 파라미터화:**
$$h_k(x; NA) = \mathcal{F}^{-1}\left[P_k(f,g) \cdot \text{circ}\left(\frac{\sqrt{f^2+g^2}}{NA/\lambda}\right)\right]$$
NA 변화에 따른 동공 함수 변화가 커널 $h_k$에 반영.

**그래디언트 기반 최적화:**
$$\boldsymbol{\theta}_s^{(t+1)} = \boldsymbol{\theta}_s^{(t)} - \mu_s \frac{\partial F}{\partial \boldsymbol{\theta}_s}$$
$$NA^{(t+1)} = NA^{(t)} - \mu_{NA} \frac{\partial F}{\partial NA}$$
$$m^{(t+1)} = m^{(t)} - \mu_m \frac{\partial F}{\partial m}$$

**NA 그래디언트:**
$$\frac{\partial F}{\partial NA} = \sum_j \frac{\partial F}{\partial I(x_j)} \cdot \frac{\partial I(x_j)}{\partial NA}$$

**DOF 목적함수 통합:**
$$\min F = F_{EPE,nominal} + \lambda_{DOF} \sum_{i} F_{EPE,defocus_i}$$
다중 디포커스 조건에서 EPE 최소화로 DOF 향상.

## OPC 툴 SMO 구현 관련성
- SKOPC SMNO 구현 시 소스+마스크+NA 3변수 동시 최적화 구조 참고
- `skopc/smo/smno.py`에 NA 파라미터화 및 그래디언트 계산 구현
- 파라미터화 소스는 `skopc/smo/parametric_source.py`의 기하학적 소스 모델과 연동
- Guo et al. 2014 MPLCO와 함께 도구 파라미터 공동 최적화 전략 비교 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Ma et al., "Pixelated SMO immersion," JOSAA 2013
- Guo et al., "MPLCO conjugate gradient," JM3 2014

## 태그
`SMO`, `JM3`, `SMNO`, `numerical-aperture`, `parametric-source`, `NA-optimization`, `immersion-lithography`, `gradient-based`, `DOF`, `EPE`, `three-variable-cooptimization`, `fabrication-cost`
