# Full Chip Inverse Lithography Technology Mask Synthesis for Advanced Memory Manufacturing

## 메타데이터
- **저자**: Jennefir Digaum, Gary Chiang, Lin Wang, Kyle Braam, Dave Gerold, Yongdong Wang, Thuc Dam
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 1249503
- **DOI/URL**: https://doi.org/10.1117/12.2657538

## 핵심 요약
첨단 메모리 제조를 위한 full-chip ILT(Inverse Lithography Technology) 마스크 합성 방법을 개발한다. 메모리 제조에서 수율에 영향을 미치는 세 가지 핵심 요소인 리소그래피 공정 창, 전체 필드 CD 균일도, 보정 런타임을 개선하기 위해 GAD(Global Array Detect), PBC(Periodic Boundary Condition), CLILT(Cell-Level ILT)를 결합한 메모리 특화 ILT 플로우를 제안한다.

## 주요 기여
1. **메모리 특화 Full-chip ILT**: 메모리 어레이 반복 구조를 활용한 효율적 ILT 마스크 합성
2. **GAD(Global Array Detect)**: 셀 반복 패턴 감지 및 최적화로 어레이 영역 처리 효율화
3. **PBC(Periodic Boundary Condition)**: 주기적 경계 조건으로 셀 대칭성 유지 및 시뮬레이션 정확도 향상
4. **CLILT(Cell-Level ILT)**: 반복 셀 단위 ILT 처리 후 전체 어레이로 전파하는 계층적 접근법
5. **공정 창 확대 + CD 균일도 향상 + 런타임 단축**: 세 가지 핵심 지표 동시 개선

## Recipe/Flow 상세
- **메모리 Full-chip ILT 플로우**:
  1. **레이아웃 분석 및 GAD**:
     - 전체 칩 레이아웃에서 반복 셀 패턴 자동 감지 (GAD)
     - 셀 단위 경계 및 반복 규칙 추출
     - 어레이 영역 vs. 주변 회로 영역 분리
  2. **CLILT (Cell-Level ILT)**:
     - 대표 셀(unit cell)에 대해서만 ILT 최적화 실행
     - PBC 적용: 셀 경계에서 연속성 및 대칭성 유지
     - ILT 비용 함수: 공정 창 최대화 + CD 균일도 최적화
  3. **ILT 결과 전체 어레이 전파**:
     - 최적화된 단위 셀 ILT 결과를 전체 어레이에 타일링
     - 경계 영역(array-periphery 접합부) 블렌딩
     - 완전히 일관된 어레이 마스크 생성
  4. **주변 회로 OPC**:
     - 랜덤 로직 구조의 주변 회로는 기존 OPC 적용
     - 어레이-주변 경계 영역 특화 처리
  5. **검증**:
     - 공정 창 향상 확인 (DOF, EL 증가)
     - CD 균일도 개선 측정
     - 전체 런타임 vs. 패턴별 ILT 비교
- **메모리 ILT 핵심 메커니즘**:
  - GAD + PBC: 어레이 반복성 활용으로 연산량 1/N 감소 (N = 반복 수)
  - CLILT: 단위 셀만 최적화 → 전체 어레이 확장
  - 결과: 일관된 마스크 어레이 + 넓은 공정 창 + 최소 CD 변동
- **적용 제품**: 첨단 DRAM/NAND 메모리 셀 어레이 레이어

## OPC 툴 구현 관련성
- SKOPC 메모리 ILT 모드에서 GAD + PBC + CLILT 통합 구현
- `memory_ilt_flow.py`: 어레이 감지 → 단위 셀 ILT → 전체 어레이 전파 파이프라인
- 메모리 공정 창 최적화를 위한 ILT 비용 함수 설계
- 전체 런타임 최적화: 반복 구조 캐싱으로 full-chip ILT 실현

## 태그
`ILT`, `FullChip`, `Memory`, `DRAM`, `NAND`, `CellLevelILT`, `PBC`, `ProcessWindow`, `CDUniformity`, `Runtime`, `SPIE`, `2023`
