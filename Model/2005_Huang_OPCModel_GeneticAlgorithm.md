# OPC Modeling by Genetic Algorithm

## 메타데이터
- **저자**: W. C. Huang, C. M. Lai, B. Luo, C. K. Tsai, C. S. Tsay, C. W. Lai, C. C. Kuo, R. G. Liu, H. T. Lin, Burn J. Lin
- **연도**: 2005
- **게재지**: Proc. SPIE 5754, Optical Microlithography XVIII
- **DOI/URL**: https://doi.org/10.1117/12.602096

## 핵심 요약
연속 및 이산 파라미터가 혼합된 리소그래피 모델 교정 문제에 대해 전통적 수치 최적화 방법의 한계를 극복하기 위해 유전 알고리즘(GA)을 OPC 모델 파라미터 회귀에 적용한다.

## 주요 기여
1. OPC 모델 파라미터 교정에 유전 알고리즘(GA) 최초 적용
2. 연속 + 이산 혼합 파라미터 공간에서의 효과적 전역 최적화
3. 전통적 최소제곱법 대비 복잡한 파라미터 공간 탐색 능력 향상
4. 리소그래피 모델(Hopkins TCC + 레지스트) 파라미터의 GA 최적화 구현
5. 실험 데이터 기반 OPC 모델 파라미터 회귀의 새로운 접근법 제시

## 모델 수식/아키텍처
- **GA 최적화 문제**:
  - 목적 함수: min Σ (CD_simulated - CD_measured)² (교정 게이지 오차)
  - 최적화 변수: 광학 모델 커널 계수 + 레지스트 모델 파라미터
  - 제약: 파라미터 범위 (물리적 의미 유지)
- **GA 연산**: 선택(selection), 교차(crossover), 돌연변이(mutation)
- 인코딩: 실수 코딩(real-valued encoding) 또는 이진 코딩
- 수렴 기준: 세대 수 또는 적합도 개선 임계값

## 모델 유형
- [x] 광학
- [x] 레지스트
- [x] ML/DL (메타휴리스틱 최적화)
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC 모델 교정 자동화에서 GA 기반 전역 최적화 옵션 구현 참조
- 연속/이산 혼합 파라미터를 가진 OPC 모델 교정 문제의 GA 솔버
- `2025_Chiu_DRL_OPCModelCalibration.md` 등 현대 RL 기반 교정의 역사적 선행 연구
- 광학 + 레지스트 모델 공동 최적화 접근의 초기 사례

## 태그
`Model`, `OPC`, `Calibration`, `GeneticAlgorithm`, `Optimization`, `MetaHeuristic`, `SPIE`
