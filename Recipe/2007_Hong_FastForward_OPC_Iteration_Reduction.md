# A Generic Technique for Reducing OPC Iteration: Fast Forward OPC

## 메타데이터
- **저자**: Le Hong, John L. Sturtevant
- **연도**: 2007
- **게재지**: Proc. SPIE 6730, Photomask Technology 2007, 67302M
- **DOI/URL**: https://doi.org/10.1117/12.746757
- **인용수**: ~40

## 핵심 요약
OPC는 단일 시뮬레이션과 폴리곤 단편화 이동 시퀀스를 하나의 이터레이션으로 하는 반복 사이클로, 정확한 OPC 레시피는 통상 8회 이상 이터레이션이 필요하다. Fast Forward OPC(FFOPC)는 특정 조건을 충족하는 임의의 Golden OPC 레시피를 최소 정확도 손실로 고정 4회 이터레이션으로 축소하는 범용 기법이다. 이는 테이프아웃 과정에서 가장 계산 비용이 높은 OPC 단계의 런타임을 대폭 단축한다.

## 주요 기여
1. Golden OPC 레시피를 4회 고정 이터레이션으로 압축하는 범용 알고리즘
2. 최소 정확도 손실 보장 조건 수학적 정형화
3. 전체 칩 OPC 런타임의 ~50% 감소 달성
4. 다양한 레이어 유형(게이트, 금속, 비아)에 적용 가능한 일반성

## Recipe/Process Flow 상세

### 기존 OPC 이터레이션 구조
```
이터레이션 1: 초기 마스크 → 시뮬레이션 → EPE 측정 → 보정 적용
이터레이션 2: 업데이트 마스크 → 시뮬레이션 → EPE 측정 → 보정 적용
...
이터레이션 N: ... → 수렴 (N ≥ 8)

문제점:
- 각 이터레이션: 1회 전체 칩 리소그래피 시뮬레이션
- 총 런타임 = N × (단일 이터레이션 시간)
- N=8 → 런타임 병목
```

### Fast Forward OPC 알고리즘
```
1. Golden 레시피 분석 (오프라인)
   - 기준 레시피(N 이터레이션)의 수렴 거동 분석
   - 각 이터레이션에서의 EPE 감소 곡선 특성 파악
   - 수렴 가속 가능한 이터레이션 구간 식별

2. 이터레이션 압축 조건 확인
   조건 1: 레시피가 안정적 수렴 거동 보임
   조건 2: 초기 몇 이터레이션에서 대부분의 EPE 감소 발생
   조건 3: 잔여 이터레이션은 미세 조정 (fine-tuning)

3. 압축 알고리즘 (4 이터레이션으로)
   이터레이션 1: 보정량 스케일 팩터 α1 > 1 (가속 보정)
   이터레이션 2: 보정량 스케일 팩터 α2 (조정)
   이터레이션 3: 보정량 스케일 팩터 α3
   이터레이션 4: 최종 수렴 보정 (αN과 유사)

   → αi는 Golden 레시피의 EPE 감소 곡선에서 수치 최적화로 결정

4. 검증 (온라인)
   - 압축 레시피(4회)로 OPC 수행
   - Golden 레시피(N회) 결과와 EPE 비교
   - 허용 오차 내 일치 확인
```

### 성능 결과
```
이터레이션 감소: N → 4 (N=8 기준 50% 감소, N=12 기준 67% 감소)
EPE 정확도: Golden 레시피 대비 최소 손실 (< 0.5nm RMS EPE 차이)
런타임: 비례적 감소 (~50~67% 단축)
적용 레이어: 게이트 레이어, 금속 레이어, 비아 레이어 검증
```

### 레시피 조건 (FFOPC 적용 가능 기준)
- 레시피가 단조 감소(monotonic decrease) EPE 수렴 보임
- 발산 없는 안정적 수렴 특성
- MEEF(Mask Error Enhancement Factor)가 과도하게 높지 않은 패턴

## OPC 툴 구현 관련성
- **SKOPC 수렴 가속**: `skopc/modeling/model_opc.py`의 이터레이션 루프에 FFOPC 스케일 팩터 적용 가능
- **레시피 파라미터**: α1, α2, α3, α4 스케일 팩터를 레시피 YAML에 정의 가능
- **런타임 목표**: 전체 칩 OPC 시간 50% 이상 단축을 위한 핵심 기법
- **Mentor Graphics 출처**: Calibre OPC의 이론적 기반 중 하나

## 참고문헌
- Proc. SPIE 6730, Photomask Technology 2007
- 저자 소속: Mentor Graphics Corp.
- 관련: Classical control theory applied to OPC convergence (SPIE, 2004)
- 관련: Managing high-accuracy and fast convergence in OPC (SPIE, 2006)

## 태그
`Recipe`, `SPIE`, `ModelBasedOPC`, `IterationReduction`, `FastOPC`, `Runtime`, `ConvergenceAcceleration`, `GoldenRecipe`, `MentorGraphics`
