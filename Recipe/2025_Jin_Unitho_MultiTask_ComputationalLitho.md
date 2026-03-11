# Unitho: A Unified Multi-Task Framework for Computational Lithography

## 메타데이터
- **저자**: Qian Jin, Yumeng Liu, Yuqi Jiang, Qi Sun, Cheng Zhuo
- **연도**: 2025
- **게재지/학회**: arXiv preprint (Invited Paper), arXiv:2511.10255
- **DOI/URL**: https://arxiv.org/html/2511.10255
- **인용수**: N/A (2025 신규)

## 핵심 요약
Unitho는 계산 리소그래피(Computational Lithography)의 마스크 생성, 규칙 위반 검출, 레이아웃 최적화를 하나의 통합 멀티태스크 대형 비전 모델(Large Vision Model)로 처리하는 프레임워크다. Swin Transformer 기반의 계층적 특성 추출과 크로스 어텐션 퓨전을 활용하며, 55nm 기술 노드에서 624,129개의 레이아웃-마스크-윤곽 삼중쌍(triplet) 산업용 데이터셋으로 검증되었다. 상용 툴 대비 85배 빠른 속도와 98.01% F1-score의 DRC 검출 성능을 달성한다.

## 주요 기여
- **통합 멀티태스크 프레임워크**: 마스크 생성, 리소그래피 시뮬레이션, 위반 검출을 단일 파이프라인으로 통합
- **공정 조건 퓨전**: 크로스 어텐션 메커니즘으로 레이아웃 구조와 공정 파라미터 간의 의미론적 연결
- **대조 학습 전략**: SAC(Structure-Aware Contrast)와 PAC(Process-Aware Contrast)로 구조적 구별성 및 엣지 정밀도 향상
- **산업 규모 검증**: 624,129개 레이아웃 클립으로 Lithography-Friendly-Design 워크플로우 실용성 입증

## Recipe/Process Flow 상세

### 통합 OPC/리소그래피 파이프라인

```
레이아웃 입력
     ↓
[레이아웃 인코더: Swin Transformer]
     ↓                     ↓
[공정 조건 인코더: BGE 임베딩]
     ↓
[크로스 어텐션 퓨전 모듈]
     ↓
[이미지 디코더: Transposed Conv + Residual Blocks]
     ↓                     ↓
   마스크 생성          레지스트 윤곽 생성
     ↓
[멀티스케일 검출기: ResNet-18 + Transformer]
     ↓
DRC/LRC 위반 검출 결과
```

### 3단계 학습 전략
#### 1단계: 생성 사전 학습 (Generation Pre-training)
- BCE, Dice, Edge-aware 손실 함수 결합
- 대조 학습 목적 함수 포함 (SAC + PAC)
- 마스크 생성 가중치 = 윤곽 생성의 2배 (정확도 우선)

#### 2단계: 검출 사전 학습 (Detection Pre-training)
- Varifocal Loss (클래스 불균형 처리)
- False Positive Penalty Loss (불필요한 제조 조정 감소)
- L1 및 Generalized IoU 회귀 손실

#### 3단계: 공동 파인튜닝 (Joint Fine-tuning)
- 생성 모듈 가중치 고정(Frozen)
- 검출기가 생성된 윤곽 특성에 적응
- 엔드-투-엔드 LRC 핫스팟 예측

### 공정 조건 파라미터
공정 인코더가 처리하는 스칼라 공정 파라미터 예시:
- 노광 선량(Exposure Dose)
- 초점 오프셋(Focus Offset)
- NA(Numerical Aperture)
- 조명 형상(Illumination Shape)
- 레지스트 파라미터

### 성능 지표 (55nm 노드)
| 태스크 | 지표 | Unitho | 상용 툴 |
|--------|------|--------|---------|
| 마스크 생성 | 픽셀 정확도 | 98.96% | - |
| 마스크 생성 | Edge F1 | 99.08% | - |
| DRC 검출 | F1-score | 98.01% | - |
| LRC 검증 | 오차 | < 4% | 기준 |
| 처리 속도 | 클립당 시간 | 104.96ms | 8,913.1ms |

## OPC 툴 구현 관련성
Unitho의 통합 접근 방식은 SKOPC 아키텍처 개선에 활용 가능:
- **통합 검증 파이프라인**: SKOPC의 분리된 OPC/DRC/검증 단계를 단일 포워드 패스로 통합하는 설계 영감
- **공정 조건 인식**: `process_model.py`의 공정 파라미터를 크로스 어텐션으로 OPC에 반영하는 구현 참조
- **55nm 레시피**: 55nm 노드 산업용 데이터 기반 검증으로 레시피 파라미터 범위 파악
- **LRC 핫스팟 검출**: 모델 OPC 후 자동 핫스팟 검출 모듈 구현에 활용

## 참고문헌 (핵심)
- Yang et al., "GAN-OPC" (IEEE TCAD 2020)
- Jiang et al., "Neural-ILT" (ICCAD 2020)
- Chen et al., "DAMO: Deep Agile Mask Optimization" (IEEE TCAD 2022)
- Liu et al., "LithoNet: Fast Lithography Simulation Using Convolutional Neural Network" (2019)
- Liu et al., "A Unified Design-Process Co-Optimization Framework for Lithography-Friendly Manufacturing" (2023)

## 태그
`Unitho`, `Multi-task Learning`, `Computational Lithography`, `Mask Generation`, `DRC`, `LRC`, `Transformer`, `Swin Transformer`, `Contrastive Learning`, `Process Condition`, `55nm`, `2025`, `Invited Paper`
