# VLSI Mask Optimization: From Shallow To Deep Learning

## 메타데이터
- **저자**: Haoyu Yang, Wei Zhong, Yuzhe Ma, Hao Geng, Ran Chen, Wanli Chen, Bei Yu
- **연도**: 2020 (arXiv 2019년 12월)
- **게재지/학회**: 25th Asia and South Pacific Design Automation Conference (ASP-DAC 2020)
- **DOI/URL**: https://arxiv.org/abs/1912.07254 / https://ieeexplore.ieee.org/document/9045241/
- **인용수**: 100+

## 핵심 요약
본 논문은 VLSI 마스크 최적화 분야의 기계학습 기법을 천층(shallow) 학습부터 심층(deep) 학습까지 포괄적으로 조망하는 서베이다. 인쇄 가능성 추정을 지원하는 결정론적 ML 모델과 인쇄 가능한 마스크를 직접 합성하는 생성 모델의 최근 발전을 검토한다. 이질적(heterogeneous) OPC 프레임워크를 제안하여 기존 EDA 솔루션의 대안 가능성을 시연하며, VLSI 설계 사이클 가속화를 위한 ML 기법의 효율성과 효과성을 보인다.

## 주요 기여
- **ML 기반 마스크 최적화 체계적 분류**: 천층 학습 → 심층 학습으로의 발전 계통도 제시
- **결정론적 모델 서베이**: 인쇄 가능성 예측, 핫스팟 검출 등 분류/회귀 모델
- **생성 모델 서베이**: GAN, VAE 등 직접 마스크 합성 생성 모델
- **이질적 OPC 프레임워크**: ML과 수치 최적화를 결합한 하이브리드 접근법

## Recipe/Process Flow 상세

### ML 기반 마스크 최적화 분류 체계

```
VLSI 마스크 최적화 ML 기법 분류
        ├── 천층(Shallow) ML 기법
        │     ├── SVM 기반 인쇄 가능성 예측
        │     ├── 랜덤 포레스트 기반 핫스팟 검출
        │     ├── 결정 트리 기반 레이아웃 분류
        │     └── SVM 기반 레이아웃 타겟팅 (역방향 리소그래피 근사)
        │
        └── 심층(Deep) 학습 기법
              ├── 결정론적 모델 (판별기)
              │     ├── CNN 기반 리소그래피 시뮬레이션
              │     ├── FCN 기반 마스크 인쇄 가능성 예측
              │     ├── CNN 기반 핫스팟 검출
              │     └── DNN 기반 레지스트 윤곽 예측
              │
              └── 생성 모델 (생성기)
                    ├── GAN 기반 마스크 생성 (GAN-OPC)
                    ├── cGAN 기반 레이아웃-마스크 변환
                    ├── VAE 기반 마스크 변이 탐색
                    └── 이질적 OPC (결정론 + 생성 혼합)
```

### 이질적 OPC 프레임워크

```
레이아웃 입력
        ↓
[ML 기반 빠른 인쇄 가능성 예측]
  - CNN/SVM으로 각 패턴의 인쇄 난이도 분류
  - "쉬운 패턴": 규칙 기반 OPC → 빠른 처리
  - "어려운 패턴": 심층 학습 또는 수치 ILT → 고품질
        ↓
[이질적 처리]
  쉬운 패턴 경로:
    레이아웃 → 규칙 기반 OPC → 마스크

  어려운 패턴 경로:
    레이아웃 → GAN 마스크 예측 → (선택적) ILT 정제 → 마스크
        ↓
[결과 통합]
  전체 칩 마스크 재조합
```

### ML 적용 OPC 단계별 정리
| OPC 단계 | 전통 방법 | ML 대체/보완 방법 |
|---------|---------|----------------|
| 리소그래피 시뮬레이션 | SOCS/Hopkins 수치계산 | CNN 기반 빠른 예측 (DLS) |
| 마스크 최적화 | 반복 경사하강 | GAN/신경망 직접 생성 |
| 핫스팟 검출 | 규칙 기반 검색 | CNN/SVM 분류기 |
| 레지스트 윤곽 예측 | 물리 시뮬레이션 | DNN 회귀 |
| SRAF 배치 | 모델 기반 안내 맵 | U-Net 생성 |

### 발전 방향 (2019년 당시 예측)
논문에서 제시한 미래 연구 방향 (이후 실현됨):
1. 더 강력한 생성 모델 (→ DAMO, DevelSet, DiffOPC 등으로 실현)
2. 물리 지식 통합 (→ Physics-informed 신경망으로 실현)
3. 풀칩 스케일 처리 (→ CFNO, AdaOPC 등으로 실현)
4. 공정 윈도우 인식 최적화 (→ PW-aware OPC로 실현)

## OPC 툴 구현 관련성
이 서베이는 SKOPC 전체 아키텍처 설계의 이론적 배경:
- **아키텍처 정당성**: SKOPC의 규칙 기반 + 모델 기반 이중 구조가 이질적 OPC 프레임워크와 일치
- **GNN-OPC 위치**: 서베이의 생성 모델 범주에서 GNN 기반으로 확장된 최신 접근
- **평가 기준선**: 2019년 당시 SOTA 방법들이 SKOPC 성능 평가의 역사적 기준점
- **ML 파이프라인**: 서베이의 이질적 처리 흐름이 SKOPC recipe_runner의 레이어별 처리에 반영

## 참고문헌 (핵심)
- Yang et al., "GAN-OPC" (DAC 2018) - 이 서베이에서 핵심 참조
- Ma et al., "Rethinking the Open-Source Mask Optimisation" (ISPD 2020)
- LeCun et al., "Deep Learning" (Nature 2015)
- Goodfellow et al., "Generative Adversarial Nets" (NeurIPS 2014)

## 태그
`Survey`, `Mask Optimization`, `Shallow Learning`, `Deep Learning`, `GAN`, `CNN`, `OPC`, `Heterogeneous Framework`, `ASP-DAC 2020`, `2020`, `CUHK`, `Printability`, `Hotspot Detection`
