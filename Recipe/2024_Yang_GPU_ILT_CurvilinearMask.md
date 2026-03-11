# GPU-Accelerated Inverse Lithography Towards High Quality Curvy Mask Generation

## 메타데이터
- **저자**: Haoyu Yang, Haoxing Ren
- **연도**: 2024 (게재: ISPD 2025)
- **게재지/학회**: International Symposium on Physical Design (ISPD) 2025, Austin TX
- **DOI/URL**: https://arxiv.org/abs/2411.07311
- **인용수**: N/A (2025 발표 예정)

## 핵심 요약
본 논문은 GPU 병렬 컴퓨팅을 활용하여 역리소그래피 기술(ILT)의 커빌리니어(곡선형) 마스크 생성 속도와 품질을 동시에 향상시키는 알고리즘을 제시한다. 멀티빔 마스크 라이터의 상용화로 커빌리니어 마스크 직접 제조가 가능해진 현 시점에서, GPU 가속 ILT는 기존 학술 ILT 엔진 대비 유의미한 윤곽 품질, 공정 윈도우, 마스크 형상 정밀도 향상을 보인다. NVIDIA 연구팀(cuLitho 프로젝트의 연속선)의 결과물이다.

## 주요 기여
- **GPU 가속 ILT 알고리즘**: GPU 코어 병렬화로 기존 CPU 기반 ILT 대비 대규모 연산 공간 탐색
- **커빌리니어 마스크 품질 향상**: e-빔 샷 수 감소가 아닌 마스크 복잡도 관리에 초점
- **공정 윈도우 개선**: 선도적 학술 ILT 엔진 대비 우수한 공정 윈도우 성능
- **제조 가능성 확보**: 멀티빔 마스크 라이터와의 호환성을 통한 직접 제조 가능

## Recipe/Process Flow 상세

### ILT 기반 마스크 최적화 플로우

```
설계 레이아웃 입력
        ↓
[리소그래피 시스템 모델링]
  - 조명 설정 (부분 간섭성, 조명 형상)
  - 투영 광학계 (NA, 수차)
  - 레지스트 모델 (임계값, 확산)
        ↓
[역문제(Inverse Problem) 정식화]
  목적 함수: min_M ||I(M) - T||² + R(M)
  - I(M): 마스크 M의 리소그래피 이미징 함수
  - T: 타겟 웨이퍼 패턴
  - R(M): 마스크 복잡도 정규화 항
        ↓
[GPU 가속 그래디언트 최적화]
  - 순방향: M → 공중 이미지 → 레지스트 윤곽
  - 역방향: 손실 → 그래디언트 → 마스크 업데이트
  - GPU 병렬화: 타일 단위 병렬 처리
        ↓
[커빌리니어 마스크 형상 생성]
  - 이진화: 연속 마스크 → 곡선형 이진 마스크
  - MRC 검사: 제조 가능성 규칙 확인
        ↓
최적화된 커빌리니어 포토마스크
```

### GPU 병렬화 전략
- **타일 병렬 처리**: 전체 칩 레이아웃을 타일로 분할하여 GPU 코어에 분배
- **배치 최적화**: 다수의 마스크 타일 동시 최적화
- **메모리 최적화**: GPU 메모리 계층 구조 활용으로 데이터 이동 최소화
- **커널 퓨전**: 연속된 연산을 단일 GPU 커널로 통합

### 커빌리니어 마스크 생성 특징
- 멀티빔 마스크 라이터(Multi-beam Mask Writer)와 직접 호환
- 전통 맨해튼 기하학적 마스크 대비 더 넓은 최적화 공간
- 복잡한 2D 패턴에서 특히 우수한 인쇄 품질
- 제조 일관성 유지를 위한 마스크 복잡도 관리

### 성능 비교 (벤치마크)
- 선도적 학술 ILT 엔진 대비 유의미한 성능 우위
- 윤곽 품질(Contour Quality), 공정 윈도우(Process Window), 마스크 형상 정밀도 모두 향상

## OPC 툴 구현 관련성
SKOPC의 고급 OPC 기능 구현에 활용 가능:
- **cuLitho 연동**: NVIDIA cuLitho API를 통한 GPU 가속 ILT 기능 통합
- **커빌리니어 마스크 지원**: SKOPC 레이아웃 에디터에서 커빌리니어 폴리곤 지원 확장
- **EUV OPC 적용**: EUV 고 NA 리소그래피에서의 커빌리니어 마스크 레시피 개발
- **GPU 가속 시뮬레이션**: `litho_engine.py`의 Hopkins 계산을 CUDA로 가속하는 구현 참조

## 참고문헌 (핵심)
- Yang et al., "NVIDIA cuLitho: Computational Lithography Acceleration" (2023)
- Chen et al., "DiffOPC: Differentiable Edge-based OPC" (ICCAD 2024)
- Granik, "Fast Pixel-Based Mask Optimization for Inverse Lithography" (JM3 2006)
- Peng et al., "Illumination Source Optimization in Optical Lithography" (2011)

## 태그
`ILT`, `GPU Acceleration`, `Curvilinear Mask`, `NVIDIA`, `cuLitho`, `Process Window`, `ISPD 2025`, `2024`, `Inverse Lithography`, `Multi-beam Mask Writer`
