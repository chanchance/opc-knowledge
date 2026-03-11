# OPC Strategies to Reduce Failure Rates with Rigorous Resist Model Stochastic Simulations in EUVL

## 메타데이터
- **저자**: Alessandro Vaglio Pret, Trey Graves, David Blankenship, Stewart A. Robertson, Patrick Lee, John J. Biafore
- **연도**: 2019
- **게재지**: Proc. SPIE 10957, Extreme Ultraviolet (EUV) Lithography X
- **DOI/URL**: https://doi.org/10.1117/12.2515124

## 핵심 요약
5nm 기술 노드의 SRAM 셀(다크필드 마스크)을 대상으로, 서로 다른 OPC 전략과 포토레지스트 특성이 EUV 스토캐스틱 결함 발생률(failure rate)에 미치는 영향을 정량 비교한 논문. 유기계 CAR(Chemically Amplified Resist) 모델과 금속산화물 레지스트 모델을 모두 검토하였으며, 리고러스 스토캐스틱 시뮬레이션을 OPC 보정 루프에 통합하는 방법론을 제시하였다.

## 주요 기여
1. **4가지 OPC 전략 정량 비교**:
   - Case 1: 유기계 CAR + 마스크 바이어싱 기반 에어리얼 이미지 최적화
   - Case 2-a: 유기계 CAR + 모델 기반 OPC
   - Case 2-b: 금속산화물 레지스트 + 모델 기반 OPC
   - Case 3: 유기계 CAR + 리고러스 스토캐스틱 모델링 통합 모델 기반 OPC
2. **스토캐스틱 결함률 지표화**: bridge/break 결함을 확률 함수로 정의하고 OPC 결과별 비교
3. **레지스트 재료 영향 분리**: 레지스트 물성(CAR vs. 금속산화물)이 스토캐스틱 실패율에 미치는 독립적 기여 정량
4. **스토캐스틱 OPC 루프**: 결함률 최소화를 비용함수로 삼는 OPC 반복 수렴 프레임워크 제안

## 검증 방법론
- 5nm 노드 SRAM 다크필드 마스크 레이아웃을 테스트케이스로 사용
- Prolith/K2T 리고러스 스토캐스틱 시뮬레이터로 bridge/break 결함 확률 분포 계산
- 포커스-도즈 매트릭스(FEM) 상에서 결함 발생 확률 곡선 비교
- OPC 전략별 MEEF, EPE, 프로세스 윈도우 면적 동시 검증

## OPC 툴 구현 관련성
- SKOPC의 EUV 스토캐스틱 OPC 비용함수 설계에 직접 적용 가능
- `2024_Wang_stochastic_OPC_cost_function_EUV.md` 문헌의 선행 기초 연구
- 스토캐스틱 결함률을 OPC 수렴 지표로 사용하는 모드 구현 시 참조 필수
- 레지스트 모델 선택(CAR vs. MOR)이 OPC 결과에 미치는 영향 분석 기준 제공

## 태그
`Verification`, `SPIE`, `EUV`, `Stochastic`, `OPC`, `Failure Rate`, `Resist Model`, `SRAM`, `5nm`
