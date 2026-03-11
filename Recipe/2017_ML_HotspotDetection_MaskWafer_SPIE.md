# Machine Learning for Mask/Wafer Hotspot Detection and Mask Synthesis

## 메타데이터
- **저자**: (SPIE 10451 - Photomask Technology 2017)
- **연도**: 2017
- **게재지**: Proc. SPIE 10451, Photomask Technology 2017, 104510A
- **DOI/URL**: https://doi.org/10.1117/12.2282943
- **인용수**: ~45

## 핵심 요약
머신러닝을 리소그래피 핫스팟 감지 및 마스크 합성에 적용하는 종합적 프레임워크를 제시한다. SVM, 부스팅, DNN 기반 핫스팟 분류기를 비교 평가하며, 피처 추출 방법이 ML 핫스팟 감지 정확도에 미치는 영향을 체계적으로 분석한다. OPC 이후 레이아웃에서 잠재 핫스팟을 고속으로 감지하는 대안으로서 ML 기반 방법의 유효성을 입증한다.

## 주요 기여
1. 마스크/웨이퍼 핫스팟 감지에 ML 적용의 체계적 비교 분석
2. 피처 추출 방법(물리 기반 vs. CNN 자동 추출)의 정확도 영향 분석
3. 불균형 데이터셋(핫스팟 vs. 비핫스팟) 처리 전략
4. ML-OPC와 ML 핫스팟 감지의 통합 프레임워크

## Recipe/Process Flow 상세

### 리소그래피 핫스팟 감지의 도전
```
기존 핫스팟 감지 방법:
  ORC (Optical Rule Check):
    - 기하학 규칙 기반 패턴 매칭
    - 속도 빠름, 복잡한 핫스팟 놓칠 수 있음

  시뮬레이션 기반 (Full-chip LRC):
    - 리소그래피 시뮬레이션으로 모든 패턴 검사
    - 정확하지만 런타임 수일~수주 소요

ML 기반 핫스팟 감지 동기:
  - ORC의 낮은 감지율과 시뮬레이션의 긴 런타임 간 균형
  - 훈련 후 추론: 초고속 (per-pattern ms 이하)
  - 데이터 기반: 알려진 핫스팟 패턴 학습
```

### ML 핫스팟 감지 파이프라인
```
1단계: 데이터 준비
  a) 클립 추출:
     OPC 이후 레이아웃 → 고정 크기 윈도우(clip)로 분할
     클립 크기: 수 μm × 수 μm (조명 범위 포함)

  b) 레이블링:
     시뮬레이션으로 각 클립의 핫스팟 여부 판정
     핫스팟: 공정 윈도우 기준 미달 패턴
     불균형 데이터: 핫스팟 << 비핫스팟 (100:1 이상)

  c) 불균형 처리:
     SMOTE (합성 소수 오버샘플링)
     클래스 가중치 조정
     앙상블 방법 (Boosting)

2단계: 피처 추출
  방법 1: 물리 기반 피처
    - 공간 이미지 강도, NILS, MEEF
    - 패턴 밀도, 피치, CD 통계
    - 근접 패턴 기하 특성

  방법 2: 이미지 기반 피처 (CNN)
    - 마스크 클립을 이미지로 직접 입력
    - CNN이 자동으로 관련 피처 학습
    - ResNet, VGG 등 전이학습 활용

3단계: ML 분류기
  SVM (Support Vector Machine):
    - 고차원 피처 공간에서 결정 경계 학습
    - 커널: RBF, 다항식
    - 성능: 전통적 벤치마크에서 기준

  Boosting (AdaBoost, GBM):
    - 약한 분류기 앙상블
    - 불균형 데이터에 강건
    - 피처 중요도 해석 가능

  DNN (Deep Neural Network):
    - 다층 완전연결 또는 CNN
    - 자동 피처 학습
    - 대용량 데이터에서 우수한 성능
```

### 피처 추출 방법 비교 분석
```
물리 기반 피처 vs. CNN 자동 피처:
  물리 기반:
    - 해석 가능성 높음
    - 수작업 설계 필요
    - 작은 데이터셋에서 좋은 성능

  CNN 자동:
    - 더 풍부한 표현
    - 대용량 데이터 필요
    - 물리 의미 불투명

최적 조합:
  물리 기반 피처 + ML 분류기: 중간 데이터에 적합
  CNN end-to-end: 대용량 데이터에서 최고 성능
```

### 성능 결과
```
핫스팟 감지 성능 (정밀도/재현율):
  SVM: 베이스라인 성능
  Boosting: SVM 대비 재현율 향상
  DNN: 가장 높은 정확도 (충분한 데이터 시)

런타임 (vs. 풀-칩 시뮬레이션):
  ML 추론: 수 배 ~ 수십 배 빠름
  트레이드오프: 학습 데이터 수집 비용
```

## OPC 툴 구현 관련성
- **SKOPC 핫스팟 감지**: `skopc/modeling/` OPC 이후 핫스팟 감지기 추가 (ML 기반)
- **클립 추출**: `skopc/core/layout_db.py`에서 레이아웃 클립 추출 기능
- **불균형 처리**: scikit-learn의 SMOTE, 클래스 가중치 파라미터 활용
- **SKOPC PWO 연동**: `skopc/pwo/` 핫스팟 클립에 공정 윈도우 분석 집중 배치

## 참고문헌
- Proc. SPIE 10451, Photomask Technology 2017
- 관련: Machine learning based lithographic hotspot detection (UT Austin, 2009)
- 관련: High performance lithography hotspot detection with ML (ICCAD, 2012)
- 관련: Automatic correction of lithography hotspots with GAN (SPIE, 2019)

## 태그
`Recipe`, `SPIE`, `HotspotDetection`, `MachineLearning`, `SVM`, `DNN`, `CNN`, `PatternMatching`, `OPC-Verification`, `ImbalancedData`, `2017`
