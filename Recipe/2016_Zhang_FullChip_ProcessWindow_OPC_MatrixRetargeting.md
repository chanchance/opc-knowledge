# A Novel Full Chip Process Window OPC Based on Matrix Retargeting

## 메타데이터
- **저자**: Xima Zhang, Zhitang Yu, Qingwei Liu, Xuan Shen, Liguo Zhang, Le Hong, Vlad Liubich, George Lippincott, Cynthia Zhu, James Word
- **연도**: 2016
- **게재지**: Proc. SPIE 9780, Optical Microlithography XXIX, 97801C
- **DOI/URL**: https://doi.org/10.1117/12.2219913
- **인용수**: ~20

## 핵심 요약
매트릭스 리타겟팅(matrix retargeting) 기반의 새로운 전체 칩 공정 윈도우 OPC(PWOPC) 방법론을 제시한다. 제약 기반 행렬 풀이와 최소 리타겟팅 적용으로 최적 OPC 해를 찾는다. Mentor Graphics와 SMIC(Semiconductor Manufacturing International Corp.) 협력으로 실제 산업 공정에 적용된 결과를 보고한다.

## 주요 기여
1. 제약 기반 행렬 최적화로 공정 윈도우 최대화하는 PWOPC 알고리즘
2. 최소 리타겟팅으로 마스크 복잡도를 줄이면서 공정 윈도우 확보
3. 전체 칩 규모 적용 검증 (Mentor Calibre 기반)
4. SMIC 실제 공정 노드에서 산업 적용 결과

## Recipe/Process Flow 상세

### 매트릭스 리타겟팅 기반 PWOPC
```
전통적 OPC vs. PWOPC 비교:
- 전통 OPC: 명목 조건(best focus, best dose)에서 EPE 최소화
- PWOPC: 공정 윈도우 전체에서 인쇄 가능성 최대화

매트릭스 리타겟팅 개념:
- 리타겟팅: 주 패턴 목표 CD를 명목값에서 오프셋 조정
- 최적 리타겟팅: 공정 윈도우 내 모든 조건에서 EPE 최소화
```

### 알고리즘 상세
```
1. 공정 윈도우 모델링
   - (focus, dose) 그리드로 공정 윈도우 이산화
   - 각 PW 포인트에서 리소그래피 시뮬레이션 행렬 구성
   - 세그먼트 CD = A · (mask_edge_positions) + b
     여기서 A = 전달 행렬, b = 바이어스 항

2. 제약 기반 최적화
   목적함수: PW 전체에서 |CD - CD_target|² 최소화
   제약 조건:
     - 마스크 에지 이동 범위 제한 (MFR)
     - 최소 리타겟팅: 리타겟팅량 최소화 페널티
     - 공정 윈도우 요건: 각 PW 포인트에서 EPE < 임계값

3. 행렬 풀이
   - 선형 최소 자승 문제로 정식화
   - 희소 행렬 구조 활용한 효율적 풀이
   - 전체 칩 규모: 병렬화/계층적 처리

4. OPC 보정 생성
   - 최적 리타겟팅값으로 세그먼트 목표 업데이트
   - 기존 OPC 엔진에 업데이트된 목표 전달
   - 표준 OPC 이터레이션으로 최종 보정 완성
```

### PWOPC 파라미터
```
공정 윈도우 샘플링:
- 초점 범위: [-DOF/2, +DOF/2], 스텝 수: 5~9
- 노광량 범위: [-10%, +10%], 스텝 수: 3~5

최적화 파라미터:
- 리타겟팅 페널티 가중치 λ
- PW 포인트별 가중치 (명목 조건 > 극단 조건)
- 최대 리타겟팅 허용량 (마스크 복잡도 제어)
```

### 산업 검증 결과 (SMIC 공정)
- Mentor Graphics Calibre PWOPC로 전체 칩 처리
- 기존 OPC 대비 공정 윈도우 확장
- 마스크 복잡도: 최소 리타겟팅으로 허용 범위 유지
- 런타임: 실용적 TAT 내 처리

## OPC 툴 구현 관련성
- **SKOPC PWO 모듈**: `skopc/pwo/` 공정 윈도우 최적화와 직접 연계 — 행렬 리타겟팅이 NSGA-II 목적함수
- **전달 행렬 A**: 세그먼트별 CD-마스크 전달 함수는 `skopc/core/litho_engine.py`의 Jacobian 행렬과 동일
- **다중 PW 조건**: 여러 focus/dose 조건에서 시뮬레이션은 `skopc/core/process_model.py` 확장으로 구현
- **Mentor/SMIC**: 산업 현장 검증으로 방법론의 실용성 입증

## 참고문헌
- Proc. SPIE 9780, Optical Microlithography XXIX (2016)
- 저자 소속: Mentor Graphics Corp. (US), SMIC (China), Mentor Graphics Shanghai (China)
- 관련: Process variation aware OPC with VLIM (DAC, 2006)
- 관련: Fast Forward OPC (SPIE, 2007)

## 태그
`Recipe`, `SPIE`, `ProcessWindowOPC`, `PWOPC`, `MatrixRetargeting`, `FullChip`, `Calibre`, `SMIC`, `MentorGraphics`, `Retargeting`
