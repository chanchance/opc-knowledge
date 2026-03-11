# NVIDIA cuLitho: GPU-Accelerated Computational Lithography Platform

## 메타데이터
- **저자**: NVIDIA, TSMC, Synopsys, ASML (공동 발표)
- **연도**: 2023
- **게재지**: NVIDIA GTC 2023 발표; 기술 백서; Synopsys/TSMC 공동 생산 적용 발표
- **DOI/URL**: https://developer.nvidia.com/culitho
- **인용수**: 산업계 기술 발표 (광범위 인용)

## 핵심 요약
NVIDIA cuLitho는 GPU를 활용하여 OPC, ILT 등 계산 리소그래피 워크로드를 대규모 가속화하는 라이브러리다. 기존 40,000개 CPU 시스템이 2주에 처리하던 포토마스크 작업을 500개의 NVIDIA H100 GPU로 하룻밤에 완료한다. Synopsys Proteus OPC 소프트웨어와 통합되어 TSMC 양산 공정에 적용되었으며, 커브형 OPC, High-NA EUV 등 차세대 리소그래피 기술의 상용화를 가능하게 한다.

## 주요 기여
1. OPC/ILT의 GPU 병렬화로 40× 속도 향상 (CPU 대비)
2. 40,000 CPU → 500 GPU로 인프라 대폭 축소 (1/80 시스템 수)
3. Synopsys Proteus OPC + cuLitho 통합으로 즉시 생산 적용
4. 커브형 ILT/OPC, High-NA EUV 등 차세대 기술 실용화 가속

## Recipe/Process Flow 상세

### 계산 리소그래피의 컴퓨팅 병목
```
OPC/ILT 계산 특성:
  - 전체 칩: 수십억 개 엣지 세그먼트
  - 각 세그먼트: 리소그래피 시뮬레이션 + 보정 계산
  - 핵심 연산: 광학 합성곱 (FFT 기반)
  - 반복 (iterations): 수십 회

기존 CPU 기반 현황:
  - 28nm OPC: ~수십 CPU × 수 시간
  - 7nm OPC: 수천 CPU × 수십 시간
  - EUV ILT: 수만 CPU × 수 주
  - 커브형 ILT: 현실적 불가 (너무 느림)

계산 특성 분석:
  - 대규모 병렬 데이터: 독립적 클립/세그먼트
  - FFT 집약적: GPU에 최적화된 연산
  - 메모리 집약적: 대용량 레이아웃 데이터
  → GPU 병렬화에 이상적
```

### cuLitho 기술 아키텍처
```
cuLitho 핵심 구성:
  1. GPU 가속 리소그래피 시뮬레이션
     - 항공 이미지(aerial image) 계산: CUDA FFT 최적화
     - 레지스트 시뮬레이션: GPU 배치 처리
     - 마스크 렌더링: GPU 래스터화

  2. GPU 가속 OPC/ILT 최적화
     - 병렬 세그먼트 업데이트: SIMD 벡터화
     - 그래디언트 계산: CUDA 커널
     - 멀티-GPU 스케일아웃: NVLink/InfiniBand

  3. Synopsys Proteus 통합
     - Proteus OPC 엔진 → cuLitho API 호출
     - 기존 레시피/워크플로우 호환성 유지
     - CPU/GPU 하이브리드 실행

성능 수치:
  OPC 가속비: ~40× (CPU 대비)
  시스템 효율: 40,000 CPU → 500 H100 GPU
  전력 효율: 1/9 전력 소비
  공간 효율: 1/8 공간 점유
```

### 차세대 리소그래피 기술 가속화
```
커브형 OPC/ILT:
  기존 CPU: 전체 칩 커브형 ILT 수행 불가 (수 주 예상)
  cuLitho: 하룻밤 내 처리 가능
  → 커브형 마스크의 양산 적용 실용화

High-NA EUV (NA=0.55):
  엄밀한 마스크 3D 시뮬레이션 포함 OPC
  더 높은 계산 부하 → GPU 더욱 필요
  cuLitho로 High-NA EUV OPC 런타임 현실화

Stochastic 시뮬레이션:
  EUV 광자 수 제한 노이즈 몬테카를로 시뮬레이션
  기존 CPU: 통계적으로 충분한 샘플 수 불가
  GPU: 대규모 병렬 몬테카를로 가능
```

### 산업계 채택 현황
```
TSMC:
  - cuLitho 기반 OPC를 양산 흐름에 통합 (2023)
  - 2nm 이하 노드를 위한 핵심 인프라로 채택

Synopsys:
  - Proteus OPC의 cuLitho 백엔드 지원
  - 기존 레시피 변경 없이 GPU 가속 자동 활용

ASML:
  - EUV 스캐너 데이터와 cuLitho OPC 통합 검증
  - High-NA EUV OPC 공동 개발

결과:
  - 포토마스크 TAT (Turn-Around-Time): 2주 → 1일
  - 신규 노드 OPC 개발 사이클 대폭 단축
  - 커브형 ILT 양산 가능성 확보
```

## OPC 툴 구현 관련성
- **SKOPC GPU 가속**: `skopc/core/litho_engine.py` 리소그래피 시뮬레이션에 CuPy/CUDA FFT 적용
- **병렬 OPC**: `skopc/modeling/` OPC 이터레이션의 세그먼트 단위 GPU 병렬화
- **TorchLitho 연동**: PyTorch 기반 GPU 리소그래피 시뮬레이션 (cuLitho 오픈소스 대안)
- **스케일아웃**: 멀티-GPU 또는 분산 처리로 전체 칩 OPC 런타임 최적화

## 참고문헌
- NVIDIA GTC 2023 Keynote, Jensen Huang (March 2023)
- TSMC-Synopsys-NVIDIA cuLitho 생산 적용 공동 발표 (2023)
- 관련: GPU accelerated O(p) computing for curvilinear OPC (SPIE 12751, 2023)
- 관련: Advancing the curvilinear ILT and OPC ecosystem (SPIE 12954, 2024)

## 태그
`Recipe`, `Industry`, `GPU`, `cuLitho`, `NVIDIA`, `OPC-Acceleration`, `ComputationalLithography`, `CurvilinearOPC`, `HighNA`, `EUV`, `TSMC`, `Synopsys`, `2023`
