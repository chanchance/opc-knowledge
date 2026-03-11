# Tackling Data Inconsistency and Runtime Issues in Inverse Lithography Technology (ILT) with Comparative Convergence Study

## 메타데이터
- **저자**: Po-Hsun Fang, Peichen Yu
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129541E
- **DOI/URL**: https://doi.org/10.1117/12.3007748

## 핵심 요약
ILT(Inverse Lithography Technology)의 실용적 full-chip 적용을 가로막는 두 가지 핵심 문제인 데이터 불일치(data inconsistency)와 런타임을 분석하고 해결한다. 다양한 ILT 수렴 알고리즘을 비교하여 정확도와 런타임 간 트레이드오프를 체계적으로 제시하며, 수렴 전략 선택 가이드라인을 도출한다.

## 주요 기여
1. **ILT 수렴 문제 체계적 분석**: 다양한 수렴 알고리즘의 성능을 비교 연구
2. **데이터 불일치 해결**: 클립 단위 ILT 처리 시 경계에서 발생하는 데이터 불일치 문제 해결
3. **런타임 최적화 가이드라인**: 정확도-런타임 트레이드오프에 따른 알고리즘 선택 기준 제시
4. **비교 수렴 연구**: 그래디언트 기반, 레벨-셋, ML 하이브리드 등 다양한 수렴 방법 벤치마크
5. **실용적 full-chip ILT 경로 제시**: HVM(High-Volume Manufacturing) 적용을 위한 ILT 실용화 방안

## Recipe/Flow 상세
- **ILT 수렴 비교 연구 플로우**:
  1. **ILT 문제 정의**:
     - 목표: 마스크 패턴 M → 웨이퍼 패턴 W와 목표 T의 차이 최소화
     - 비용 함수: EPE, NILS, 공정 창 등 리소 지표 포함
     - 제약 조건: MRC(Mask Rule Check), 마스크 복잡도
  2. **수렴 알고리즘 비교**:
     - 그래디언트 강하(Gradient Descent): 고전적 방법, 느린 수렴
     - Anderson Mixing: 가속 수렴, 메모리 요구 증가
     - 레벨-셋(Level-Set): 위상학적 변화 가능, 복잡성 높음
     - ML 사전 초기화: ML 예측 → 수렴 가속
  3. **데이터 불일치 분석**:
     - 클립 경계에서 SRAF/OPC 솔루션 불연속 발생
     - 클립 중첩(overlap) 처리로 경계 불일치 최소화
     - Stitching 영역 특화 비용 함수 추가
  4. **런타임 벤치마크**:
     - 알고리즘별 iteration 횟수 vs. 수렴 정확도
     - GPU 가속 적용 효과 분석
     - Full-chip TAT(Turn-Around-Time) 예측
  5. **최적 알고리즘 선택 가이드라인**:
     - 레이어 유형별(메탈, 컨택, 게이트) 권장 알고리즘
     - 허용 런타임 제약 내 최대 정확도 달성 전략
- **ILT vs. OPC 비교**: ILT는 공정 창 우수하지만 런타임 10~100배 높음
- **적용 전략**: Critical layer(게이트, 컨택)는 ILT, 나머지는 OPC 적용

## OPC 툴 구현 관련성
- SKOPC ILT 모듈 수렴 알고리즘 선택 옵션 추가
- `ilt_solver.py`: Anderson Mixing, 레벨-셋 등 다중 수렴 전략 구현
- 클립 경계 데이터 불일치 처리를 위한 overlap stitching 로직
- 레이어별 ILT/OPC 자동 선택 레시피 설계 기준

## 태그
`ILT`, `InverseLithography`, `Runtime`, `Convergence`, `OPC`, `FullChip`, `DataConsistency`, `SPIE`, `2024`
