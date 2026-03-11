# Compact Modeling of Stochastics and Application in OPC

## 메타데이터
- **저자**: Werner Gillijns, Jae-uk Lee, Ryan Ryoung Han Kim, Chih-I Wei, Xima Zhang, Azat Latypov, Germain Fenger, John Sturtevant
- **연도**: 2023
- **게재지**: Proc. SPIE 12494, Optical and EUV Nanolithography XXXVI, 124940J
- **DOI/URL**: https://doi.org/10.1117/12.2658260
- **인용수**: ~20

## 핵심 요약
EUV 리소그래피의 확률론적 효과를 OPC 루프에 직접 통합하기 위한 컴팩트 확률론적 모델(compact stochastic model)을 제안하고 적용한다. 리고러스 Monte Carlo 시뮬의 높은 계산 비용 문제를 해결하기 위해 확률론적 핫스팟 예측에 특화된 빠른 컴팩트 모델을 구축하며, 이를 OPC에 적용하여 확률론적 실패율을 크게 줄인다. 확률론적 인식 OPC(ST-OPC)가 SRAM과 로직 설계 모두에서 EPE를 약간 희생하는 대신 확률론적 결함 확률을 최소 1자릿수(10×) 이상 줄임을 실증한다.

## 주요 기여
1. OPC 적용 가능한 빠른 컴팩트 확률론적 EUV 모델
2. ST-OPC (Stochastic-aware OPC): 확률론적 실패율 직접 최소화
3. SRAM + 로직 설계에서 확률론적 결함 10× 이상 감소 실증
4. 확률론적 핫스팟 스크리닝을 OPC-검증 흐름에 통합하는 경로 제시

## Recipe/Process Flow 상세

### 컴팩트 확률론적 모델의 필요성
```
리고러스 Monte Carlo 확률론적 시뮬:
  방법: 수천~수백만 번 전체 리소그래피 시뮬
  정확도: 높음 (ppm 수준 실패율 정량화)
  단점: 매우 느림 → OPC 루프에 적용 불가
    (클립당: 수 시간 이상)

OPC 루프 요구사항:
  클립당: ~ms 수준 목적함수 평가
  수렴까지: 수십~수백 이터레이션
  → 리고러스 시뮬: OPC에 직접 사용 불가

컴팩트 확률론적 모델:
  리고러스 시뮬 결과로 훈련/보정
  OPC 루프에서 빠른 확률론적 리스크 평가 가능
  정확도/속도 균형: OPC 루프에서 실용적
```

### 컴팩트 확률론적 모델링
```
EUV 확률론적 효과 분해:
  1. 광자 샷 노이즈:
     항공 이미지 I(x) → 포아송 분포 I_stoch(x) ~ Poisson(I(x)/σ²_shot)
     σ²_shot = I(x) × F_Fano / (η_DQE × dose)
     F_Fano: 팬오 인자 (EUV 광자 → 이차 전자 변환)
     η_DQE: 레지스트 DQE (Detector Quantum Efficiency)

  2. 레지스트 확률론적 효과:
     화학 증폭: 광산 (PAG) 생성 → 반응-확산
     컴팩트 모델: Gaussian 흐림 + 확률론적 임계값
     I_chem(x) = G_σ * I_stoch(x) + N(0, σ²_chem)

  3. 패터닝 실패 확률:
     P_fail(M) = P(브리지 or 단선 | M, process)
     = f(항공 이미지 최솟값/최댓값, 기울기, 공정 변동)

컴팩트 모델 형태:
  P_fail ≈ Q(-ILS × (I_min - I_th) / σ_total)
  ILS: Image Log Slope
  σ_total: 총 확률론적 변동 (샷 + 레지스트)
  → 빠른 해석적 계산 가능
```

### ST-OPC (확률론적 인식 OPC)
```
기존 OPC 목적함수:
  L_OPC = Σ (CD_sim - CD_target)²  (EPE 최소화)
  한계: EPE 작아도 확률론적 실패율 높을 수 있음

ST-OPC 목적함수:
  L_ST-OPC = L_EPE + λ_stoch × L_stoch(M)
  L_stoch(M) = Σ_hotspot P_fail(M, location)
  → 확률론적 실패율 직접 최소화

ST-OPC 흐름:
  표준 MB-OPC 수렴 → ST-OPC 추가 최적화
  변경: EPE 약간 희생 → P_fail 크게 감소
  목적함수 균형: λ_stoch로 EPE vs. P_fail 조절

적용 패턴:
  확률론적 핫스팟 식별 → 해당 위치 집중 최적화
  SRAM 비트셀: 가장 취약한 컨택/비아 위치
  로직: 좁은 공간 (브리지 위험) 위치
```

### 성능 결과
```
확률론적 결함 감소 (ST-OPC vs. 표준 OPC):
  SRAM 설계: 1자릿수 이상 (10×) 감소
  로직 설계: 1자릿수 이상 (10×) 감소
  최신 Siemens-imec 협력 결과 (2025): 수 자릿수 감소 달성

EPE 변화:
  ST-OPC: 표준 OPC 대비 약간 EPE 증가
  균형: 실패율 10× 감소 vs. EPE ~5% 증가 (수용 가능)

OPC 속도:
  컴팩트 모델: OPC 루프에서 실용적 속도
  리고러스 시뮬 대비: 수백~수천 배 빠름
```

## OPC 툴 구현 관련성
- **SKOPC ST-OPC**: `skopc/modeling/litho_engine.py`에 컴팩트 확률론적 모델 통합
- **P_fail 목적함수**: OPC 최적화에 확률론적 실패 손실 L_stoch 추가
- **확률론적 핫스팟**: OPC-검증 후 확률론적 핫스팟 스크리닝 단계 추가
- **EUV 레지스트 모델**: CAR/MOR 레지스트 확률론적 파라미터 지원

## 참고문헌
- Proc. SPIE 12494, Optical and EUV Nanolithography XXXVI (April 2023)
- 저자 소속: imec + Siemens EDA + ASML
- 관련: Compact modeling to predict stochastic hotspots in EUVL (SPIE 11323, 2020)
- 관련: OPC strategies to reduce failure rates - Vaglio Pret (SPIE 10957, 2019)
- 관련: Stochastic effects in EUV - DeBisschop (JMM 2017)

## 태그
`Recipe`, `SPIE`, `EUV`, `Stochastic`, `OPC`, `CompactModel`, `FailurePrediction`, `ST-OPC`, `Hotspot`, `SRAM`, `Logic`, `imec`, `Siemens`, `2023`
