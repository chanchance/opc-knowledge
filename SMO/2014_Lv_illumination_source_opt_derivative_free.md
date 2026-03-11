# Illumination Source Optimization in Optical Lithography via Derivative-Free Optimization

## 메타데이터
- **저자**: Wen Lv, Shiyuan Liu, Xiaofei Wu, Edmund Y. Lam
- **연도**: 2014
- **게재지/학회**: Journal of the Optical Society of America A (JOSAA), Vol. 31, No. 12, pp. B19–B26
- **DOI/URL**: https://doi.org/10.1364/JOSAA.31.000B19
- **인용수**: 다수

## 핵심 요약
광학 리소그래피 조명 소스 최적화에 미분 불필요(derivative-free optimization, DFO) 방법을 적용하는 새로운 접근법을 제안한다. 닫힌 형태의 그래디언트 공식 없이도 소스 패턴을 최적화할 수 있어, 복잡한 비용함수나 블랙박스 시뮬레이터에도 적용 가능하다. 새로운 소스 패턴 표현 방법과 함께 엄밀한 시뮬레이션 모델 기반 DFO 방법을 개발한다.

## 주요 기여
- 광학 리소그래피 소스 최적화에 DFO 방법 최초 적용
- 닫힌 형태 그래디언트 없이 소스 최적화 가능한 일반적 프레임워크 제시
- 복잡한 비용함수 및 블랙박스 시뮬레이터에도 적용 가능
- 새로운 소스 파라미터 표현 방법 개발

## 알고리즘/수식
**DFO 기반 소스 최적화:**
$$\min_{\boldsymbol{\theta}} F(\boldsymbol{\sigma}(\boldsymbol{\theta}))$$
소스 파라미터 $\boldsymbol{\theta}$에 대한 그래디언트 계산 없이 직접 최적화.

**소스 패턴 파라미터화:**
소스를 제어 파라미터 $\boldsymbol{\theta}$로 표현:
$$\sigma(f,g) = \mathcal{T}(\boldsymbol{\theta}; f,g)$$
변환 함수 $\mathcal{T}$로 조명 분포를 유연하게 파라미터화.

**DFO 방법 (모델 기반 DFO):**
모델 함수 $m_k(\boldsymbol{\theta})$로 $F$ 근사:
$$m_k(\boldsymbol{\theta}) \approx F(\boldsymbol{\theta}), \quad \|\boldsymbol{\theta} - \boldsymbol{\theta}_k\| \leq \Delta_k$$
신뢰 영역(trust region) 반경 $\Delta_k$ 내에서 모델 최적화.

**신뢰 영역 업데이트:**
$$\boldsymbol{\theta}_{k+1} = \arg\min_{\|\boldsymbol{\theta} - \boldsymbol{\theta}_k\| \leq \Delta_k} m_k(\boldsymbol{\theta})$$

**모델 평가 (함수값만 사용):**
그래디언트 없이 샘플 점 $\{\boldsymbol{\theta}_i\}$의 함수값 $\{F(\boldsymbol{\theta}_i)\}$만으로 모델 구성.

**비용함수 (일반형):**
$$F = \sum_j \left(I(x_j; \boldsymbol{\theta}) - I_{target}(x_j)\right)^2$$

## OPC 툴 SMO 구현 관련성
- SKOPC 소스 최적화에서 그래디언트 미지원 비용함수나 외부 시뮬레이터 사용 시 참고
- `skopc/smo/dfo_source_opt.py` 구현으로 블랙박스 리소그래피 모델과 소스 최적화 연동
- 복잡한 EUV 마스크 모델(두꺼운 마스크, M3D 효과) 포함 SMO에 DFO 적용 방안 참고
- Zernike 소스 파라미터화와 DFO 결합으로 변수 감소 + 그래디언트 불필요 전략 가능

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Wu et al., "Zernike source representation SMO," Optics Express 2014
- Chen et al., "CMA-ES SMO," Optics Express 2020

## 태그
`SMO`, `JOSAA`, `derivative-free-optimization`, `DFO`, `source-optimization`, `gradient-free`, `trust-region`, `black-box-optimization`, `illumination-source`, `general-framework`
