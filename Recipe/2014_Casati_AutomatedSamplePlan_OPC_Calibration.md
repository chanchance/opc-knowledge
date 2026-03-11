# Automated Sample Plan Selection for OPC Modeling

## 메타데이터
- **저자**: Nathalie Casati, Maria Gabrani, Ramya Viswanathan, Zikri Bayraktar, Om Jaiswal, David DeMaris, Amr Y. Abdo, James Oberschmidt, Andreas Krause
- **연도**: 2014
- **게재지**: Proc. SPIE 9052, Optical Microlithography XXVII, 90520J
- **DOI/URL**: https://doi.org/10.1117/12.2045461
- **인용수**: ~30

## 핵심 요약
OPC 모델 캘리브레이션을 위한 계측 데이터 생성 시간을 줄이면서 실제 회로 설계의 패턴 다양성을 잘 대표하는 데이터 품질을 유지하는 자동화 샘플 계획 선택 방법론. LLE(Locally Linear Embedding) 기반 샘플 선택으로 POR(Plan of Record) 세트와 동등한 모델 품질을 더 적은 계측 데이터로 달성하며, 14nm 및 22nm CMOS 공정 캘리브레이션에 적용 검증한다.

## 주요 기여
1. OPC 모델 캘리브레이션을 위한 패턴 선택을 최적화 문제로 정형화
2. LLE(Locally Linear Embedding) 기반 샘플 선택 기법
3. 계측 데이터 수요 감소 + 모델링 TAT 개선 (정확도 희생 없음)
4. 14nm 및 22nm CMOS 기술 검증 (IBM Research + ETH Zürich)

## Recipe/Process Flow 상세

### OPC 모델 캘리브레이션 샘플 계획 문제
```
전통적 접근:
  - POR(Plan of Record): 경험과 직관으로 선택된 패턴 세트
  - 수백~수천 측정 포인트
  - 계측 시간: 수일~수주
  - 한계: 체계적 방법 없음, 비효율 가능

목표:
  최소한의 측정 패턴으로 최고 모델 품질 달성
  = 대표적 패턴 최적 선택 문제
```

### LLE 기반 샘플 선택 알고리즘
```
1. 후보 패턴 공간 정의
   - 실제 회로 설계에서 모든 가능한 패턴 추출
   - 패턴 피처 표현: CD, pitch, density, aspect ratio 등
   - 피처 행렬 X ∈ R^(N_candidates × D)

2. LLE (Locally Linear Embedding) 차원 축소
   - 고차원 패턴 피처 → 저차원 다양체(manifold)
   - LLE: 국소 이웃 관계를 보존하는 비선형 차원 축소
   - 결과: X → Z ∈ R^(N_candidates × d), d << D

3. 샘플 선택 최적화
   목적함수 (다목적 최적화):
     a) 대표성: 선택된 샘플이 전체 분포 커버
     b) 다양성: 선택된 샘플 간 최대 다양성
     c) 모델러 전문성: 중요 패턴 우선 (가중치)
     d) 측정 비용: 최소 샘플 수

   최적화 알고리즘:
     - 탐욕적 선택 (greedy) 또는 유전 알고리즘
     - 각 이터레이션: 다목적 기준 최대화 샘플 추가

4. 선택된 샘플로 OPC 모델 캘리브레이션
   - 계측 실행 (선택된 패턴만)
   - 모델 파라미터 최적화
   - 검증 패턴 세트에서 모델 정확도 확인
```

### 검증 결과 (14nm 및 22nm CMOS)
```
14nm CMOS:
  POR 세트 대비 측정 패턴 수: 유의미한 감소
  모델 RMS 오차: POR과 동등
  TAT: 감소

22nm CMOS:
  LLE 기반 선택 > 랜덤 선택 > 전문가 선택 일부
  모델 안정성: POR 동등
```

### 기존 기법과의 비교
```
기존 방법:
  - 랜덤 샘플링: 빠르지만 대표성 낮음
  - 전문가 기반: 지식 의존, 비체계적
  - 클러스터링 기반: 대표성은 좋으나 모델러 전문성 반영 미흡

LLE 기반 (본 논문):
  - 비선형 다양체 구조 보존
  - 다목적 최적화로 균형 달성
  - 모델러 전문성 통합 가능
```

## OPC 툴 구현 관련성
- **SKOPC 모델 캘리브레이션**: `skopc/modeling/` OPC 모델 캘리브레이션 시 최적 샘플 패턴 선택 자동화에 직접 적용
- **데이터 효율**: 적은 측정 데이터로 고품질 모델 달성 → 신규 노드 개발 비용 절감
- **LLE 구현**: scikit-learn의 LocallyLinearEmbedding으로 즉시 구현 가능
- **IBM Research + ETH Zürich**: 학계-산업계 협력 연구, 최첨단 노드 검증

## 참고문헌
- Proc. SPIE 9052, Optical Microlithography XXVII (2014)
- 저자 소속: IBM Research (Watson), IBM Microelectronics, ETH Zürich
- 관련: Automation of sample plan creation for process model calibration (SPIE 7640, 2010)
- 관련: SEM image contouring for OPC model calibration (SPIE 6520, 2007)

## 태그
`Recipe`, `SPIE`, `ModelCalibration`, `SamplePlan`, `LLE`, `PatternSelection`, `OPC-Model`, `14nm`, `22nm`, `IBM`, `ETH`
