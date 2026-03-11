# Full Chip Inverse Lithography Technology Mask Synthesis for Advanced Memory Manufacturing

## 메타데이터
- **저자**: Zeng, Q. et al. (ASML Brion / Samsung)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II
- **DOI/URL**: https://doi.org/10.1117/12.2657538
- **인용수**: ~18

## 핵심 요약
첨단 메모리 양산을 위한 전체 칩 ILT(Inverse Lithography Technology) 마스크 합성 방법을 제안한다. GAD(Global Array Detect)로 셀 반복 패턴을 감지·최적화하고, PBC(Periodic Boundary Condition)로 시뮬레이션·마스크 대칭성을 유지하며, CLILT(Cell-Level ILT) 플로우로 반복 셀 영역을 처리한다. 이를 통해 합리적인 시간과 계산 자원으로 전체 필드 마스크의 ILT를 완성하고, 기존 OPC 대비 공정 윈도우를 확장한다.

## 주요 기여
1. GAD(Global Array Detect): 메모리 어레이의 셀 반복성 자동 감지 및 ILT 가속
2. PBC(Periodic Boundary Condition): ILT 최적화 중 주기 경계 조건으로 물리적 일관성 보장
3. CLILT(Cell-Level ILT): 반복 셀 단위 ILT로 계산량 대폭 절감
4. 전체 필드 메모리 마스크 ILT: OPC 대비 확장된 공정 윈도우 및 감소된 로컬 CD 변동
5. 메모리 양산 환경에서의 ILT 실현 가능성 최초 실증

## 모델 수식/아키텍처

**ILT 목적함수 (기본):**
```
min_{mask} L(mask) = ||I_sim(mask) - I_target||² + λ·R(mask)
R(mask) = 마스크 복잡도 정규화 (SRAF 수, 엣지 수)
```

**GAD 기반 셀 반복 감지:**
```
cell_library = {cell_i: layout_pattern_i, position_list_i}
ILT_result_i = ILT(cell_i)  [1회 계산]
Full_chip_mask = tile(ILT_result_i, position_list_i)  [타일링]
```

**PBC(주기 경계 조건) 적용:**
```
mask(x + P, y) = mask(x, y)  [x 방향 주기성]
mask(x, y + P) = mask(x, y)  [y 방향 주기성]
→ ILT 최적화 시 경계 효과 제거
```

**CLILT 플로우:**
```
Step 1: 셀 추출 (cell boundary + PBC 포함)
Step 2: 셀 단위 ILT (I_sim_PBC → 최적화)
Step 3: 경계 처리 (boundary blending)
Step 4: 전체 칩 마스크 어셈블리
```

**공정 윈도우 비교:**
```
PW_OPC: CD ±10% @ Focus ±50nm, Dose ±5%
PW_ILT: CD ±10% @ Focus ±70nm, Dose ±8%
→ ILT: DOF +40%, 도즈 윈도우 +60%
```

## 모델 유형
- [x] 광학 모델 (ILT 리소 시뮬레이션)
- [ ] 레지스트 모델
- [ ] ML/DL
- [x] 하이브리드 (ILT + 셀 반복 가속 기법)

## OPC 툴 구현 관련성
- skopc ILT 모듈: 메모리 어레이용 CLILT + GAD + PBC 구현
- 메모리 제품(DRAM, NAND): 강한 셀 반복성 → CLILT로 ILT 계산량 100× 절감 가능
- PBC: FFT 기반 시뮬레이션에서 자연스럽게 구현 (주기 컨볼루션)
- 전체 칩 ILT의 실용화를 위한 핵심 최적화 기법
- Samsung/ASML Brion의 메모리 ILT 양산 적용 사례

## 참고문헌
- Yang, Y. et al., "GPU-accelerated ILT for curvilinear mask" (2024)
- Sakr, E. et al., "High accuracy OPC EM full-chip modeling" (2024)
- Liu, Y. et al., "Neural ILT" (ICCAD 2020)

## 태그
`Model`, `SPIE`, `ILT`, `FullChip`, `Memory`, `GAD`, `PBC`, `CLILT`, `ProcessWindow`, `2023`
