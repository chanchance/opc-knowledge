# Towards Efficient and Accurate Cost Functions for EUVL Stochastic-Aware OPC Correction and Verification

## 메타데이터
- **저자**: Shuling Wang, Azat Latypov, Shumay Shang, Germain Fenger, Chih-I Wei, Xima Zhang
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 1295319
- **DOI/URL**: https://doi.org/10.1117/12.3010912
- **인용수**: 신규 논문 (Siemens EDA, SPIE Advanced Lithography 2024)

## 핵심 요약
EUV 스토캐스틱 변동을 정량화하는 기존 접근법(이미지 지표, PVB 파라미터 등)이 스토캐스틱 OPC 보정·검증 알고리즘에서 비아(via) 결함 확률을 정확하게 예측할 수 있는지를 Calibre 스토캐스틱 모델의 정밀 결함 확률 계산과 비교·검증한다. NILS 등 단순 이미지 지표나 PVB 파라미터가 다양한 레이아웃에 걸쳐 결함 확률을 정확히 예측할 수 있는지를 평가하며, Calibre 스토캐스틱 모델의 결함 확률 예측을 Brute-Force Monte Carlo로 검증한다.

## 주요 기여
1. NILS·PVB 기반 단순 비용 함수와 정밀 결함 확률 기반 비용 함수의 체계적 비교 — EUV OPC 검증 정확도 평가
2. Calibre 스토캐스틱 모델 결함 확률 예측의 Brute-Force Monte Carlo 검증
3. 스토캐스틱-aware OPC 보정·검증에 적합한 효율적이고 정확한 비용 함수 지침 도출
4. 현대 IC 비아 레이어에 전형적인 다양한 레이아웃에서의 비교 실증

## 검증 방법론
- **비용 함수 비교 평가**:
  1. 이미지 지표 기반: NILS(Normalized Image Log Slope), 최소 이미지 강도(Min Intensity)
  2. PVB(Process Variation Band) 파라미터: PVB 폭, PVB 내 최소 마진
  3. 스토캐스틱 결함 확률: Calibre 스토캐스틱 모델로 계산한 비아 개방/브리지 확률
- **Monte Carlo 검증**: 수천 회 리소그래피 시뮬레이션 반복으로 결함 확률 기준값(ground truth) 생성
- **Calibre 스토캐스틱 모델**: Siemens EDA의 컴팩트 스토캐스틱 리소그래피 모델 (EUV 광자 통계 + 레지스트 화학 변동 포함)
- **대상 패턴**: 현대 IC 비아 레이어 전형적 레이아웃 다수 (다양한 CD, 피치, 주변 패턴)

## 검증 지표
- EPE 허용 범위: 비아 결함 확률 기준 (< 10⁻⁴/비아 또는 공정 노드별 목표값)
- 시뮬레이터: Calibre 스토캐스틱 모델 + Brute-Force Monte Carlo
- 커버리지: 현대 IC 비아 레이어 다양한 레이아웃 패턴

## OPC 툴 구현 관련성
- **EUV 스토캐스틱 OPC 검증 비용 함수 설계의 핵심 참조**: `VerificationEngine`에서 EUV 스토캐스틱 검증 시 NILS/PVB 기반 간이 체크와 결함 확률 기반 정밀 체크를 언제 적용할지 결정하는 알고리즘 설계에 직접 활용
- 스토캐스틱 OPC 검증 비용 함수로 결함 확률을 직접 사용하는 구현의 이론적·실증적 근거
- Brute-Force Monte Carlo 검증 방법론은 OPC 검증 툴의 스토캐스틱 모델 정확도 벤치마크 프레임워크로 활용 가능
- EUV OPC 검증에서 간이 지표(NILS, PVB)와 정밀 스토캐스틱 시뮬레이션의 트레이드오프 분석 근거

## 참고문헌
- SPIE Optical and EUV Nanolithography XXXVII 2024, Vol. 12953
- 관련: OPC strategies to reduce failure rates with rigorous stochastic simulations in EUVL (SPIE 2019)
- Siemens Calibre 스토캐스틱 모델 관련 연구

## 태그
`Verification`, `SPIE`, `EUV`, `Stochastic`, `OPCVerification`, `CostFunction`, `FailureProbability`, `MonteCarlo`, `NILS`, `PVB`, `Calibre`, `ViaDefect`
