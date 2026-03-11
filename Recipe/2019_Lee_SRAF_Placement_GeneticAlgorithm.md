# Placement of Sub-Resolution Assist Features Based on a Genetic Algorithm

## 메타데이터
- **저자**: (IEEE document 8752222 - ArF 시스템, DRAM 노드 연구)
- **연도**: 2019
- **게재지**: IEEE Transactions on Semiconductor Manufacturing (또는 IEEE Journal)
- **DOI/URL**: https://ieeexplore.ieee.org/document/8752222/
- **인용수**: ~20

## 핵심 요약
ArF(193nm) 액침 광 리소그래피 시스템을 위한 SRAF 배치 최적화에 유전 알고리즘을 적용한 연구. Hopkins 모델 기반 광학 모델로 간섭 맵(interference map)과 컷-레벨 맵(cut-level map)을 생성하고, 이를 SRAF 후보 위치 예측에 활용한다. DRAM 기술 노드의 미세화에 효과적인 방법론을 제시한다.

## 주요 기여
1. Hopkins 모델 기반 간섭 맵 → 컷-레벨 맵 → SRAF 후보 위치 예측 파이프라인
2. GA 기반 SRAF 배치 최적화 (초기 집단을 컷-레벨 맵에서 생성)
3. SRAF 및 주 패턴을 섹션 맵과 인코딩된 유전자로 표현
4. ArF 액침 리소그래피에서 공정 윈도우 개선 검증

## Recipe/Process Flow 상세

### 광학 모델 기반 SRAF 후보 생성
```
1. Hopkins 모델 설정
   - 광원 파라미터: λ=193nm, NA, σ (부분 가간섭성)
   - 조명 조건: Annular, Dipole, Quasar 등
   - 마스크 투과율 함수 정의

2. 간섭 맵(Interference Map) 계산
   - 마스크 패턴의 광학 전달 함수 계산
   - 이미지 강도 분포 I(x,y) 계산
   - 간섭 항 분리하여 맵 생성

3. 컷-레벨 맵(Cut-Level Map) 생성
   - 레지스트 임계값 기반 바이너리 맵
   - SRAF 삽입 가능 영역 = 강도가 프린팅 임계값 미만인 영역
   - 설계 규칙 마스킹 적용

4. SRAF 후보 랜덤 생성 (GA 초기 집단)
   - 컷-레벨 맵에서 허용 영역 내 랜덤 SRAF 생성
   - 집단 크기 N으로 초기 chromosomes 정의
```

### 유전 알고리즘 SRAF 최적화
```
염색체 인코딩:
- 섹션 맵(Section Map): 레이아웃을 격자로 분할
- 각 섹션에 SRAF 유무 및 크기를 유전자로 인코딩

적합도 함수:
- 항공 이미지 품질 지표 (NILS, image slope)
- 공정 윈도우 면적 (EL × DOF)
- 설계 규칙 위반 페널티

GA 연산:
- 선택: 토너먼트 선택
- 교배: 섹션 단위 교환
- 돌연변이: 랜덤 섹션 SRAF 추가/제거/변형

종료 조건:
- 최대 세대 수 또는 적합도 수렴
```

### DRAM 적용 결과
- ArF 액침 리소그래피 (193nm) 기반
- 기술 노드: DRAM 최소 피처 크기 최소화
- 공정 윈도우 개선: SRAF 없는 경우 대비 DOF 증가
- Rule-based SRAF 대비 최적화된 위치 배치

## OPC 툴 구현 관련성
- **SKOPC SRAF 생성기**: Hopkins 모델 간섭 맵 계산은 `skopc/core/litho_engine.py`에서 활용 가능
- **GA 최적화**: `skopc/pwo/` PWO 모듈의 NSGA-II와 유사한 진화 알고리즘 구조
- **컷-레벨 맵**: 레지스트 임계값 기반 맵은 SRAF 후보 영역 자동 결정에 직접 활용
- **ArF 파라미터**: λ=193nm, NA, 조명 조건은 `skopc/core/process_model.py`에서 설정

## 참고문헌
- IEEE Xplore Document 8752222 (2019)
- 관련: CTM-SRAF (IEEE TCAD, 2023)
- 관련: Model-based placement and optimization of subresolution assist features (SPIE 6154, 2006)
- 관련: Automatic assist feature placement optimization (SPIE 6730, 2007)

## 태그
`Recipe`, `IEEE`, `SRAF`, `GeneticAlgorithm`, `HopkinsModel`, `InterferenceMap`, `DRAM`, `ArF`, `ProcessWindow`, `MaskOptimization`
