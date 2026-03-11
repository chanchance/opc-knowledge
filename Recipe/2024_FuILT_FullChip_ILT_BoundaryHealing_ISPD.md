# FuILT: Full Chip ILT System With Boundary Healing

## 메타데이터
- **저자**: Shuo Yin, Wenqian Zhao, Xiaoxiao Liang, Guojin Chen, Yuzhe Ma, Martin D.F. Wong (HKUST)
- **연도**: 2024
- **게재지**: Proceedings of ISPD 2024 (International Symposium on Physical Design)
- **DOI/URL**: https://doi.org/10.1145/3626184.3633315
- **인용수**: ~10

## 핵심 요약
전체 칩 ILT(Inverse Lithography Technology) 마스크 최적화 시스템 FuILT를 제안한다. 다중 레벨 분할(multi-level partitioning) 전략으로 전체 칩을 타일로 분해하고, 다중 GPU 병렬 처리로 각 타일을 독립적으로 최적화한 뒤, 경계 치유(boundary healing) 기법으로 타일 경계의 최적화 불일치를 해결한다. 실제 칩 설계의 다양한 레이어에서 효과적이고 일반화 가능한 전체 칩 ILT 시스템을 구현한다.

## 주요 기여
1. 전체 칩 ILT를 위한 다중 레벨 분할 + 분할 정복 전략
2. 다중 GPU 병렬 처리로 확장 가능한 작업 분산 프레임워크
3. 기울기 융합(gradient-fusion) + 다중 레벨 경계 치유 기법
4. 실제 설계 레이어에서 효과적이고 일반화 가능한 전체 칩 ILT 시스템

## Recipe/Process Flow 상세

### 전체 칩 ILT의 과제
```
단일 클립 ILT:
  한 번에 최적화하는 패턴 크기: ~수 μm × 수 μm
  속도: 클립당 수 초~수 분
  품질: 높은 인쇄 가능성

전체 칩 ILT 과제:
  현대 칩 면적: 수백 mm²
  직접 전체 칩 ILT: 메모리 + 계산 불가능
  필요 전략:
    분할 + 병렬 최적화
    타일 경계 불일치 해결

경계 불일치 문제:
  타일 독립 최적화:
    타일 A, 타일 B: 각자 최적 마스크 생성
    경계에서: A의 마스크 ≠ B의 마스크 예상
    → 스티칭 불일치 → 인쇄 오류
  FuILT: 경계 치유(Boundary Healing)로 해결
```

### 다중 레벨 분할 전략
```
레벨 1: 칩-블록 분할
  전체 칩 → 독립 블록 (회로 계층 기반)
  각 블록: 타일로 추가 분할

레벨 2: 블록-타일 분할
  각 블록 → 겹침(overlap) 있는 타일
  타일 크기: ILT 최적화 단위 (수 μm)
  겹침: 경계 치유에 사용

레벨 3: 타일 내 최적화
  각 타일: GPU ILT 최적화 독립 수행
  GPU 병렬: 다수 타일 동시 최적화

분할 고려사항:
  OPC 근접 효과 범위(proximity range)보다 큰 겹침 필요
  타일 크기-수 균형: GPU 메모리 vs. 병렬화 효율
```

### 경계 치유 (Boundary Healing)
```
경계 불일치 감지:
  인접 타일 경계에서 마스크 불일치 측정:
    δM_boundary = |M_tile_A - M_tile_B| at boundary
  임계값 초과 시 치유 필요

기울기 융합 (Gradient Fusion):
  타일 A, B 경계 근방:
    g_A = ∂L_A/∂M (타일 A 기울기)
    g_B = ∂L_B/∂M (타일 B 기울기)
  융합 기울기: g_fused = α × g_A + (1-α) × g_B
  → 경계 마스크를 양쪽 최적 방향으로 동시 유도

다중 레벨 치유:
  레벨 1: 타일 경계 즉각 치유 (작은 불일치)
  레벨 2: 블록 경계 재최적화 (큰 불일치)
  레벨 3: 칩 레벨 검증 + 나머지 불일치 보정

스티칭(Stitching) 후 치유:
  모든 타일 최적화 완료 후:
    경계 영역 추출 → 재최적화
    양쪽 타일 마스크 기울기 동시 사용
    → 수렴까지 반복
```

### 다중 GPU 병렬화
```
작업 분산:
  타일 풀 → GPU 큐
  각 GPU: 타일 가져와 ILT 최적화
  비동기 처리: GPU 간 통신 없이 독립 최적화

GPU 메모리 관리:
  타일 크기 × 배치 수 = GPU 메모리에 맞게 조정
  동적 배치 크기: GPU 유휴 시간 최소화

경계 치유 GPU 처리:
  경계 타일 쌍 → 경계 영역 병렬 재최적화
  GPU 간 경계 마스크 공유 (minimal communication)
```

### 성능 결과
```
전체 칩 ILT 달성:
  실제 설계 다수 레이어 (Metal, Contact, Via) 적용
  경계 치유로 스티칭 불일치 크게 감소

품질:
  단일 타일 ILT와 동등한 인쇄 가능성
  경계 영역 EPE: 치유 후 내부와 동등 수준

속도:
  다중 GPU 선형 확장: N GPU → ~N× 가속
  전체 칩 처리: 실용적 TAT
```

## OPC 툴 구현 관련성
- **SKOPC 전체 칩 ILT**: `skopc/modeling/openilt_adapter.py`에 FuILT 전체 칩 분할 전략 통합
- **타일 분할**: 레이아웃 DB에서 OPC 근접 효과 범위 기반 자동 타일 분할
- **경계 치유**: 인접 타일 최적화 결과 스티칭 + 기울기 융합 치유
- **다중 GPU**: SKOPC 배치 처리에 FuILT 다중 GPU 작업 분산 적용

## 참고문헌
- ISPD 2024; PDF: http://www.cse.cuhk.edu.hk/~byu/papers/C203-ISPD2024-FuILT.pdf
- 저자 소속: HKUST (Martin D.F. Wong 그룹)
- 관련: DevelSet (ICCAD 2021 / TCAD 2023)
- 관련: GPU-ILT Curvilinear (ISPD 2025)
- 관련: L2O-ILT (TCAD 2024)

## 태그
`Recipe`, `ISPD`, `ILT`, `FullChip`, `BoundaryHealing`, `MultiGPU`, `Partitioning`, `MaskOptimization`, `GradientFusion`, `Stitching`, `HKUST`, `2024`
