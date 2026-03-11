# Implementing Machine Learning for OPC Retargeting

## 메타데이터
- **저자**: Kevin Hooker, Marco Guajardo, Nai-Chia Cheng, Guangming Xiao
- **연도**: 2020
- **게재지**: Proc. SPIE 11328, Design-Process-Technology Co-optimization for Manufacturability XIV
- **DOI/URL**: https://doi.org/10.1117/12.2552402
- **인용수**: ~20

## 핵심 요약
OPC 실행 전 리소그래피 한계와 식각 효과를 보상하기 위해 설계 타겟을 재조정(retargeting)하는 과정에 ML을 적용하는 방법론을 제시한다. Retargeting은 OPC의 목표 CD를 설계 의도에서 벗어나 리소그래피 + 식각의 조합 효과를 미리 보상하는 단계이다. ML로 retargeting 오프셋을 예측함으로써 기존 수작업/규칙 기반 retargeting 대비 정확도와 효율성을 향상시킨다.

## 주요 기여
1. OPC retargeting에 ML을 최초 적용하여 자동화 및 정확도 향상
2. 리소그래피 + 식각 통합 효과의 패턴 의존적 retargeting 예측
3. ML retargeting + 표준 OPC 결합 흐름의 최종 CD 정확도 개선
4. 수작업 규칙 기반 retargeting 대체 가능성 실증

## Recipe/Process Flow 상세

### OPC Retargeting의 정의와 역할
```
표준 설계 → OPC 흐름:
  설계 CD (design intent) = Silicon 목표 CD
  → OPC로 리소그래피 보정

OPC Retargeting이 필요한 이유:
  1. 리소그래피 한계:
     특정 패턴에서 설계 CD 그대로 인쇄 불가
     (예: 매우 좁은 라인-공간 비율)
  2. 식각 효과:
     리소그래피 후 CD ≠ 최종 실리콘 CD
  3. 공정 편향(Process Bias):
     체계적 CD 오프셋 (공정 노드 의존)

Retargeting의 역할:
  설계 CD → [Retargeting] → OPC 타겟 CD
  OPC 타겟 CD ≠ 설계 CD
  (리소그래피 + 식각 보상이 선반영됨)
```

### ML Retargeting 방법론
```
입력 피처 (패턴별):
  - 로컬 CD (선폭, 공간 폭)
  - 피치
  - 주변 패턴 밀도
  - 2D 기하 특성
  - 레이어 유형

출력:
  Retargeting 오프셋 ΔCD_retarget (nm)
  OPC 타겟 = 설계 CD + ΔCD_retarget

ML 모델:
  Random Forest, Gradient Boosting 또는 Neural Network
  훈련 데이터: 기존 수작업 retargeting 결과 또는
               리소그래피+식각 시뮬레이션으로 역산

훈련 데이터 수집:
  방법 1: 기존 공정 경험치 retargeting 값 학습
  방법 2: (설계 CD, 최종 웨이퍼 CD) 측정 쌍에서
          최적 retargeting 값 역산
```

### ML Retargeting + OPC 통합 흐름
```
단계 1: ML Retargeting
  설계 레이아웃 → ML 모델 → ΔCD_retarget 예측
  OPC 타겟 = 설계 CD + ΔCD_retarget

단계 2: 표준 OPC
  OPC 타겟 → MB-OPC → 마스크 패턴
  OPC 모델: 리소그래피 컴팩트 모델

단계 3: 검증
  마스크 → 리소그래피 시뮬 → CD_litho
  CD_litho → 식각 모델 → CD_final
  CD_final vs. 설계 CD → 최종 EPE

장점:
  ML retargeting: 빠름 (추론 ms 수준)
  패턴 의존적 retargeting: 균일 오프셋보다 정확
  식각 효과 통합: 최종 CD 정확도 향상
```

### 수작업 대비 ML Retargeting
```
수작업/규칙 기반 Retargeting:
  방법: 엔지니어가 공정 경험으로 패턴별 오프셋 결정
  장점: 직관적, 검증된 경험치
  단점: 시간 소모, 일관성 부족, 신규 노드 적용 어려움

ML Retargeting:
  방법: 데이터 기반 예측
  장점: 자동화, 일관성, 빠른 신규 노드 적응
  단점: 충분한 훈련 데이터 필요

결합 접근:
  수작업 retargeting 결과 → ML 훈련 데이터
  ML이 수작업 패턴 학습 → 전체 칩에 자동 적용
  → 수작업 전문 지식의 확장 및 자동화
```

### 성능 결과
```
최종 CD 정확도 (설계 CD 대비):
  수작업 Retargeting + OPC: 기준
  ML Retargeting + OPC: 동등하거나 개선

특히 개선 효과가 큰 패턴:
  - 공정 편향 의존적 패턴 (밀도 변화 큰 구간)
  - 식각 의존성 높은 패턴 (좁은 공간, 높은 밀도)

TAT:
  ML Retargeting: 수작업 대비 대폭 단축
  전체 OPC 흐름: 큰 영향 없음 (Retargeting은 전처리)
```

## OPC 툴 구현 관련성
- **SKOPC Retargeting 모듈**: `skopc/modeling/` OPC 실행 전 ML 기반 retargeting 전처리
- **패턴 피처 추출**: `skopc/core/layout_db.py`에서 retargeting용 패턴 피처 추출
- **식각 모델 연동**: `skopc/modeling/etch_model.py`와 연계하여 식각 보상 retargeting
- **레시피 통합**: YAML 레시피에 ml_retargeting 파라미터로 ML retargeting 활성화

## 참고문헌
- Proc. SPIE 11328, Design-Process-Technology Co-optimization XIV (2020)
- 저자 소속: Mentor Graphics (Siemens EDA)
- 관련: Implementing ML OPC on product layouts (SPIE 11328, 2020)
- 관련: Wafer hotspot prevention using etch-aware OPC (SPIE 9781, 2016)
- 관련: Accurate etch modeling with massive metrology (SPIE 11327, 2020)

## 태그
`Recipe`, `SPIE`, `OPC-Retargeting`, `MachineLearning`, `EtchAware`, `TargetCD`, `PreOPC`, `ProcessBias`, `MentorGraphics`, `2020`
