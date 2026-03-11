# Co-Optimization of Optical and Resist Models in the OPC Modeling Process Using In-House Genetic Algorithm

## 메타데이터
- **저자**: Yinuo Pan, Yingfang Wang, Norman Chen, Keeho Kim, Eric Parent
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124951Q
- **DOI/URL**: https://doi.org/10.1117/12.2657959

## 핵심 요약
OPC 모델링에서 광학 모델(optical model)과 레지스트 모델(resist model)을 별도로 최적화하는 기존 방법 대신, 자체 개발 유전 알고리즘(Genetic Algorithm)으로 두 모델을 동시에 공동 최적화(co-optimization)하는 방법을 제안한다. HFC Semiconductor(미국)에서 개발된 이 접근법은 OPC 모델 캘리브레이션 정확도를 향상시키고 파라미터 간 상관관계로 인한 로컬 최솟값 문제를 해결한다.

## 주요 기여
1. **광학-레지스트 모델 공동 최적화**: 두 모델을 분리하지 않고 GA로 동시에 최적화
2. **자체 개발 유전 알고리즘**: OPC 모델 캘리브레이션 특화 GA 구현
3. **로컬 최솟값 회피**: GA의 전역 탐색 능력으로 기존 그래디언트 방법의 로컬 최솟값 문제 극복
4. **파라미터 간 상관관계 처리**: 광학-레지스트 파라미터 간 결합 최적화로 정확도 향상
5. **캘리브레이션 자동화**: GA 기반 자동 파라미터 탐색으로 수동 튜닝 감소

## Recipe/Flow 상세
- **GA 기반 OPC 모델 공동 최적화 플로우**:
  1. **모델 파라미터 공간 정의**:
     - 광학 모델: NA, sigma(inner/outer), aberration 계수, flare 등
     - 레지스트 모델: 확산 계수, 현상 속도, 임계값 등
     - 전체 파라미터 벡터: [광학 파라미터 | 레지스트 파라미터]
  2. **GA 초기 집단 생성**:
     - 파라미터 공간에서 무작위 초기 개체군(population) 생성
     - 각 개체: 광학+레지스트 파라미터의 하나의 조합
     - 집단 크기: 수십~수백 개 개체
  3. **적합도(Fitness) 평가**:
     - 각 개체의 파라미터로 OPC 시뮬레이션 실행
     - SEM 측정 CD와 시뮬레이션 CD 비교
     - 적합도 = -RMS(EPE): 낮은 오차가 높은 적합도
  4. **진화 연산**:
     - 선택(Selection): 높은 적합도 개체 우선 선택
     - 교차(Crossover): 두 부모 파라미터 조합으로 자식 생성
     - 돌연변이(Mutation): 무작위 파라미터 변형으로 다양성 유지
  5. **수렴 및 최적 파라미터 추출**:
     - 세대 반복 후 수렴 조건 확인
     - 최고 적합도 개체의 파라미터를 최종 OPC 모델로 사용
     - 교차 검증으로 일반화 성능 확인
- **공동 최적화 장점**:
  - 광학-레지스트 파라미터 간 트레이드오프 자동 균형
  - 전역 최적해 탐색으로 기존 방법 대비 더 나은 캘리브레이션 결과
  - 파라미터 수 증가에도 확장 가능한 탐색 알고리즘
- **적용 공정**: HFC Semiconductor 첨단 노드 OPC 모델 캘리브레이션

## OPC 툴 구현 관련성
- SKOPC OPC 모델 캘리브레이션 모듈에 GA 기반 공동 최적화 옵션 추가
- `ga_opc_calibration.py`: 광학+레지스트 파라미터 동시 GA 최적화
- 집단 크기, 교차율, 돌연변이율 등 GA 하이퍼파라미터 설정 인터페이스
- 기존 Levenberg-Marquardt vs. GA 캘리브레이션 성능 비교 모드

## 태그
`OPC`, `ModelCalibration`, `GeneticAlgorithm`, `OpticalModel`, `ResistModel`, `CoOptimization`, `Optimization`, `SPIE`, `2023`
