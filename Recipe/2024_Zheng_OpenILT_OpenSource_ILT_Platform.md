# OpenILT: An Open Source Inverse Lithography Technique Framework + Model-Based OPC Extension

## 메타데이터
- **저자**: Su Zheng, Ziyang Yu, et al. (CUHK, Bei Yu 연구그룹)
- **연도**: 2023 (ASICON 2023 최초 발표) / 2024 (ISEDA 2024 MB-OPC 확장)
- **게재지/학회**: ASICON 2023 (IEEE) + ISEDA 2024 (MB-OPC 확장)
- **DOI/URL**: https://github.com/OpenOPC/OpenILT / https://ieeexplore.ieee.org/document/10396314/
- **오픈소스**: https://github.com/OpenOPC/OpenILT (Apache 2.0)

## 핵심 요약
OpenILT는 역리소그래피 기술(ILT) 연구를 위한 GPU 가속 오픈소스 플랫폼으로, 다양한 ILT 방법의 빠른 개발 및 평가를 지원한다. 리소그래피 시뮬레이션, 목적 함수, 평가 지표 등 다양한 ILT 구성 요소를 통합하는 모듈식 유연한 프레임워크를 제공한다. ISEDA 2024에서 MB-OPC 확장이 발표되어 대형 레이아웃 리소그래피 시뮬레이션 제한을 해결하고, GPU 가속으로 5배 이상의 속도 향상을 달성한다.

## 주요 기여

### OpenILT 기본 프레임워크 (ASICON 2023)
- **GPU 가속 ILT**: CUDA 기반 GPU 병렬 처리로 ILT 연산 가속
- **모듈식 아키텍처**: 리소그래피 모델, 목적 함수, 평가 지표 독립 교체 가능
- **다중 ILT 방법 지원**: 수치 ILT, Neural-ILT, DevelSet 등 통합 지원
- **오픈소스 공개**: 재현 가능한 ILT 연구 환경 제공

### MB-OPC 확장 (ISEDA 2024)
- **대형 레이아웃 지원**: 기존 OpenILT의 레이아웃 크기 제한 해결
- **모델 기반 OPC 구현**: OpenILT에 MB-OPC 기능 추가
- **5배+ 속도 향상**: GPU 가속으로 OPC 처리 속도 대폭 향상
- **유연한 OPC 알고리즘 개발 플랫폼**: 새 OPC 기법 구현 및 평가 용이

## Recipe/Process Flow 상세

### OpenILT 모듈식 아키텍처

```
OpenILT 프레임워크 구조:

[리소그래피 시뮬레이션 모듈]
  ├── Hopkins/Abbe 이미징 모델 (GPU 가속)
  ├── SOCS 근사 (Sum of Coherent Systems)
  ├── 레지스트 모델 (임계값, 확산)
  └── TorchLitho 통합 (미분 가능)

[목적 함수 모듈]
  ├── L2/L1 손실 (인쇄 품질)
  ├── EPE 기반 손실
  ├── PVB (공정 변동 밴드)
  ├── 마스크 복잡도 정규화 (L1, TV 노름)
  └── 사용자 정의 손실 지원

[최적화 모듈]
  ├── 수치 ILT (경사 하강, L-BFGS)
  ├── Neural-ILT 통합
  ├── DevelSet 통합
  ├── DiffOPC 통합
  └── 사용자 정의 최적화기 플러그인

[평가 지표 모듈]
  ├── EPE (Edge Placement Error)
  ├── PVB (Process Variation Band)
  ├── 핫스팟 검출
  ├── 마스크 복잡도 (e-beam 샷 수)
  └── 리소그래피 충실도 지표
```

### MB-OPC 확장 플로우 (ISEDA 2024)

```
대형 레이아웃 입력 (풀칩 스케일)
        ↓
[레이아웃 분할 (Layout Partitioning)]
  - 대형 레이아웃을 처리 가능한 타일로 분할
  - 오버랩 마진으로 경계 아티팩트 방지
  - 타일 크기: GPU 메모리에 최적화
        ↓
[GPU 가속 MB-OPC 처리]
  각 타일에 대해 병렬 GPU 처리:
  ┌─────────────────────────────┐
  │ 타일 리소그래피 시뮬레이션  │
  │ (GPU 가속 Hopkins 모델)    │
  │           ↓                 │
  │ 세그먼트 분할 및 이동       │
  │ (EBOPC 방식)               │
  │           ↓                 │
  │ EPE 계산 및 수렴 판단       │
  └─────────────────────────────┘
        ↓
[타일 재조합]
  - 오버랩 영역 블렌딩
  - 전체 레이아웃 마스크 재구성
        ↓
최적화된 마스크 출력
```

### 성능 결과 (MB-OPC 확장)
- GPU 가속 속도 향상: 5배 이상 (CPU 기반 대비)
- 지원 레이아웃 크기: 기존 OpenILT 제한 초과 가능
- 모듈식 구현: 새 OPC 알고리즘 추가 용이

### 지원 방법 (OpenILT 생태계)
| 방법 | 유형 | 구현 상태 |
|------|------|---------|
| 수치 ILT | 픽셀/엣지 기반 | 기본 지원 |
| Neural-ILT | DL 기반 | 통합 |
| DevelSet | 레벨 셋 | 통합 |
| L2O-ILT | 알고리즘 전개 | 통합 |
| MB-OPC | 엣지 기반 | 2024 추가 |
| DiffOPC | 미분 가능 | 통합 예정 |

## OPC 툴 구현 관련성
OpenILT는 SKOPC의 직접적인 비교 및 참조 플랫폼:
- **SKOPC vs OpenILT**: 동일 벤치마크에서 SKOPC와 OpenILT 성능 직접 비교 가능
- **모듈 통합**: SKOPC에 OpenILT의 GPU 가속 리소그래피 시뮬레이션 모듈 통합 고려
- **MB-OPC 참조**: OpenILT의 MB-OPC 확장 코드를 SKOPC `model_opc.py` 구현 참조
- **벤치마크 공유**: OpenILT 공개 벤치마크로 SKOPC 성능 객관적 평가
- **오픈소스 기여**: SKOPC를 OpenILT 생태계에 기여하는 방향 고려

## 참고문헌 (핵심)
- Zheng et al., "LithoBench" (NeurIPS 2023)
- Jiang et al., "Neural-ILT" (ICCAD 2020)
- Chen et al., "DevelSet" (ICCAD 2021)
- Chen et al., "DiffOPC" (ICCAD 2024)
- TorchLitho (SPIE 2024)

## 태그
`OpenILT`, `Open Source`, `ILT`, `MB-OPC`, `GPU Acceleration`, `Modular Framework`, `CUHK`, `ASICON 2023`, `ISEDA 2024`, `5x Speedup`, `Large Layout`, `Benchmark Platform`
