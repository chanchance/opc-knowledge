# Introducing Etch Kernels for Efficient Pattern Sampling and Etch Bias Prediction

## 메타데이터
- **저자**: Lafferty, N. et al. (Mentor Graphics / Siemens EDA)
- **연도**: 2018
- **게재지**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 17, No. 1
- **DOI/URL**: https://doi.org/10.1117/1.JMM.17.1.013505
- **인용수**: ~35

## 핵심 요약
에칭 편향(etch bias) 예측을 위한 기하학적 커널(etch kernels) 기반 컴팩트 에칭 모델을 제안한다. 에칭 커널의 정의와 캘리브레이션 패턴 선택이 모델의 견고성(robustness)에 결정적임을 분석한다. OPC 플로우 내 에칭 모델 통합을 위한 효율적인 패턴 샘플링 방법론을 함께 제시한다.

## 주요 기여
1. 에칭 편향 예측을 위한 기하학적 etch kernel 개념 정립
2. 최적 캘리브레이션 패턴 선택 방법론 (커널 공간 커버리지 기반)
3. 컴팩트 에칭 모델의 견고성 분석: 어떤 조건에서 실패하는가
4. OPC 플로우 통합: 리소 OPC 후 에칭 보정 단계로 추가
5. 실제 DUV 공정 데이터로 모델 검증

## 모델 수식/아키텍처

**에칭 편향 모델:**
```
etch_bias(segment) = Σ_k c_k · K_k(geometry_context)
```
K_k = k번째 에칭 커널 (기하학적 컨텍스트 특성 함수)
c_k = 캘리브레이션 계수

**기하학적 에칭 커널 예시:**
```
K_density(r) = ∫∫_{||x||<r} pattern_density(x',y') w(x-x',y-y') dx'dy'
```
w = 가중함수 (균일 또는 가우시안)
r = 커널 반경 (수십~수백 nm)

**2D 에칭 편향 (주변 영역 의존):**
```
etch_bias(x) = f(CD_resist(x), density_r1(x), density_r2(x), ...,
                  pitch(x), orientation(x), aspect_ratio(x))
```
density_ri: 반경 ri 이내 패턴 밀도

**캘리브레이션 절차:**
```
1. 다양한 geometry_context 패턴 노광 및 에칭
2. 리소 후 CD + 에칭 후 CD 동시 측정
3. etch_bias = CD_etch - CD_litho 계산
4. 최소자승 피팅: min_{c} ||etch_bias_meas - Σ_k c_k K_k||²
```

**모델 정확도 평가:**
```
RMS_etch = sqrt(mean((etch_bias_sim - etch_bias_meas)²))
목표: RMS_etch < 0.5nm (28nm 노드 이하)
```

## 모델 유형
- [ ] 광학 모델
- [ ] 레지스트 모델
- [ ] ML/DL
- [x] 하이브리드 (기하학적 커널 기반 컴팩트 에칭 모델)

## OPC 툴 구현 관련성
- skopc/modeling/etch_model.py: etch kernel 기반 컴팩트 에칭 모델 구현
- OPC 플로우: 리소 OPC 수렴 → 에칭 보정(etch retargeting) → 재검증
- 에칭 커널 계산: 픽셀 기반 밀도 맵 컨볼루션으로 구현
- 캘리브레이션 패턴: 1D(다양한 pitch/CD) + 2D(코너, T자, dense/isolated) 포함
- Siemens Calibre의 기본 에칭 모델 접근법

## 참고문헌
- Sato, T. et al., "OPC accuracy improvement with deep-learning etch model" (2022)
- Sturtevant, J. et al., "Roadmap to sub-nanometer OPC model accuracy" (2012)
- Mentor Graphics etch model documentation

## 태그
`Model`, `SPIE-JMM`, `EtchModel`, `EtchKernel`, `EtchBias`, `CompactModel`, `OPC`, `Calibration`, `2018`
