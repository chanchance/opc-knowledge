# Implementing Machine Learning OPC on Product Layouts

## 메타데이터
- **저자**: Hesham Abdelghany, Kevin Hooker, Marco Guajardo, Chia-Chun Lu
- **연도**: 2020
- **게재지**: Proc. SPIE 11328, Design-Process-Technology Co-optimization for Manufacturability XIV
- **DOI/URL**: https://doi.org/10.1117/12.2552398
- **인용수**: ~30

## 핵심 요약
ML-OPC(머신러닝 기반 OPC)를 실제 양산 레이아웃(product layout)에 적용하는 방법론과 그 정확도 및 TAT(Turn-Around-Time) 이점을 실증한다. ML 모델이 마스크 세그먼트 이동량(displacement)을 예측하여 초기 OPC 추정값을 제공하고, 이후 표준 OPC 이터레이션을 최소화한다. 고급 노드 양산 테스트 케이스에서 상세한 정확도 측정과 전체 OPC TAT 개선을 보고한다.

## 주요 기여
1. 양산 레이아웃에서 ML-OPC의 정확도 및 TAT 이점 실증
2. ML 세그먼트 변위 예측 + 표준 OPC 잔여 이터레이션 통합 흐름
3. 실제 양산 노드에서 ML-OPC 구현의 실용적 고려사항
4. 데이터 샘플링 전략 및 훈련 데이터 품질이 ML-OPC 성능에 미치는 영향

## Recipe/Process Flow 상세

### ML-OPC의 동기 및 아키텍처
```
기존 MB-OPC의 병목:
  - 각 이터레이션에서 모든 세그먼트에 대해 리소그래피 시뮬
  - 10-15 이터레이션 × 수억 세그먼트 = 수십 시간 런타임
  - 7nm 이하 노드: 런타임 더욱 증가

ML-OPC 접근:
  - 사전 훈련된 ML 모델이 초기 세그먼트 이동량 예측
  - 예측이 좋을수록 → 이후 OPC 이터레이션 수 감소
  - ML 추론: ms 수준 → 전체 TAT 대폭 단축

통합 흐름:
  레이아웃 → [ML 초기화] → [표준 OPC 잔여 이터레이션 (~3-5)] → 검증
  vs. 기존: 레이아웃 → [표준 OPC 10-15 이터레이션] → 검증
```

### ML 모델 아키텍처
```
입력 피처 (세그먼트별):
  - 주변 패턴 밀도 (다양한 반경)
  - 로컬 CD (선폭, 공간 폭)
  - 피치
  - 세그먼트 방향 (수평/수직/대각선)
  - 이웃 세그먼트 수

피처 표현:
  - 세그먼트 주변 영역을 이미지로 래스터화 (픽셀 기반)
  - 또는 극 좌표 피처 (회전 불변)
  - 피처 벡터 차원: 수십~수백

ML 모델:
  - Gradient Boosting 또는 Random Forest: 빠른 훈련, 해석 가능
  - CNN: 이미지 입력에서 자동 피처 학습
  - 출력: 세그먼트 이동량 (nm) = 마스크 바이어스 예측
```

### 훈련 데이터 수집 전략
```
훈련 데이터:
  소스: 기존 OPC 실행 결과 (ground truth)
  쌍: (레이아웃 피처, 수렴된 OPC 세그먼트 이동량)
  크기: 수백만 세그먼트 (다양한 레이아웃에서)

샘플링 전략:
  - 균등 샘플링: 모든 피처 범위 커버
  - 중요도 샘플링: 어려운 패턴(핫스팟 주변) 강화
  - 계층화(Stratified) 샘플링: 피치/CD 분포 균형

데이터 품질:
  - 수렴된 OPC 결과만 사용 (미수렴 제외)
  - 다양한 레이어/노드 데이터 포함 (일반화)
  - 테스트 세트: 훈련 레이아웃과 다른 설계
```

### 양산 레이아웃 적용 결과
```
정확도 (고급 노드 테스트 케이스):
  ML 예측 RMS 오차: 기존 방법 대비 개선
  초기 EPE (ML 이후, OPC 전): 감소
  최종 EPE (OPC 완료 후): 동등하거나 개선

TAT (Turn-Around-Time) 개선:
  ML 사전 초기화 사용:
    OPC 이터레이션 수: 10-15 → 3-5
    전체 OPC 런타임: 유의미한 감소 (수십 %)

  추가 이점:
    수렴 안정성: 더 안정적 수렴 (좋은 초기값 덕분)
    핫스팟 발생률: 감소 (더 정확한 초기 보정)

한계:
  훈련 데이터와 크게 다른 패턴: 예측 정확도 낮을 수 있음
  신규 노드 첫 적용 시: 기존 OPC 데이터 축적 필요
```

## OPC 툴 구현 관련성
- **SKOPC ML-OPC 모듈**: `skopc/modeling/` ML 초기화 모듈 추가로 OPC 이터레이션 수 감소
- **피처 추출**: `skopc/core/layout_db.py`에서 세그먼트별 주변 피처 추출 함수
- **모델 서빙**: 사전 훈련된 ML 모델을 pickle/ONNX로 저장 후 추론 시 로드
- **훈련 파이프라인**: 기존 OPC 결과에서 자동 훈련 데이터 생성 스크립트

## 참고문헌
- Proc. SPIE 11328, Design-Process-Technology Co-optimization XIV (2020)
- 관련: Effective data sampling techniques for ML-OPC in full chip production (SPIE 11613, 2021)
- 관련: Speeding up OPC by leveraging existing designs with ML (SPIE 11614, 2021)
- 관련: Optimization of ML-guided OPC: PFT+RFR (IEEE 8623985, 2019)

## 태그
`Recipe`, `SPIE`, `ML-OPC`, `MachineLearning`, `ProductLayout`, `SegmentDisplacement`, `TAT`, `MaskBias`, `FullChip`, `DataSampling`, `2020`
