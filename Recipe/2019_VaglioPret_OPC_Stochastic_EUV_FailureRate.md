# OPC Strategies to Reduce Failure Rates with Rigorous Resist Model Stochastic Simulations in EUVL

## 메타데이터
- **저자**: Alessandro Vaglio Pret, Trey Graves, David Blankenship, Stewart A. Robertson, Patrick Lee, John J. Biafore
- **연도**: 2019
- **게재지**: Proc. SPIE 10957, Extreme Ultraviolet (EUV) Lithography X, 109570J
- **DOI/URL**: https://doi.org/10.1117/12.2515124

## 핵심 요약
확률론적 효과(stochastic effects)는 광학 리소그래피의 궁극적 한계로, 차세대 기술 노드에서 주요 우려 사항이다. 5nm 기술 노드의 darkfield 마스크 SRAM 셀을 대상으로, 서로 다른 OPC 전략과 포토레지스트 특성이 실패율(failure rate)에 미치는 영향을 연구한다. 초점-노광량 조합별로 2150회(3.5σ) 확률론적 시뮬레이션을 수행하여 공정 창을 생성한다.

## 주요 기여
1. **OPC 전략별 실패율 비교**: 다양한 OPC 바이어스/전략이 EUV stochastic 실패율에 미치는 영향 정량화
2. **레지스트 특성 영향 분석**: 포토레지스트 물리적 특성(photon sensitivity, diffusion length 등)과 실패율의 상관관계
3. **통계적 공정 창**: 3.5σ 수준의 대규모 stochastic 시뮬레이션 기반 공정 창 정의
4. **5nm 노드 검증**: 실제 SRAM 셀 레이아웃에 적용한 실용적 결과 제시
5. **최적 OPC 전략 도출**: 실패율을 최소화하는 OPC 파라미터 조합 규명

## Recipe/Flow 상세
- **EUV Stochastic-aware OPC 평가 플로우**:
  1. **SRAM 셀 레이아웃 준비**: 5nm 노드 darkfield 마스크 SRAM contact/via 패턴
  2. **OPC 전략 정의**:
     - Strategy A: 표준 deterministic OPC
     - Strategy B: 보수적 바이어스 OPC (larger CD target)
     - Strategy C: NILS 최대화 OPC
     - Strategy D: Failure probability 직접 최소화 OPC
  3. **Stochastic 시뮬레이션**:
     - 각 focus-dose 조합에서 2150회 반복 시뮬레이션
     - Monte Carlo 방식으로 포토레지스트 stochastic 변동 샘플링
  4. **실패율 계산**:
     - 각 OPC 전략별 failure rate vs. focus/dose 맵 생성
     - 3.5σ 공정 창 내 허용 가능한 실패율 기준 평가
  5. **레지스트 최적화**: 레지스트 파라미터 스윕으로 최적 레지스트-OPC 조합 탐색
- **5nm SRAM 특화 고려사항**:
  - Contact/via 홀: 폐쇄 실패(closed) 및 열림 실패(opened) 양쪽 검토
  - Darkfield 마스크: 흡수체 면적이 크므로 flare 최소화 중요
- **평가 지표**: failure rate, process window (DOF×EL at 3.5σ)

## OPC 툴 구현 관련성
- EUV OPC에 stochastic 시뮬레이션 루프 통합 방법
- OPC 전략별 실패율 평가 파이프라인
- SRAM 레이어 OPC 수렴 기준에 stochastic 목표 추가
- `stochastic_opc_eval.py`: Monte Carlo 기반 실패율 계산 → OPC 전략 비교

## 태그
`Stochastic`, `EUV`, `OPC`, `FailureRate`, `SRAM`, `5nm`, `ResistModel`, `SPIE`, `2019`
