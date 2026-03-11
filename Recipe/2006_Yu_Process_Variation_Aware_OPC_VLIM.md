# Process Variation Aware OPC With Variational Lithography Modeling

## 메타데이터
- **저자**: Peng Yu, Sean X. Shi, David Z. Pan
- **연도**: 2006
- **게재지**: Proceedings of the 43rd Annual Design Automation Conference (DAC 2006), pp. 785–790
- **DOI/URL**: https://doi.org/10.1145/1146909.1147108 / https://ieeexplore.ieee.org/document/1688902
- **인용수**: ~200

## 핵심 요약
진정한 공정 변동 인식 OPC(PV-OPC) 프레임워크를 최초로 제안한 선구적 연구. VLIM(Variational Lithography Model)으로 공정 윈도우 전체를 추가 런타임 없이 시뮬레이션하고, V-EPE(Variational Edge Placement Error) 메트릭으로 OPC를 가이드한다. 기존 OPC 대비 2~3배의 런타임 증가만으로 노광량(dosage)과 초점(focus) 변동에 훨씬 강건한 OPC 결과를 달성한다.

## 주요 기여
1. VLIM: 공정 윈도우 전체를 시뮬레이션하는 변동 리소그래피 모델 도출
2. VLIM 캘리브레이션 방법론 — 비변동 모델과 동등한 정확도 달성
3. V-EPE: 변동 EPE 메트릭 — 기존 EPE의 자연스러운 확장
4. PV-OPC: V-EPE 기반 OPC 알고리즘 — 기존 OPC 대비 2~3X 런타임으로 공정 강건성 달성

## Recipe/Process Flow 상세

### VLIM (Variational Lithography Model) 도출
```
기존 리소그래피 모델:
I(x; f0, d0) = ∑|TCCij| · Mi · Mj*   (단일 공정 조건)

VLIM 확장:
I(x; f, d) = I(x; f0, d0) + ∂I/∂f · Δf + ∂I/∂d · Δd + ...

여기서:
- f = 초점 (focus), d = 노광량 (dose/defocus)
- f0, d0 = 명목 공정 조건
- ∂I/∂f, ∂I/∂d = 1차 감도 항 (오프라인 사전 계산)

런타임 이점:
- 명목 조건 시뮬레이션 + 사전 계산된 감도 항 조합
- 전체 공정 윈도우 샘플링 대비 ~추가 런타임 없음
```

### V-EPE (Variational EPE) 메트릭
```
기존 EPE(x) = |edge_position_simulated - edge_position_target|

V-EPE(x) = max_{(f,d) ∈ PW} |edge_position(x; f,d) - target|

실용적 근사:
V-EPE(x) ≈ EPE(x; f0,d0) + |∂EPE/∂f|·σf + |∂EPE/∂d|·σd

여기서 σf, σd = 공정 변동의 표준편차
```

### PV-OPC 알고리즘
```
For each OPC iteration:
1. VLIM으로 명목 조건 + 변동 조건 시뮬레이션
2. V-EPE 계산 (각 에지 세그먼트)
3. V-EPE를 최소화하는 방향으로 세그먼트 이동
   - 기존 EPE가 아닌 V-EPE를 목적함수로 사용
4. 수렴 체크: RMS V-EPE < threshold
```

### 성능 결과
```
런타임: 기존 OPC 대비 2~3X (허용 가능한 오버헤드)
공정 강건성:
  - 노광량(dosage) 변동에 강건
  - 초점(focus) 변동에 강건
  - 기하학적 인쇄 가능성 개선
  - 전기적 특성(Vt, Ion) 변동 감소
```

## OPC 툴 구현 관련성
- **SKOPC 공정 모델**: `skopc/core/process_model.py`에 VLIM 확장 가능
- **V-EPE 목적함수**: OPC 이터레이션에서 단순 EPE 대신 V-EPE 사용으로 강건성 향상
- **PWO 연계**: `skopc/pwo/` 공정 윈도우 최적화와 상보적 — OPC 단계에서 PV 인식 보정
- **David Z. Pan 그룹**: UT Austin UTDA, OPC/DFM 분야 최고 연구팀

## 참고문헌
- DAC 2006, ACM/IEEE Design Automation Conference
- 확장 버전: JM3 Vol. 6, No. 3, 031004 (SPIE, 2007)
- 저자 소속: University of Texas at Austin
- 관련: Classical control theory applied to OPC convergence (SPIE, 2004)

## 태그
`Recipe`, `IEEE`, `DAC`, `ProcessVariation`, `PV-OPC`, `VLIM`, `V-EPE`, `ModelCalibration`, `ProcessWindow`, `DavidZPan`
