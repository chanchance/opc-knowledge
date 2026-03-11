# Classical Control Theory Applied to OPC Correction Segment Convergence

## 메타데이터
- **저자**: Benjamin Painter, Lawrence L. Melvin III, Michael L. Rieger
- **연도**: 2004
- **게재지**: Proc. SPIE 5377, Optical Microlithography XVII
- **DOI/URL**: https://doi.org/10.1117/12.537586
- **인용수**: ~80

## 핵심 요약
Model-based OPC는 레이아웃 패턴을 세그먼트로 분할하고 EPE(Edge Placement Error)를 0으로 수렴시키기 위해 반복적으로 보정을 적용하는 개방 루프(open-loop) 제어 방식이다. 본 논문은 고전 제어 이론(PID 제어기)을 OPC 보정 세그먼트 수렴에 적용하여 수렴 속도를 개선하고 발산을 방지하는 방법을 제시한다.

## 주요 기여
1. OPC 세그먼트 보정을 제어 시스템 문제로 재정의
2. PID(비례-적분-미분) 제어기의 OPC 적용 방법론
3. 댐핑 팩터 기반 수렴 제어의 한계 분석
4. 이터레이션 수 감소를 통한 OPC 런타임 개선

## Recipe/Process Flow 상세

### 기존 Model-Based OPC 수렴 메커니즘
```
초기 마스크 → 시뮬레이션 → EPE 측정 → 보정 적용 → 반복
```
- 각 이터레이션: 단일 시뮬레이션 + 폴리곤 단편화 이동 시퀀스
- 전형적 수렴: 정확한 OPC 레시피는 8회 이상 이터레이션 필요
- 문제점: 잘못된 댐핑 팩터 → 발산 또는 느린 수렴

### PID 제어기 적용 프레임워크

**제어 변수 정의**
- 설정값(Setpoint): target CD (목표 에지 위치)
- 측정값(Process Variable): 시뮬레이션된 에지 위치
- 제어 출력: 에지 세그먼트 이동량 (displacement)

**PID 수식**
```
u(k) = Kp·e(k) + Ki·Σe(j) + Kd·[e(k) - e(k-1)]

여기서:
- e(k) = EPE at iteration k (목표-측정 차이)
- Kp = 비례 이득 (proportional gain)
- Ki = 적분 이득 (integral gain)
- Kd = 미분 이득 (derivative gain)
- u(k) = k번째 이터레이션에서의 세그먼트 이동량
```

**각 항의 역할**
- P 항: 현재 EPE에 비례하는 즉각적 보정
- I 항: 누적 오차 제거 (steady-state error 제거)
- D 항: 오차 변화율 기반 예측적 보정 (오버슈트 방지)

### 수렴 개선 효과
```
기존 방식 (비례 댐핑 팩터만 사용):
- 이터레이션 수: 8~12회
- 일부 구조에서 발산 위험

PID 제어기 적용:
- 이터레이션 수: 4~6회 (~50% 감소)
- 발산 방지 (D 항의 예측 효과)
- 다양한 구조 유형에서 안정적 수렴
```

### 구조 유형별 게인 튜닝
- Dense lines: Kp 높게, Kd 낮게
- Isolated features: Kp 낮게, Ki 추가
- Line-ends (2D): 별도 게인 파라미터 필요
- Sub-resolution features: 특수 처리 필요

## OPC 툴 구현 관련성
- **SKOPC 수렴 알고리즘**: `skopc/modeling/model_opc.py`의 이터레이션 루프에 PID 수렴 제어 직접 적용 가능
- **핵심 공식**: `segment_move = Kp * epe + Ki * sum(epe_history) + Kd * (epe - prev_epe)`
- **파라미터**: Kp, Ki, Kd를 구조 유형별로 레시피에 정의
- **런타임 단축**: 이터레이션 감소로 전체 OPC 런타임 ~50% 단축 가능
- **Synopsys 출처**: Synopsys Proteus OPC 툴의 이론적 기반

## 참고문헌
- Proc. SPIE 5377, Optical Microlithography XVII (2004)
- 저자 소속: Synopsys, Inc.
- 관련: Model-Based OPC With Adaptive PID Control Through Reinforcement Learning (IEEE, 2025)
- 관련: Design of automatic controllers for model-based OPC (SPIE 6924, 2008)

## 태그
`Recipe`, `SPIE`, `PID-Control`, `Convergence`, `ModelBasedOPC`, `EdgeSegment`, `EPE`, `IterationControl`, `Synopsys`
