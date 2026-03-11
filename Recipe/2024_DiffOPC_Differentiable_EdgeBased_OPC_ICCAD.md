# Differentiable Edge-Based OPC (DiffOPC)

## 메타데이터
- **저자**: Guojin Chen, Haoyu Yang, Haoxing Ren, Bei Yu, David Z. Pan
- **연도**: 2024
- **게재지**: Proceedings of ICCAD 2024 (43rd IEEE/ACM International Conference on Computer-Aided Design)
- **DOI/URL**: https://doi.org/10.1145/3676536.3676764; arXiv:2408.08969
- **인용수**: ~10

## 핵심 요약
엣지 기반 OPC(Edge-based OPC)와 ILT(Inverse Lithography)의 장점을 모두 활용하는 미분 가능(differentiable) OPC 프레임워크 DiffOPC를 제안한다. 마스크 엣지 세그먼트의 이동을 비용 함수로부터 진짜 기울기(true gradient)로 직접 안내함으로써, 기존 엣지 기반 OPC의 수렴 문제를 해결한다. CUDA 가속 미분 가능 래스터화(rasterization)와 새로운 SRAF 시드 생성 알고리즘을 결합하여 SOTA OPC 대비 EPE를 낮추면서 마스크 제조 비용을 절반으로 줄인다.

## 주요 기여
1. 엣지 세그먼트 이동을 진짜 기울기로 안내하는 미분 가능 엣지 기반 OPC
2. CUDA 가속 미분 가능 래스터화 (레이 캐스팅 기반)
3. 새로운 SRAF 시드 생성 알고리즘
4. 기존 SOTA 대비 EPE ↓, 마스크 제조 비용 50% 감소

## Recipe/Process Flow 상세

### 엣지 기반 OPC vs ILT의 트레이드오프
```
엣지 기반 MB-OPC:
  마스크: 다각형 엣지 세그먼트로 표현
  최적화: 각 세그먼트를 독립적으로 이동
    δ_seg = -sign(∂L/∂δ_seg) 또는 정해진 스텝
  장점: 제조 가능한 마스크 (Manhattan 또는 커비리니어)
  단점:
    근사 기울기 사용 (true gradient 아님)
    세그먼트 간 상관관계 무시
    수렴 느림 또는 국소 최적

ILT (Pixel-based):
  마스크: 픽셀 값으로 표현
  최적화: ∂L/∂M_pixel 진짜 기울기 사용
  장점: 전역 최적화, 높은 인쇄 가능성
  단점: 제조 불가능 형상, MRC 위반 가능성

DiffOPC 목표:
  엣지 기반의 제조 가능성 + ILT의 진짜 기울기
  → 엣지 파라미터에 대한 진짜 기울기 계산
  → 엣지 이동을 최적 방향으로 안내
```

### 미분 가능 래스터화 (CUDA 가속)
```
래스터화 문제:
  다각형 엣지 → 픽셀 마스크 변환
  기존: 불연속 → 기울기 소실

미분 가능 래스터화 (레이 캐스팅):
  다각형 내부 판별: 레이 캐스팅 알고리즘
    점 P → 수평 레이 → 교차 횟수 → 내부/외부 판단
  미분 가능 근사:
    M(P) = sigmoid(signed_distance(P, polygon) / τ)
    signed_distance: 부호 있는 거리 함수
    τ: 연화(softening) 온도 파라미터
  기울기:
    ∂M/∂segment_params = ∂M/∂signed_distance × ∂signed_distance/∂params

CUDA 병렬화:
  픽셀별 병렬 처리: 수만 픽셀 동시 계산
  레이 캐스팅 CUDA 커널: 고속 다각형 내부 판별
  → 래스터화 + 기울기 계산 ms 단위 완료
```

### DiffOPC 최적화 흐름
```
마스크 표현:
  다각형 엣지 세그먼트: {(x1_s, y1_s, x2_s, y2_s)} for s in segments
  엣지 이동 변수: δ_s (수직 변위)

최적화 루프:
  1. 엣지 파라미터 → CUDA 래스터화 → 픽셀 마스크 M
  2. TorchLitho → 항공 이미지 I(M)
  3. 비용 함수: L = L_EPE + λ_MRC × L_MRC
  4. 역전파: ∂L/∂δ_s = ∂L/∂I × ∂I/∂M × ∂M/∂δ_s
  5. 엣지 이동: δ_s ← δ_s - lr × ∂L/∂δ_s
  6. MRC 강제: 이동 후 MRC 위반 시 클리핑
  반복 수렴까지

MRC 통합:
  L_MRC: 미분 가능 형태학적 연산 (에로전/딜레이션) 기반
  또는: 이동 범위 제약 (각 세그먼트 최대 이동 클리핑)
```

### SRAF 시드 생성
```
기존 SRAF 삽입:
  규칙 테이블: (Space, Width) → SRAF 위치/크기
  Model-based: ILT 또는 리소그래피 시뮬로 최적 위치 탐색

DiffOPC SRAF 시드 생성:
  항공 이미지의 부분 이미지 분석:
    주 패턴 사이 공간의 이미지 강도 분포 분석
  SRAF 시드: 이미지 강도가 특정 임계값 이하인 위치
  시드 → 초기 SRAF 다각형 (작은 직사각형)
  → DiffOPC 최적화 루프에서 SRAF 크기/위치 정밀 조정

SRAF 인쇄 방지 제약:
  SRAF 강도가 레지스트 임계값 초과 시 페널티
  → SRAF가 웨이퍼에 인쇄되지 않도록 강제
```

### 성능 결과
```
기준: 기존 SOTA OPC (Calibre 스타일 엣지 기반 OPC)

EPE (Edge Placement Error):
  DiffOPC: SOTA 대비 낮은 EPE
  특히 복잡한 2D 패턴에서 개선

마스크 제조 비용:
  DiffOPC: SOTA 대비 50% 감소
  (마스크 복잡도, 엣지 수, 코너 수 기반 비용 지표)

픽셀-엣지 갭 해소:
  DiffOPC: 픽셀 기반 OPC(ILT) 정확도 + 엣지 기반 제조 가능성 결합
  → 산업 채택 가능한 고정밀 OPC
```

## OPC 툴 구현 관련성
- **SKOPC DiffOPC 엔진**: `skopc/modeling/mb_opc.py`에 DiffOPC 기울기 기반 세그먼트 이동 통합
- **미분 가능 래스터화**: TorchLitho + CUDA 래스터화로 엣지 → 픽셀 → 이미지 → 기울기 파이프라인
- **SRAF 최적화**: DiffOPC SRAF 시드 생성 + 미분 가능 최적화로 SRAF 품질 향상
- **MRC 통합**: 미분 가능 형태학적 연산으로 OPC 최적화 중 MRC 강제

## 참고문헌
- ICCAD 2024; arXiv:2408.08969 (August 2024)
- 저자 소속: CUHK + NVIDIA + UT Austin
- GitHub 슬라이드: https://www.cse.cuhk.edu.hk/~byu/papers/C240-ICCAD2024-DiffOPC-slides.pdf
- 관련: TorchLitho (SPIE 12954, 2024)
- 관련: Neural-ILT (ICCAD 2020 / TCAD 2022)
- 관련: GPU-ILT curvilinear (ISPD 2025)

## 태그
`Recipe`, `ICCAD`, `OPC`, `DifferentiableOPC`, `EdgeBasedOPC`, `SRAF`, `CUDA`, `Rasterization`, `MaskManufacturability`, `EPE`, `CUHK`, `BeiYu`, `NVIDIA`, `2024`
