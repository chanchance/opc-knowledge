# MaskOpt: A Large-Scale Mask Optimization Dataset to Advance AI in Integrated Circuit Manufacturing

## 메타데이터
- **저자**: Yuting Hu, Lei Zhuang, Hua Xiang, Jinjun Xiong, Gi-Joon Nam
- **연도**: 2025
- **게재지/학회**: arXiv preprint, arXiv:2512.20655
- **DOI/URL**: https://arxiv.org/html/2512.20655
- **인용수**: N/A (2025 신규)

## 핵심 요약
MaskOpt는 실제 IC 디자인에서 추출한 대규모 마스크 최적화 벤치마크 데이터셋으로, 45nm 노드에서 금속 레이어 104,714개 및 비아 레이어 121,952개 샘플을 포함한다. 합성 레이아웃이 아닌 OpenROAD 플로우를 통해 실제 IC 디자인에서 추출하여 셀 구조와 주변 컨텍스트를 보존하며, 딥러닝 기반 OPC/ILT 연구의 실용성을 높인다. 셀 정보와 컨텍스트 기하 구조가 마스크 생성 정확도를 유의미하게 개선함을 실험적으로 검증한다.

## 주요 기여
- **실제 IC 기반 데이터셋**: 합성 레이아웃이 아닌 5개 실제 IC 디자인에서 추출 (다양한 로직 게이트 포함)
- **계층적 셀 구조 보존**: 표준 셀 배치 경계를 기준으로 클리핑하여 셀 구조 맥락 유지
- **멀티 컨텍스트 윈도우**: 0, 16, 32, 64, 128nm 5가지 컨텍스트 마진 제공
- **종합 벤치마크**: GAN-OPC, Neural-ILT, DAMO, CFNO 4개 SOTA 모델 비교 검증

## Recipe/Process Flow 상세

### 데이터셋 구성
| 구분 | 수량 | 해상도 | 노드 |
|------|------|--------|------|
| 금속 레이어 | 104,714 tiles | 1024×1024 px | 45nm |
| 비아 레이어 | 121,952 tiles | 1024×1024 px | 45nm |
| 핵심 영역 크기 | - | 512nm × 512nm | - |

### 마스크 최적화 파이프라인 (OPC 플로우)
Model-based OPC의 표준 반복 플로우:
1. **패턴 분할(Segmentation)**: 레이아웃 패턴을 이동 가능한 라인 세그먼트로 분할
2. **리소그래피 시뮬레이션**: 현재 마스크 패턴의 공중 이미지 및 레지스트 윤곽 계산
3. **윤곽 비교(Contour Comparison)**: 시뮬레이션된 윤곽과 설계 타겟 비교
4. **국소 보정(Local Correction)**: 각 세그먼트에 대한 이동 보정 적용
5. **수렴 판단**: 보정된 마스크 패턴의 EPE가 허용 범위 이내인지 확인
6. **반복(Iteration)**: 수렴 기준 충족까지 반복

### 딥러닝 모델 워크플로우
```
입력: 레이아웃 타겟 이미지 + 셀 태그 (컨텍스트 윈도우 포함)
↓
DL 모델 (GAN-OPC / Neural-ILT / DAMO / CFNO)
↓
최적화된 마스크 이미지 출력
↓
손실 함수 평가:
  - L₂(프린트 패턴 vs 타겟)
  - PVB (공정 변동 밴드)
  - EPE (엣지 배치 오차)
```

### 손실 함수 상세
$$\mathcal{L} = \lambda_1 \|M_{printed} - T\|_2^2 + \lambda_2 \cdot PVB + \lambda_3 \cdot EPE$$

### 포함 디자인 로직 게이트
- AND, NAND, NOR, OR, XOR 계열
- 다양한 입력 구성 및 드라이브 강도 변형
- 실제 배치 기반 다양한 주변 컨텍스트

### 데이터 소스
- **IC 디자인**: OpenROAD 플로우 기반 5개 실제 IC
- **기술 라이브러리**: 45nm 공정 기술 라이브러리
- **추출 방식**: 표준 셀 배치 경계 기준 타일 클리핑

## OPC 툴 구현 관련성
MaskOpt 데이터셋은 SKOPC 개발에 다음 방식으로 활용 가능:
- **GNN-OPC 학습 데이터**: 실제 IC 레이아웃 기반의 다양한 패턴을 GNN 모델 학습에 활용 (`skopc/modeling/gnn/`)
- **벤치마크 기준선**: SKOPC의 모델 OPC 출력을 MaskOpt 데이터와 비교하여 성능 검증
- **45nm 레시피 검증**: 45nm 노드에서의 OPC 레시피 파라미터 튜닝 기준 데이터로 활용
- **컨텍스트 인식 OPC**: 주변 셀 컨텍스트를 OPC 보정에 반영하는 구현 가이드

## 참고문헌 (핵심)
- Yang et al., "GAN-OPC: Mask Optimization with Lithography-guided Generative Adversarial Nets" (IEEE TCAD 2020)
- Jiang et al., "Neural-ILT" (ICCAD 2020)
- Chen et al., "DAMO: Deep Agile Mask Optimization" (IEEE TCAD 2022)
- Zhong et al., "CFNO: Clifford Fourier Neural Operator for Lithography Simulation" (2023)
- OpenROAD Project, "OpenROAD: Toward a Self-Driving, Open-Source Digital Layout Implementation Tool Chain" (TODAES 2021)

## 태그
`MaskOpt`, `Dataset`, `Mask Optimization`, `OPC`, `ILT`, `Deep Learning`, `45nm`, `Benchmark`, `GAN-OPC`, `Neural-ILT`, `OpenROAD`, `2025`
