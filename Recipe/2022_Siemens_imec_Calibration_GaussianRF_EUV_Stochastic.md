# Calibration of Gaussian Random-Field Stochastic EUV Models

## 메타데이터
- **저자**: Siemens Digital Industries Software / imec 연구진 (Germain Fenger, John Sturtevant, Werner Gillijns, et al.)
- **연도**: 2022
- **게재지**: Proc. SPIE 12051, Optical and EUV Nanolithography XXXV
- **DOI/URL**: https://doi.org/10.1117/12.2614xxx (SPIE 12051)

## 핵심 요약
EUV 리소그래피 stochastic 거동을 모델링하는 가우시안 랜덤 필드(Gaussian Random Field, GRF) 모델의 캘리브레이션 방법을 개발한다. 실험적으로 측정된 리소그래피 피처의 에지(LER, LWR, PSD)를 이용하여 GRF 모델 파라미터를 캘리브레이션하고, 이를 Siemens Calibre 플랫폼의 stochastic-aware OPC 플로우에 적용한다. 이 연구는 2023년 SPIE "Compact modeling of stochastics and application in OPC" 및 2025년 웨이퍼 수준 검증 논문으로 이어지는 일련의 연구 중 핵심 선행 연구이다.

## 주요 기여
1. **GRF 스토케스틱 EUV 모델 캘리브레이션**: 가우시안 랜덤 필드 모델 파라미터를 실험 데이터로 캘리브레이션하는 방법론 확립
2. **LER/LWR/PSD 기반 캘리브레이션**: 라인 에지 거칠기(LER), 라인 폭 거칠기(LWR), 파워 스펙트럼 밀도(PSD)를 캘리브레이션 데이터로 활용
3. **Calibre 플랫폼 통합**: 캘리브레이션된 GRF 모델을 Siemens Calibre OPC 플로우에 통합
4. **첫 세대 stochastic OPC 모델**: 이후 stochastic-aware OPC 시리즈 연구의 기반 모델 확립
5. **EUV 실험 데이터 검증**: imec의 실제 EUV 웨이퍼 데이터로 GRF 모델 예측 정확도 검증

## Recipe/Flow 상세
- **GRF EUV 스토케스틱 모델 캘리브레이션 플로우**:
  1. **EUV 실험 데이터 수집**:
     - 다양한 EUV 노광 조건(dose, focus)에서 리소그래피 패턴 SEM 측정
     - LER(Line Edge Roughness): 에지 위치 변동의 표준편차
     - LWR(Line Width Roughness): 선폭 변동의 표준편차
     - PSD(Power Spectral Density): LER/LWR의 주파수 특성
  2. **GRF 모델 파라미터 정의**:
     - 공간 상관 길이(correlation length): stochastic 변동의 상관 거리
     - 분산(variance): stochastic 노이즈 강도
     - 스펙트럼 형태(spectral shape): PSD 곡선 형태 파라미터
  3. **캘리브레이션 최적화**:
     - GRF 모델 파라미터 → 시뮬레이션 LER/LWR/PSD 생성
     - 측정 데이터와 시뮬레이션 비교: 오차 최소화
     - 최적 GRF 파라미터 추출
  4. **모델 검증**:
     - 캘리브레이션에 사용되지 않은 패턴에서 모델 예측 검증
     - 다양한 피치 및 CD에서 stochastic 거동 예측 정확도 확인
  5. **Calibre OPC 통합**:
     - 캘리브레이션된 GRF 모델을 Calibre stochastic OPC 모듈에 적용
     - Stochastic 결함 확률 예측 및 OPC 보정에 활용
- **GRF 모델 물리적 근거**:
  - EUV 광자 통계: 포아송 분포에 따른 광자 수 변동
  - 레지스트 화학 반응의 확률적 특성: 산-광산 반응 공간 분포 변동
  - GRF로 통계적 특성을 컴팩트하게 표현
- **연구 시리즈**: GRF 캘리브레이션(2022) → Compact OPC 적용(2023) → 웨이퍼 검증(2025)

## OPC 툴 구현 관련성
- SKOPC EUV 레지스트 모델에 GRF stochastic 모델 통합
- `grf_stochastic_model.py`: LER/LWR/PSD 기반 GRF 파라미터 캘리브레이션
- Stochastic-aware OPC에서 GRF 모델로 결함 확률 예측
- EUV via/컨택 레이어에서 stochastic 결함 최소화 OPC 전략 기반

## 태그
`EUV`, `Stochastic`, `GaussianRandomField`, `OPC`, `Calibration`, `LER`, `LWR`, `PSD`, `Calibre`, `Siemens`, `imec`, `SPIE`, `2022`
