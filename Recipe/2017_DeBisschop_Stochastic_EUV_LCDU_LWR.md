# Stochastic Effects in EUV Lithography: Random, Local CD Variability, and Printing Failures

## 메타데이터
- **저자**: Peter De Bisschop
- **연도**: 2017
- **게재지**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 16, Issue 4, 041013
- **DOI/URL**: https://doi.org/10.1117/1.JMM.16.4.041013
- **인용수**: ~120

## 핵심 요약
EUV 리소그래피에서의 확률론적(stochastic) 효과를 체계적으로 분석한다. 동일한 조건에서 인쇄되어야 할 패턴 사이의 국소적 CD 변동성을 LWR(Line-Width Roughness), LCDU(Local CD Uniformity) 등의 지표로 정량화하며, 인쇄 실패(missing contact, microbridge) 확률을 예측하는 모델을 구축한다. OPC 모델 캘리브레이션 및 검증에서 stochastic 지표를 통합해야 함을 제안하고, stochastic 핫스팟 감지를 위한 OPC 검증 흐름 확장을 제시한다.

## 주요 기여
1. EUV stochastic 효과의 체계적 분류: LWR, LCDU, 인쇄 실패
2. Stochastic 효과 예측 모델 구축 (간단한 예측 지표 포함)
3. OPC 모델 캘리브레이션에 LER/LWR/LCDU 통합 필요성 제시
4. Stochastic 핫스팟을 OPC 검증 흐름에 포함하는 로드맵

## Recipe/Process Flow 상세

### EUV 리소그래피 Stochastic 효과의 물리적 원인
```
EUV 광자 수 제한 (Photon Shot Noise):
  에너지: E_photon = hc/λ = 91.8 eV (13.5nm)
  ArF 대비 EUV 광자 에너지: ~14× 높음
  → 동일 노광 에너지에서 광자 수 ~14× 적음
  → 광자 수 통계 변동(Poisson) 더 큼

레지스트 분자 수 제한:
  소형 피처(< 20nm): 수십~수백 개 레지스트 분자만 관여
  화학 반응 확률 변동 → CD 변동

EUV 마스크 기여:
  다층 반사경 + 흡수체의 거칠기
  → 마스크 CD 변동 → LCDU에 기여
```

### Stochastic 효과 지표 및 측정
```
1. LWR (Line-Width Roughness):
   정의: 3σ of line width variation along line direction
   측정: SEM 이미지에서 라인 에지 추출 후 통계
   목표: 7nm 이하 노드에서 LWR < 1-2nm (3σ)

2. LER (Line-Edge Roughness):
   정의: 3σ of individual edge position variation
   LWR ≈ √2 × LER (uncorrelated 양쪽 에지)

3. LCDU (Local CD Uniformity):
   정의: 3σ of CD within small area (동일 설계 패턴 반복)
   콘택/비아 어레이에서 중요
   EUV에서 LCDU 수 nm: 회로 성능 변동 유발

4. 인쇄 실패 (Stochastic Printing Failures):
   Missing Contact: 콘택 홀이 인쇄 안 됨
   Microbridge: 스페이스에 잔류 레지스트 연결
   실패 확률: P_fail = f(dose, CD, pitch, resist)
```

### OPC 검증에서의 Stochastic 핫스팟 감지
```
기존 OPC 검증 (결정론적):
  명목 조건(best focus, best dose)에서 CD 오차 감지
  → Stochastic 실패 패턴 놓침

Stochastic 인식 OPC 검증:
  1. Stochastic 모델 구축:
     P_fail(x, y) = f(aerial image, resist model)
     간단한 예측 지표: 공정 마진 = CD - CD_min
     복잡한 예측: 몬테카를로 레지스트 시뮬

  2. Stochastic 핫스팟 식별:
     P_fail > P_threshold인 패턴 = stochastic 핫스팟
     P_threshold: 수율 목표로 역산 (예: P_fail < 1e-8 per feature)

  3. OPC 수정:
     Stochastic 핫스팟 → 도즈 마진 확대 OPC
     CD 타겟 조정 (더 많은 광자 확보)
     SRAF 추가 (공정 윈도우 확대)

4단계: OPC 모델 캘리브레이션 확장:
   기존: CD만으로 모델 캘리브레이션
   개선: CD + LWR + LCDU 동시 캘리브레이션
   → 더 현실적인 OPC 예측
```

### EUV Stochastic 효과 감소 전략
```
레지스트 최적화:
  - Metal-oxide resist (고감도, 저 LWR)
  - 광자 흡수율 향상 (광민감 재료)
  - PEB 조건 최적화

공정 최적화:
  - 노광 도즈 증가 (광자 수 증가, LWR 감소)
  - Dose-to-clear 마진 확보
  - 현상(development) 조건 최적화

OPC/ILT 최적화:
  - SRAF로 공정 마진 확대 (도즈 마진 향상)
  - 패턴 배치 최적화 (stochastic 취약 패턴 분리)
  - Stochastic 인식 OPC: 도즈 마진 최대화 목적함수
```

### 주요 결과
```
EUV 공정 (0.33 NA, ArF 도즈 환산):
  LWR (3σ): 약 2-4nm (패턴 의존)
  LCDU (3σ): 약 2-5nm (콘택 패턴)
  인쇄 실패 확률: P_fail ~ 10^(-3) ~ 10^(-6) (도즈 의존)

예측 모델 정확도:
  Stochastic 핫스팟 예측: 실제 실패 패턴과 높은 상관관계
  OPC 검증 통합 가능성 확인
```

## OPC 툴 구현 관련성
- **SKOPC Stochastic OPC**: `skopc/pwo/` 공정 윈도우 최적화에 stochastic 핫스팟 감지 기능 추가
- **LCDU 모델**: `skopc/modeling/` 레지스트 모델에 간단한 LCDU 예측 지표 추가
- **도즈 마진 OPC**: EPE 최소화 외에 도즈 마진 최대화를 추가 목적함수로 설정
- **EUV 레시피**: `recipes/example_euv.yaml`에 stochastic_aware_opc 파라미터 추가

## 참고문헌
- J. Micro/Nanolith. MEMS MOEMS 16(4), 041013 (2017)
- 저자 소속: imec (Leuven, Belgium)
- 관련: Stochastic printing failures in EUV lithography (JMM 17(4), 2018)
- 관련: Stochastics in EUV: role of microscopic resist properties (JMM 17(4), 2018)
- 관련: Contribution of EUV mask CD variability on LCDU (SPIE 10143, 2017)

## 태그
`Recipe`, `SPIE`, `JM3`, `EUVLithography`, `Stochastic`, `LWR`, `LER`, `LCDU`, `PrintingFailure`, `OPC-Verification`, `StochasticHotspot`, `imec`, `2017`
