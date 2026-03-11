# ILILT: Implicit Learning of Inverse Lithography Technologies

## 메타데이터
- **저자**: Haoyu Yang, Haoxing Ren (NVIDIA Corp.)
- **연도**: 2024
- **게재지/학회**: ICML 2024 (International Conference on Machine Learning) / arXiv:2405.03574
- **DOI/URL**: https://arxiv.org/abs/2405.03574
- **인용수**: N/A (2024년 출판)

## 핵심 요약
ILILT는 마스크 최적화를 암묵적 레이어 학습 문제로 재공식화하여, ILT 솔버를 루프에 개입시키지 않고 고품질 최적화 마스크를 직접 생성하는 프레임워크다. 리소그래피 조건부 입력을 통해 물리적 리소그래피 시뮬레이션에 그라운딩하여 훈련-추론 분포 이동 문제를 해결한다. Pix2PixHD 백본으로 GPU-ILT 수치 솔버 대비 EPE를 62% 감소시키면서 10배 속도 향상을 달성한다.

## 주요 기여
- **암묵적 레이어 학습 공식화**: 마스크 최적화를 불동점(fixed-point) 수렴 문제로 재공식화
- **리소그래피 조건부 입력**: 중간 리소그래피 추정치를 마스크 업데이트 규칙에 포함하여 물리적 그라운딩
- **분포 이동 해결**: 훈련-추론 분포 이동을 인식하고 보정하는 첫 ML 기반 ILT
- **10배 속도 향상**: GPU-ILT 대비 10배 빠른 추론 속도, EPE 62% 감소

## Recipe/Process Flow 상세

### 핵심 혁신: 리소그래피 조건부 마스크 업데이트

기존 ILT 마스크 업데이트 규칙:
M_{t+1} = g(M_t, Z*, w)

ILILT 리소그래피 조건부 업데이트 규칙:
**M_{t+1} = g(M_t, Z_t, Z*, w)**

여기서:
- M_t: 현재 타임스텝 마스크
- Z_t: 현재 마스크에서 리소그래피 시뮬레이터로 계산한 웨이퍼 이미지
- Z*: 목표 웨이퍼 패턴
- w: 학습 가능한 네트워크 파라미터

### 훈련 아키텍처

**고정 깊이 T 언롤링 + 지수 가중 손실**
손실 함수:
L = Σ_{t=[T/2]}^T exp[t/T - 1] · ||M_t - M*||_F²

- 후반 타임스텝에 더 큰 가중치 (정밀 수렴 장려)
- 안정적인 불동점 수렴 학습

### 네트워크 백본 (2가지)

**CFNO (Convolutional Fourier Neural Operator)**
- 파라미터: 130K (초경량)
- 패치 기반 주파수 도메인 학습
- 빠른 추론, 낮은 메모리

**Pix2PixHD**
- 파라미터: 45M
- 고해상도 이미지 합성을 위한 계층적 지역 향상
- 최고 품질 (EPE 0.08 violations)

### ILILT 최적화 파이프라인

**단계 1: 초기화**
- 목표 패턴 Z*로 초기 마스크 M_0 설정
- 리소그래피 시뮬레이터로 Z_0 계산

**단계 2: 반복 마스크 개선 (t = 0 to T)**
1. 현재 마스크 M_t로 리소그래피 시뮬레이션 실행 → Z_t 획득
2. 네트워크 g(M_t, Z_t, Z*, w)로 업데이트된 마스크 예측
3. M_{t+1} 생성

**단계 3: 수렴 확인**
- 불동점 조건: M_{t+1} ≈ M_t
- EPE 및 PVB 지표 계산

### 성능 결과 (GPU-ILT 기준선 대비)

| 방법 | EPE 위반 | 속도 향상 |
|------|----------|-----------|
| GPU-ILT (기준) | 0.21 | 1× |
| CFNO 단독 | ~0.16 | 20× |
| Pix2PixHD 단독 | ~0.14 | 15× |
| **ILILT-Pix2PixHD** | **0.08** | **10×** |
| ILILT-CFNO | comparable | 400× 작은 모델 |

### ILILT의 고유 기능
- 부분 최적화된 마스크에서 최적화 계속 가능
- 훈련 데이터 분포 밖의 마스크 사전 학습
- 수치 솔버의 품질 변동 없는 안정적 최적화 궤적

## OPC 툴 구현 관련성
- **리소그래피 조건부 OPC**: OPC 레시피 최적화 루프에서 중간 시뮬레이션 결과를 피드백으로 활용하는 설계
- **불동점 수렴 OPC**: 수렴 조건을 명시적으로 학습하는 OPC 최적화 루프 구현
- **경량 vs 고품질 모드**: CFNO(빠름)와 Pix2PixHD(고품질)를 OPC 레시피 모드로 선택 가능
- **분포 이동 처리**: 새로운 레이아웃 패턴에 OPC 모델을 적용할 때 분포 이동 문제 해결 방법론
- **NVIDIA cuLitho 통합**: NVIDIA 연구팀의 작업으로 cuLitho 플랫폼과의 통합 가능성

## 참고문헌 (핵심)
- Yang & Ren (2024): CurvyILT (arXiv:2411.07311)
- Yang et al. (2022): CFNO (arXiv:2207.04056)
- Chen et al. (2020): DAMO (arXiv:2008.00806)
- GAN-OPC (Yang et al., 2018)

## 태그
`ILILT`, `Implicit Learning`, `Fixed-point`, `ILT`, `Pix2PixHD`, `CFNO`, `ICML2024`, `NVIDIA`, `Distribution Shift`, `Recipe`, `OPC`, `Mask Optimization`, `10x Speedup`
