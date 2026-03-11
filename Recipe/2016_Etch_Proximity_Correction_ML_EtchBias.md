# Etch Proximity Correction Through Machine-Learning-Driven Etch Bias Model

## 메타데이터
- **저자**: (SPIE 9782 - 2016 SPIE Advanced Lithography)
- **연도**: 2016
- **게재지**: Proc. SPIE 9782, Optical Microlithography XXIX
- **DOI/URL**: https://doi.org/10.1117/12.2219038
- **인용수**: ~35

## 핵심 요약
OPC(Optical Proximity Correction) 흐름에 식각(etch) 근접 효과를 통합하는 머신러닝 기반 식각 바이어스(etch bias) 모델을 제안한다. 리소그래피 후 웨이퍼 CD와 식각 후 최종 CD의 차이인 식각 바이어스를 ML로 예측하여 OPC 타겟 설정에 반영함으로써 최종 실리콘 CD 정확도를 개선한다. 식각 근접 보정(EPC)을 OPC와 통합하는 체계적 접근법을 제시한다.

## 주요 기여
1. 식각 바이어스를 ML로 모델링하는 식각 근접 보정(EPC) 방법론
2. 리소그래피 CD와 최종 실리콘 CD 간 식각 근접 효과의 체계적 특성화
3. OPC 타겟 재조정(retargeting)에 EPC 통합
4. 식각 패턴 의존성(pitch, density, CD) 파라미터화

## Recipe/Process Flow 상세

### 식각 근접 효과의 특성
```
OPC 기존 가정:
  리소그래피 후 CD ≈ 최종 실리콘 CD
  → OPC는 리소그래피 단계만 보정

실제 현실:
  식각 바이어스 = 식각 후 CD - 리소그래피 후 CD
  식각 바이어스는 패턴 의존적:
    - CD (선폭)에 따른 미분 식각률
    - Pitch/주변 밀도에 따른 로딩 효과
    - 식각 가스 농도 불균일 (마이크로 로딩)
    - 각이나 형상에 따른 식각 선택성

결과:
  리소그래피 OPC만으로는 최종 CD 목표 달성 불가
  → 식각 바이어스 보상이 필요
```

### ML 기반 식각 바이어스 모델
```
훈련 데이터 수집:
  1. 테스트 패턴 설계 (다양한 CD, pitch, 밀도)
  2. 리소그래피 후 CD 측정 (SEM, OCD 등)
  3. 식각 후 CD 측정 (동일 패턴)
  4. 식각 바이어스 계산: ΔCD_etch = CD_after_etch - CD_after_litho

피처 추출:
  - 로컬 선폭 (local CD)
  - 근접 패턴 밀도 (pattern density, 다양한 반경)
  - 피치 (pitch)
  - 종횡비 (aspect ratio)
  - 공간(space) 크기

ML 모델:
  - 회귀 모델: etch bias = f(CD, pitch, density, ...)
  - 후보: Support Vector Regression, Random Forest, Neural Network
  - 훈련: 최소제곱법 또는 크로스밸리데이션

예측 정확도:
  - 식각 바이어스 RMS 오차 최소화
  - 공정 노드별 모델 재캘리브레이션
```

### OPC에 EPC 통합 흐름
```
표준 OPC 흐름:
  마스크 타겟 → OPC → 리소그래피 시뮬레이션 → EPE 최소화

EPC 통합 OPC 흐름:
  1단계: EPC 타겟 계산
     Silicon target → ML etch model → Litho target
     리소그래피 타겟 = 실리콘 타겟 - 예측 식각 바이어스

  2단계: 수정된 타겟에 OPC 적용
     Litho target → OPC → 마스크 패턴

  3단계: 검증
     마스크 → 리소그래피 시뮬 → +식각 시뮬 → 최종 CD 검증

장점:
  - 최종 실리콘 CD 정확도 향상
  - 공정 통합의 체계적 접근
  - 피처 의존 식각 효과의 정확한 반영
```

### 성능 결과
```
EPC 통합 vs 미통합 비교:
  최종 CD 오차 (EPE): 감소
  특히 고밀도 패턴, 좁은 공간 패턴에서 개선
  리소그래피-식각 통합 시뮬레이션 정확도 향상
```

## OPC 툴 구현 관련성
- **SKOPC 식각 모델 통합**: `skopc/modeling/` OPC 흐름에 식각 근접 효과 보정 레이어 추가 참조
- **ML 식각 바이어스 모델**: scikit-learn 회귀 모델로 구현 후 OPC 타겟 계산 전처리로 활용
- **EPC 타겟 재조정**: OPC 레시피의 타겟 CD를 식각 바이어스 보상 후 설정
- **공정 통합**: 리소그래피 + 식각 2단계 시뮬레이션 파이프라인

## 참고문헌
- Proc. SPIE 9782, Optical Microlithography XXIX (2016)
- 관련: Accurate etch modeling with massive metrology and deep learning (SPIE 11327, 2020)
- 관련: Using machine learning etch models in OPC and ILT correction (SPIE 11614, 2021)
- 관련: OPC accuracy improvement through deep-learning based etch model (SPIE 12056, 2022)

## 태그
`Recipe`, `SPIE`, `EtchModel`, `EtchBias`, `EtchProximityCorrection`, `MachineLearning`, `OPC-Integration`, `EPC`, `ProcessIntegration`, `2016`
