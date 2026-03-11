# Curvilinear Mask Handling in OPC Flow

## 메타데이터
- **저자**: Yung-Yu Chen et al.
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, Optical Microlithography XXXVI; also published in Journal of Micro/Nanopatterning, Materials, and Metrology Vol. 23, Issue 1, 011203
- **DOI/URL**: https://doi.org/10.1117/12.2663274
- **인용수**: ~20

## 핵심 요약
Manhattan 형상 기반의 기존 OPC 흐름을 커브형(curvilinear) 마스크를 생성하고 처리할 수 있도록 일반화하는 방법론을 제시한다. 엣지 기반 OPC를 버텍스(vertex) 기반으로 확장하여 곡선 형상을 처리하며, 기존 분해(fragmentation), 분류, 타겟 포인트 배치 등의 OPC 핵심 기능을 커브형 마스크에 유지한다. Manhattan OPC 대비 공정 윈도우, PV 밴드, MEEF에서 커브형 마스크의 우위를 입증한다.

## 주요 기여
1. 기존 Manhattan OPC 흐름의 커브형 마스크로의 일반화 방법론
2. 엣지 기반 → 버텍스 기반 OPC 확장 (곡선 처리)
3. 커브형 마스크의 공정 윈도우 및 MEEF 개선 정량화
4. 다중 빔 마스크 기록기(MBMW) 와의 통합 호환 흐름

## Recipe/Process Flow 상세

### Manhattan vs. 커브형 마스크의 OPC 차이
```
Manhattan OPC (기존):
  마스크 형상: 직교 다각형 (수평/수직 엣지만)
  표현: 엣지 세그먼트로 마스크 경계 기술
  OPC: 각 엣지 세그먼트를 수직 방향으로 이동
  마스크 작성기: VSB(Variable Shaped Beam) 호환

  한계:
    - 최적 마스크 형상(ILT 결과)이 곡선임에도 강제 맨해턴화
    - 맨해턴화 시 OPC/ILT 성능 저하
    - 특히 라인-엔드, 코너, 복잡한 2D 패턴에서 손실

커브형 마스크 (본 논문):
  마스크 형상: 임의의 다각형/곡선
  표현: 버텍스(vertex) 집합으로 경계 기술
  OPC: 각 버텍스를 임의 방향으로 이동
  마스크 작성기: MBMW(Multi-Beam Mask Writer) 필요

  장점:
    - ILT 최적 해에 가까운 형상 달성 가능
    - 공정 윈도우 개선 (DOF × EL)
    - MEEF 감소
    - PV 밴드 감소 (공정 변동 하에서 CD 균일성)
```

### 커브형 OPC 알고리즘
```
1단계: 커브형 분해(Fragmentation)
  - 마스크 경계를 충분히 많은 버텍스로 표현
  - 버텍스 간격: 원하는 곡률 해상도에 따라 결정
  - 과분해: 런타임 증가 / 과소분해: 형상 정밀도 손실

2단계: 커브형 분류(Classification)
  - 각 버텍스를 1D(직선 구간) 또는 2D(코너/끝단) 분류
  - 분류 기준: 인근 버텍스의 방향 각도 변화
  - 2D 분류 버텍스: 특수 처리 (2D 타겟 적용)

3단계: 타겟 포인트 배치
  - 각 버텍스에 웨이퍼 상 타겟 CD 할당
  - 버텍스 방향에 직교하는 평가 방향 정의

4단계: 커브형 이동 최적화
  - 각 버텍스를 임의 방향으로 이동하여 EPE 최소화
  - 이동 제약: 최대 이동 거리 (±d_max)
  - 이웃 버텍스 간 스무딩: 곡선 부드러움 유지

5단계: MRC(Mask Rule Check) 검증
  - 커브형 마스크의 마스크 제조 규칙 검사
  - 최소 feature 크기, 최소 곡률 반경 등
  - 위반 시 형상 단순화 후 재최적화
```

### 공정 윈도우 개선 결과
```
Manhattan OPC vs. 커브형 OPC 비교 (EUV 레이어):
  공정 윈도우 (DOF × EL):
    Manhattan: 기준
    커브형: 유의미한 개선 (수 % ~ 수십 %)

  PV 밴드:
    Manhattan: 기준
    커브형: 감소 (공정 변동 내성 향상)

  MEEF:
    Manhattan: 기준
    커브형: 감소 (마스크 오차 민감도 완화)

최대 효과 패턴:
  - 라인-엔드(line-end) 패턴
  - 2D 직교 구조 (T-junction, 코너)
  - EUV/ArFi 저 k1 패턴
```

## OPC 툴 구현 관련성
- **SKOPC 커브형 확장**: `skopc/core/` 엣지 기반 OPC 엔진을 버텍스 기반으로 일반화
- **버텍스 표현**: `skopc/core/mask_shapes.py` (신규) 커브형 다각형 표현 클래스
- **MBMW 출력**: 커브형 마스크를 MBMW 호환 포맷(OASIS, GDS-II 커브 확장)으로 출력
- **MRC 커브형**: `skopc/core/drc.py`에 커브형 마스크 전용 MRC 규칙 추가

## 참고문헌
- Proc. SPIE 12495, Optical Microlithography XXXVI (2023)
- J. Micro/Nanopatterning, Materials, and Metrology 23(1), 011203 (2024)
- 관련: Why the mask world is moving to curvilinear (SPIE 12954, 2024)
- 관련: Affordable OPC runtime for EUV curvilinear mask tape-out flow (SPIE 12954, 2024)
- 관련: Curvilinear masks: an overview (SPIE 11855, 2021)

## 태그
`Recipe`, `SPIE`, `CurvilinearMask`, `CurvilinearOPC`, `Manhattan`, `VertexBased`, `ILT`, `MBMW`, `ProcessWindow`, `MEEF`, `EUV`, `2023`
