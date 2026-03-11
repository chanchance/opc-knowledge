# Advanced Simulations Using an Improved Metal Oxide Photoresist Model

## 메타데이터
- **저자**: Craig D. Needham, Ulrich Welling, Amrit Narasimhan, Peter De Schepper, Lauren McQuade, Michael Kocsis, Lawrence S. Melvin III, Jason Stowers, Stephen T. Meyers
- **연도**: 2024
- **게재지**: Proc. SPIE 12957, Advances in Patterning Materials and Processes XLI, 129571B
- **DOI/URL**: https://doi.org/10.1117/12.3010941

## 핵심 요약
EUV 리소그래피용 스핀-온 금속산화물(MOx) 레지스트의 화학적·재료적 공정을 기반으로 한 엄밀(rigorous) 확률론적 리소그래피 모델을 개발한다. 다양한 계측 기법의 실험 데이터를 이용하여 모델 방정식의 기본 파라미터를 정의하고, CD-SEM 및 개방 프레임 노광 데이터셋으로 캘리브레이션한다. 향상된 MOx 레지스트 모델로 패터닝 성능 시뮬레이션 정확도를 크게 향상시킨다.

## 주요 기여
1. **MOx 레지스트 엄밀 스토케스틱 모델**: 금속산화물 레지스트의 화학/재료 공정 기반 물리 모델 개발
2. **실험 데이터 기반 파라미터화**: CD-SEM, 개방 프레임 노광 등 다양한 계측 데이터로 모델 파라미터 캘리브레이션
3. **향상된 시뮬레이션 정확도**: 이전 MOx 모델 대비 리소그래피 성능 예측 정확도 향상
4. **High-NA EUV 적용 준비**: High-NA EUV 환경에서의 MOx 레지스트 패터닝 시뮬레이션 역량 확보
5. **OPC 적용 MOx 모델**: OPC 플로우에서 활용 가능한 실용적 MOx 레지스트 컴팩트 모델

## Recipe/Flow 상세
- **MOx 레지스트 시뮬레이션 모델 개발 플로우**:
  1. **MOx 레지스트 물리/화학 메커니즘 분석**:
     - 높은 EUV 흡수율: 금속(Sn, Hf, Zr 등) 원자의 높은 흡수 단면적
     - 광화학 반응: EUV 광자 흡수 → 금속-탄소 결합 분해
     - 현상 메커니즘: 노광 영역 용해도 변화 (현상액 기반 또는 건식)
     - 낮은 확산: 작은 분자 크기로 확산 최소화 → LWR 개선
  2. **모델 파라미터 정의**:
     - 흡수 계수: 파장별 MOx 흡수율
     - 반응 동역학: 광화학 반응 속도 및 활성화 에너지
     - 공간 분포 함수: 2차 전자 발생 및 확산 거리
     - 현상 모델: 노광량 의존 용해 속도
  3. **실험 데이터 캘리브레이션**:
     - CD-SEM: 다양한 피치/CD 패턴에서 CD 측정
     - 개방 프레임 노광: 용해 곡선(dissolution curve) 캘리브레이션
     - LER/LWR 측정: stochastic 파라미터 캘리브레이션
     - 최적화로 모델 파라미터 피팅
  4. **시뮬레이션 검증**:
     - 캘리브레이션 데이터와 독립적인 검증 패턴에서 예측 정확도 확인
     - 공정 창(DOF/EL) 예측과 실험 비교
     - Stochastic 결함률 예측 검증
  5. **OPC 플로우 통합**:
     - MOx 레지스트 컴팩트 모델 → OPC 시뮬레이션 엔진 통합
     - full-chip OPC 적용 가능한 효율적 MOx 컴팩트 모델
- **MOx 레지스트 OPC 특수 고려사항**:
  - 높은 흡수율 → 낮은 광자 수로 충분한 노광 가능 → 더 낮은 stochastic 변동
  - 낮은 확산 → 기존 CAR 대비 더 sharp한 임계값 의존성
  - 건식 또는 습식 현상 옵션에 따른 모델 차이
- **소속 기관**: Inpria Corporation (미국) - MOx 레지스트 선도 기업

## OPC 툴 구현 관련성
- SKOPC 레지스트 모델에 MOx 옵션 추가 (기존 CAR 모델 외)
- `mox_resist_model.py`: Inpria MOx 레지스트 컴팩트 모델 구현
- EUV OPC 시뮬레이션에서 MOx 레지스트 물리 파라미터 반영
- High-NA EUV MOx 패터닝 OPC 레시피 설계 기준

## 태그
`MetalOxideResist`, `MOx`, `EUV`, `OPC`, `ResistModel`, `Simulation`, `Stochastic`, `HighNA`, `Inpria`, `Calibration`, `SPIE`, `2024`
