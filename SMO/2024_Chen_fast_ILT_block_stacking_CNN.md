# Fast Inverse Lithography Based on a Model-Driven Block Stacking Convolutional Neural Network

## 메타데이터
- **저자**: Ruixiang Chen, Yang Zhao, Haoqin Li, Rui Chen
- **연도**: 2024
- **게재지/학회**: arXiv:2412.14599 (physics.optics / cs.LG)
- **DOI/URL**: https://arxiv.org/abs/2412.14599
- **인용수**: 신규 논문 (2024년 12월)

## 핵심 요약
모델 기반(model-driven) 블록 스태킹 딥러닝 프레임워크를 활용한 신속한 OPC/ILT 방법론 논문. 벡터 리소그래피 모델링(vector lithography modeling)을 학습 기반으로 삼아 대규모 레이블 데이터 없이도 제조 친화적 마스크 패턴을 생성한다. 파형 함수 붕괴(wave function collapse) 알고리즘으로 다양한 타겟 패턴을 무작위 생성하여 마스크 패러다임의 범위를 확장한다.

## 주요 기여
- 모델 기반 블록 스태킹 CNN 아키텍처로 OPC/ILT 가속화
- 벡터 리소그래피 모델링으로 대규모 레이블 데이터셋 불필요
- 파형 함수 붕괴(Wave Function Collapse) 알고리즘으로 다양한 패턴 무작위 생성
- 기존 픽셀 기반 방법의 제조 복잡도 문제 해결
- 마스크 복잡도를 효과적으로 제어하면서 근접 효과 보정

## 알고리즘/수식
- **벡터 리소그래피 모델링**:
  - 마스크를 픽셀 그리드 대신 벡터(폴리곤) 표현으로 처리
  - 연속적 물리 모델로 미분가능 순방향 패스 구성
  - 벡터 마스크 파라미터에 대한 그래디언트 계산

- **블록 스태킹 아키텍처**:
  ```
  입력 레이아웃 → Block₁ → Block₂ → ... → BlockN → 마스크 출력
  각 Block: Conv → BN → ReLU → Conv → Skip Connection
  ```
  - 잔차 연결(residual connections)로 깊은 네트워크 학습 안정화
  - 각 블록이 점진적으로 마스크 세부 사항 정제

- **파형 함수 붕괴(Wave Function Collapse)**:
  - 절차적 콘텐츠 생성 알고리즘
  - 훈련 레이아웃에서 패턴 규칙 학습
  - 무작위이지만 구조적으로 일관된 다양한 타겟 패턴 생성
  - 데이터 증강(augmentation)의 특수한 형태

- **모델 기반 학습**:
  ```
  L = L_EPE(f_litho(CNN(layout)), target) + λ·L_complexity(CNN(layout))
  ```
  - 리소그래피 시뮬레이터 f_litho를 손실 계산에 직접 활용
  - 레이블 없이 물리 기반 자기지도 학습

## OPC 툴 구현 관련성
SKOPC의 GNN-OPC 대안 또는 보완 모듈로 고려 가능. 레이블 데이터 없이 벡터 리소그래피 모델만으로 학습 가능한 점이 실용적. 블록 스태킹 CNN은 ResGNN 대비 구현이 단순하여 빠른 프로토타입 제작에 유리. 파형 함수 붕괴 기반 패턴 생성은 SKOPC 테스트용 레이아웃 자동 생성(`tests/fixtures/`) 확장에도 응용 가능.

## 참고문헌 (핵심)
- WFC (Wave Function Collapse): Gumin (2016) — 절차적 생성 원전
- 벡터 리소그래피 모델링 관련 SPIE 논문들
- 블록 스태킹 CNN: ResNet 관련

## 태그
`ILT`, `OPC`, `CNN`, `block-stacking`, `vector-lithography`, `wave-function-collapse`, `model-driven`, `no-labeled-data`, `2024`, `arxiv`, `manufacturing-friendly`
