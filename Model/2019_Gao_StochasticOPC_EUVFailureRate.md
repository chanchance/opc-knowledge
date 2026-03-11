# OPC Strategies to Reduce Failure Rates with Rigorous Resist Model Stochastic Simulations in EUVL

## 메타데이터
- **저자**: Gao, W. et al. (imec / ASML / KLA)
- **연도**: 2019
- **게재지**: Proc. SPIE 10957, Extreme Ultraviolet (EUV) Lithography X
- **DOI/URL**: https://doi.org/10.1117/12.2515124
- **인용수**: ~55

## 핵심 요약
5nm 기술 노드에서 다크필드(darkfield) SRAM 셀을 대상으로 EUV 확률론적 인쇄 실패율(stochastic printing failure rate)에 다양한 OPC 전략과 레지스트 특성이 미치는 영향을 리고러스 레지스트 모델 기반 확률론적 시뮬레이션으로 분석한다. OPC 바이어스 증가, 서브레졸루션 보조 피처(SRAF) 추가, 레지스트 블러(blur) 최소화 등의 전략이 실패율 저감에 미치는 효과를 정량화한다.

## 주요 기여
1. 확률론적 OPC 전략(바이어스, SRAF, 레지스트 파라미터) 실패율 저감 효과 정량 비교
2. 5nm SRAM 다크필드 비아 레이어의 EUV 확률론적 시뮬레이션 최초 전체 셀 분석
3. 레지스트 블러 크기(blur size)와 실패율의 비선형 관계 규명
4. 광자 샷 노이즈 vs. 레지스트 내재 확률론적 효과의 기여도 분리
5. 확률론적 인식(stochastic-aware) OPC 보정 방향성 제시

## 모델 수식/아키텍처

**EUV 확률론적 리소그래피 모델:**
```
M̂(x) = ∑_{photons} δ(x - x_absorbed) * G_blur(x; σ_blur)
```
M̂(x) = 흡수된 광자의 공간 분포 (블러 적용)
σ_blur = 레지스트 블러 파라미터 (산 확산 포함)

**현상 확률 (Bernoulli 과정):**
```
P(develop | x) = Φ((M̂(x) - C_th) / σ_local)
```
Φ = 정규 누적분포함수
C_th = 현상 임계값, σ_local = 로컬 임계값 변동

**실패 확률 정의 (NOK metric):**
```
P_fail(pattern) = P(bridge) + P(break)
P_bridge = P(resist remaining in target space)
P_break = P(resist missing in target line)
```

**몬테카를로 실패율 추정:**
```
P_fail ≈ N_fail / N_MC  (N_MC ~ 10⁴~10⁶ 시뮬레이션)
```

**OPC 전략별 실패율 개선:**
```
ΔP_fail(bias) = P_fail(CD_nom) - P_fail(CD_nom + Δbias)
목표: Δbias 최소화하면서 P_fail < P_fail_target
```

**레지스트 블러 최적화:**
```
P_fail ∝ σ_blur^α  (α > 1: 블러에 초선형 의존)
σ_blur_opt = argmin P_fail subject to process_constraints
```

## 모델 유형
- [ ] 광학 모델
- [x] 레지스트 모델 (확률론적 레지스트 모델)
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- EUV OPC 검증에 확률론적 실패 확률(P_fail) 메트릭 통합 필요
- skopc/modeling/stochastic_opc.py: 몬테카를로 + 실패율 계산 구현
- 확률론적 OPC: 결정론적 EPE 최소화 대신 P_fail 최소화 목적함수
- 계산 비용: P_fail 추정에 수천~수만 회 MC 시뮬레이션 필요 → GPU 가속 필수
- SRAF 최적화: 단순 CD 최적화보다 P_fail 기반 최적화가 더 효과적

## 참고문헌
- Gallatin, G.M. et al., "Calibration of stochastic EUV resist model" (2012)
- Gao, P. et al., "Stochastic model for EUV resist" (2012)
- Neureuther, A.R. et al., "EUV OPC modeling requirements" (2014)

## 태그
`Model`, `SPIE`, `EUV`, `StochasticOPC`, `FailureRate`, `SRAM`, `5nm`, `MonteCarlo`, `ResistBlur`, `2019`
