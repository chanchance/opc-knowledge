# Study of EUV Stochastic Defect on Wafer Yield

## 메타데이터
- **저자**: Yi-Pei Tsai, Chieh-Miao Chang, Yi-Han Chang, Apoorva Oak, Darko Trivkovic, Ryoung-Han Kim
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 1295404
- **DOI/URL**: https://doi.org/10.1117/12.3010858
- **인용수**: 신규 논문 (SPIE Advanced Lithography 2024)

## 핵심 요약
반도체 업계가 EUV 리소그래피로 전환함에 따라 EUV 스토캐스틱 결함이 칩 수율 저하에 중요한 역할을 한다. 기존 수율 모델은 EUV 리소그래피에서 피치와 CD(Critical Dimension)에 따라 변하는 스토캐스틱 기인 결함을 고려하지 않는다. 본 논문은 웨이퍼 데이터에서 교정된 스토캐스틱 결함을 이용하여 EUV 스토캐스틱을 수율 모델링에 통합하는 새로운 접근법을 제시하고, CD 재타겟팅(retargeting) 등 수율 향상 전략을 제안한다.

## 주요 기여
1. EUV 스토캐스틱 결함을 수율 모델링에 통합하는 새로운 프레임워크 — 기존 수율 모델의 공백 해소
2. 웨이퍼 실측 데이터 기반 스토캐스틱 결함 교정 방법론
3. 다양한 EUV 삽입 시나리오에 따른 수율 비교 분석
4. CD 재타겟팅을 통한 EUV 리소그래피 수율 향상 전략 제시

## 검증 방법론
- **EUV 스토캐스틱 결함 유형**:
  - 비아 개방(Via open): 레지스트가 필요한 위치에 없음
  - 브리지(Bridge): 레지스트가 없어야 할 위치에 존재
  - 핀치(Pinch)/브레이크(Break): 라인 폭 변동에 의한 단선
- **웨이퍼 교정 방법**: 실측 웨이퍼 결함 밀도 데이터로 스토캐스틱 모델 파라미터 교정
- **수율 모델 통합**: 교정된 스토캐스틱 결함 확률 분포를 Poisson 수율 모델에 통합
  - `Yield = exp(-D₀ × A_chip)` → 스토캐스틱 결함 밀도 D₀ 항 갱신
- **CD 재타겟팅 최적화**: 스토캐스틱 결함 확률 최소화를 위한 최적 CD 타겟 탐색
- **EUV 삽입 시나리오 비교**: 노광 조건(도스, 포커스), 레지스트, CD 타겟 조합별 수율 예측

## 검증 지표
- EPE 허용 범위: 스토캐스틱 결함 확률 < 목표 수율 달성 기준 (ppm 수준)
- 시뮬레이터: 교정된 스토캐스틱 모델 + 수율 예측 모델
- 커버리지: 다양한 피치·CD 조합의 EUV 레이어 (비아, 메탈 라인)

## OPC 툴 구현 관련성
- **EUV OPC 검증에서 스토캐스틱 수율 예측 통합**: `VerificationEngine` 출력의 스토캐스틱 결함 확률 결과를 수율 예측 모듈과 연계하는 아키텍처 설계에 직접 참조
- CD 재타겟팅 전략은 OPC 타겟 CD 설정 알고리즘에 스토캐스틱 결함 최소화 목적 함수를 추가하는 구현 근거
- 웨이퍼 측정 기반 스토캐스틱 모델 교정 방법론 — OPC 모델 교정(calibration) 파이프라인 확장에 활용
- ppm 수준 스토캐스틱 결함 관리를 위한 OPC 검증 허용 기준 설정의 실무 근거

## 참고문헌
- SPIE DTCO and Computational Patterning III 2024, Vol. 12954
- EUV 스토캐스틱 결함 모니터링 관련 연구 (Sah et al., SPIE 2018)
- EUV 인쇄 실패 관련 연구 (Stochastic printing failures in EUV, SPIE 2019)

## 태그
`Verification`, `SPIE`, `EUV`, `Stochastic`, `YieldModeling`, `StochasticDefect`, `CDRetargeting`, `ViaOpen`, `Bridge`, `WaferData`, `PoissonYield`
