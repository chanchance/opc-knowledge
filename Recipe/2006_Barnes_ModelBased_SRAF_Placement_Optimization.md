# Model-Based Placement and Optimization of Subresolution Assist Features

## 메타데이터
- **저자**: Levi D. Barnes, Benjamin D. Painter, Lawrence S. Melvin III
- **연도**: 2006
- **게재지**: Proc. SPIE 6154, Optical Microlithography XIX, 61542C
- **DOI/URL**: https://doi.org/10.1117/12.656691
- **인용수**: ~80

## 핵심 요약
SRAF는 첨단 리소그래피 공정의 공정 강건성(through-process robustness)을 향상시키는 중요한 도구다. 기존에는 휴리스틱 규칙으로 SRAF를 배치·조정했으나, 피처 크기 축소에 따라 규칙 복잡도가 급격히 증가하고 더 많은 웨이퍼 데이터와 엔지니어링 노력이 필요해진다. 본 논문은 공정 윈도우 모델을 활용한 모델 기반 접근법이 다양한 2D 기하구조를 더 잘 처리하고 사용자 노력을 크게 줄일 수 있음을 입증한다.

## 주요 기여
1. 공정 윈도우 모델 기반 최적 SRAF 초기 배치 규칙 도출 방법
2. 마스크 규칙 위반을 최적 방식으로 해결하는 모델 기반 접근
3. 불량 마스크 사이트의 사후 보정(post-placement correction) 방법
4. 휴리스틱 규칙 대비 모델 기반 접근의 우월성 정량적 입증

## Recipe/Process Flow 상세

### 모델 기반 SRAF 배치 3단계 프레임워크
```
단계 1: 최적 초기 배치 규칙 도출 (Model-Driven Rule Derivation)
─────────────────────────────────────────────────────────────────
a) 대표 1D 패턴 세트 선택 (pitch, CD 범위)
b) 각 패턴에서 공정 윈도우 최대화 SRAF 위치 탐색
   - 다양한 SRAF 위치 후보에 대해 리소그래피 시뮬레이션
   - DOF × EL 면적 최대화 위치 결정
c) SRAF 위치와 주 패턴 CD/pitch의 함수 관계 피팅
   - Space-Width 테이블 생성
   - 2D 패턴으로의 규칙 일반화

단계 2: 마스크 규칙 위반 최적 해결 (MRC Violation Resolution)
────────────────────────────────────────────────────────────────
규칙 기반 배치 후 SRAF가 MRC 위반 시:
a) 다양한 MRC 해결 옵션 생성
   - SRAF 크기 축소
   - SRAF 위치 이동
   - SRAF 제거
b) 각 옵션에 대해 공정 윈도우 평가
c) 공정 윈도우 손실 최소화 옵션 선택
→ 최적 MRC 해결로 공정 윈도우 유지

단계 3: 사후 보정 (Post-Placement Correction)
────────────────────────────────────────────────
배치 완료 후 공정 윈도우 불량 사이트 식별 및 보정:
a) 전체 레이아웃 공정 윈도우 평가
b) PV 밴드 불량 사이트 식별 (핫스팟)
c) 핫스팟 SRAF 재최적화
   - 위치, 크기, 형상 재탐색
   - 이웃 패턴과의 상호작용 고려
d) 재검증
```

### 공정 윈도우 모델 기반 평가
```
평가 지표:
  - DOF (Depth of Focus): 초점 심도
  - EL (Exposure Latitude): 노광 여유
  - PW 면적 = DOF × EL
  - NILS: Normalized Image Log-Slope

모델:
  - Hopkins 광학 모델
  - 임계값 기반 레지스트 모델
  - 다중 focus/dose 조건 시뮬레이션
```

### 휴리스틱 vs. 모델 기반 비교
```
휴리스틱 규칙:
  장점: 빠른 실행
  단점: 2D 구조에서 부정확, 규칙 개발 노력 큼

모델 기반:
  장점: 2D 구조에서 정확, 사용자 노력 감소
  단점: 계산 비용 높음
  결과: 공정 윈도우 개선, MRC 최적 해결
```

## OPC 툴 구현 관련성
- **SKOPC SRAF 모듈의 이론적 기반**: `skopc/modeling/sraf_generator.py`의 모델 기반 SRAF 삽입 설계 원칙
- **3단계 파이프라인**: 규칙 도출 → MRC 해결 → 사후 보정 구조는 SKOPC SRAF 워크플로우와 직접 대응
- **Synopsys 출처**: Synopsys Proteus OPC의 MB-SRAF 기능 이론적 배경
- **PV 모델 활용**: 공정 윈도우 모델로 SRAF 위치 평가하는 방식이 SKOPC LithoEngine과 연계

## 참고문헌
- Proc. SPIE 6154, Optical Microlithography XIX (2006)
- 저자 소속: Synopsys, Inc.
- 관련: CTM-SRAF (IEEE TCAD, 2023)
- 관련: Model-based SRAF solutions for advanced technology nodes (SPIE 8886, 2013)
- 특허: US8037429B2 — Model-based SRAF insertion

## 태그
`Recipe`, `SPIE`, `SRAF`, `ModelBasedSRAF`, `ProcessWindow`, `MRCResolution`, `PostPlacementCorrection`, `HeuristicRules`, `Synopsys`, `2006`
