# Curvilinear Sub-Resolution Assist Feature Placement Through a Data-Driven U-Net Model

## 메타데이터
- **저자**: Li et al.
- **연도**: 2025
- **게재지/학회**: MDPI Micromachines, Volume 16, Issue 11, Special Issue: Recent Advances in Lithography
- **DOI/URL**: https://www.mdpi.com/2072-666X/16/11/1229
- **PMC**: https://pmc.ncbi.nlm.nih.gov/articles/PMC12654570/

## 핵심 요약
곡선형(Curvilinear) SRAF(Sub-Resolution Assist Feature) 배치를 위한 데이터 기반 U-Net 프레임워크를 제안한다. 기존 규칙 기반 SRAF는 직선형 기하학에만 적합하여 첨단 노드의 복잡한 곡선형 레이아웃에서 성능이 제한된다. 이 방법은 조잡한 이진화 SRAF 패턴을 입력으로 받아 광학적으로 최적화된 곡선형 SRAF 출력을 생성하는 CNN을 학습시켜, 전통 CPU 기반 방법 대비 수 배의 속도 향상을 달성하면서 레벨셋 방법(LSM)과 동등한 패턴 충실도를 확보한다.

## 주요 기여
- **곡선형 SRAF 데이터 기반 최적화**: 직선형 한계를 극복하는 U-Net 기반 SRAF 형상 최적화
- **대규모 데이터셋 구축**: 조잡한 SRAF 입력 → 광학 최적화 SRAF 출력 쌍 데이터셋
- **멀티 오더급 속도 향상**: 전통 CPU 방법 대비 수 배 가속, GPU 방법 대비 우위
- **LSM 수준 패턴 충실도**: 계산 비용이 높은 레벨셋 방법과 동등한 정밀도

## Recipe/Process Flow 상세

### 곡선형 SRAF U-Net 파이프라인

```
입력:
  레이아웃 패턴 (메인 피처)
        ↓
[초기 규칙 기반 SRAF 배치 (RB-SRAF)]
  - 전통 간격 테이블로 직선형 SRAF 생성
  - 이진화된 조잡한 SRAF 맵 생성
  → 이 결과가 U-Net 입력
        ↓
[U-Net SRAF 형상 최적화]
  ┌──────────────────────────────┐
  │     U-Net 아키텍처           │
  │  인코더 (다운샘플링):         │
  │    Conv → BN → ReLU × 4    │
  │    특징 맵: 64→128→256→512 │
  │                              │
  │  보틀넥:                     │
  │    512채널 특징 추출          │
  │                              │
  │  디코더 (업샘플링):           │
  │    Upconv + Skip connection │
  │    512→256→128→64          │
  │                              │
  │  출력: 곡선형 SRAF 확률 맵   │
  └──────────────────────────────┘
        ↓
[곡선형 SRAF 마스크 생성]
  - 확률 맵 임계값 처리
  - 메인 피처와 SRAF 결합
        ↓
최종 OPC 마스크 (메인 피처 + 곡선형 SRAF)
```

### 전통 SRAF vs 곡선형 SRAF 비교

```
규칙 기반 SRAF (RB-SRAF):
  장점: 빠른 처리, 구현 용이
  단점: 직선형 기하학 한정
        첨단 노드에서 성능 저하
        곡선형 레이아웃 부적합

모델 기반 SRAF (MB-SRAF):
  장점: 더 나은 패턴 품질
  단점: 계산 집약적
        공정 변이 반영 제한적

레벨셋 방법 (LSM) SRAF:
  장점: 최고 품질 곡선형 SRAF
  단점: 매우 느린 처리 속도
        풀칩 스케일 부적합

U-Net 곡선형 SRAF (본 논문):
  장점: LSM 수준 품질
        CPU 방법 대비 멀티 오더 속도 향상
        GPU 가속 방법 대비 우위
  단점: 학습 데이터 필요
        일반화 한계 (분포 외 패턴)
```

### U-Net 학습 데이터셋 구성

```
데이터셋 구조:
  입력: 조잡한 이진화 SRAF 맵 (규칙 기반 초기 배치)
  출력: 광학 최적화 곡선형 SRAF 맵 (LSM 정답)

데이터 생성 파이프라인:
  1. 다양한 레이아웃 패턴 수집 (라인/스페이스, 2D 피처 등)
  2. 규칙 기반 SRAF 초기 배치 → 입력 데이터
  3. LSM 최적화 SRAF 계산 → 라벨 데이터
  4. 입출력 쌍으로 데이터셋 구성

학습 설정:
  - 손실함수: BCE (Binary Cross-Entropy) + SSIM 조합
  - 최적화기: Adam (lr=1e-4)
  - 배치 크기: 16~32
  - 에폭: 100~200

데이터 증강:
  - 회전 (90°, 180°, 270°)
  - 수평/수직 플립
  - 랜덤 크롭
```

### 성능 평가 지표

```
패턴 품질 지표:
  - PVBand: 공정 변동 밴드 면적
  - EPE: 엣지 배치 오차
  - SRAF 형상 정확도 (LSM 대비)

속도 지표:
  - CPU LSM 대비 속도 향상: 수 배 이상
  - GPU 가속 방법 대비: 동등 이상

비교 방법:
  1. 규칙 기반 SRAF (기준선)
  2. CPU 기반 LSM SRAF (품질 기준)
  3. GPU 가속 SRAF 최적화
  4. U-Net 곡선형 SRAF (제안 방법)
```

### 첨단 노드에서의 SRAF 중요성

```
기술 노드별 SRAF 요구사항:

≥65nm: 규칙 기반 SRAF로 충분
        직선형 SRAF 유효

28-45nm: 모델 기반 SRAF 도입
          일부 곡선형 필요

≤16nm: 곡선형 SRAF 필수
        공정 윈도우 확보에 결정적
        ILT와 통합 최적화

EUV (≤7nm): 고도화된 곡선형 SRAF
              stochastic 효과 보상
              3D 마스크 효과 고려
```

## OPC 툴 구현 관련성
Curvilinear SRAF U-Net은 SKOPC의 SRAF 배치 모듈에 직접 적용 가능:
- **SRAF 모듈 통합**: `skopc/modeling/sraf_placement.py`에 U-Net 기반 SRAF 배치 추가
- **곡선형 마스크 지원**: SKOPC의 SRAF가 직선형 한계를 극복하여 첨단 노드 지원
- **OpenILT 연동**: OpenILT의 SRAF 모듈에 U-Net 플러그인으로 통합
- **레시피 파라미터**: SRAF 규칙 테이블을 U-Net 모델 경로 파라미터로 대체하는 레시피 스키마 설계
- **GNN-OPC 보완**: GNN-OPC 마스크 최적화 후 U-Net SRAF를 추가 삽입하는 2단계 파이프라인

## 참고문헌 (핵심)
- Yang et al., "GAN-OPC" (DAC 2018) - SRAF + 마스크 공동 최적화 선행 연구
- OpenILT SRAF 모듈 (ASICON 2023)
- RuleLearner for SRAF (IEEE TCAD 2025) - 자동 SRAF 규칙 추출
- Level Set Method for SRAF - 품질 기준선
- U-Net 기반 SRAF 배치 선행 연구 (SPIE 2021)

## 태그
`Curvilinear SRAF`, `U-Net`, `Data-Driven`, `Sub-Resolution Assist Feature`, `Deep Learning`, `MDPI Micromachines`, `2025`, `Advanced Node`, `Lithography`, `Pattern Fidelity`, `Level Set Method`, `GPU Acceleration`
