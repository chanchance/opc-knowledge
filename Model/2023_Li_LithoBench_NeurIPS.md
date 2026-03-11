# LithoBench: Benchmarking AI Computational Lithography for Semiconductor Manufacturing

## 메타데이터
- **저자**: Hao Geng, Guojin Chen, Yuzhe Ma, Bei Yu, Martin D.F. Wong (CUHK, HKBU)
- **연도**: 2023
- **게재지/학회**: 37th Conference on Neural Information Processing Systems (NeurIPS 2023), Datasets and Benchmarks Track
- **DOI/URL**: https://proceedings.neurips.cc/paper_files/paper/2023/hash/604b9fa9e1c16284e6517d923cf9ff20-Abstract-Datasets_and_Benchmarks.html; GitHub: https://github.com/shelljane/lithobench
- **인용수**: 60+

## 핵심 요약
딥러닝 기반 리소그래피 시뮬레이션과 마스크 최적화를 위한 최초의 대규모 실제 설계(real-world design) 기반 데이터셋 LithoBench를 발표한 논문. 실제 회로 설계에서 추출하거나 ILT 테스트케이스 레이아웃 토폴로지로 합성한 12만 개 이상의 타일로 구성된다. 학계 유명 리소그래피 모델과 고급 ILT 방법으로 생성된 ground truth를 포함하며, 다양한 딥러닝 모델을 설계하고 평가하기 위한 표준 프레임워크를 함께 제공한다.

## 주요 기여
- 실제 회로 설계 기반 최초의 대규모 AI 리소그래피 벤치마크 데이터셋 구축
- 12만 개+ 레이아웃 타일 (리소그래피 시뮬레이션 + 마스크 최적화 포함)
- 학계 검증된 리소그래피 모델로 생성된 고품질 ground truth
- 표준 DNN 설계/평가 프레임워크 제공
- 리소그래피 시뮬레이션 및 ILT 두 작업에 대한 공정한 비교 기반 확립

## 모델 아키텍처/수식
**데이터셋 구성:**
```
LithoBench
├── Lithography Simulation Track
│   ├── Input: mask tile (binary, 512×512)
│   └── Output: wafer image (grayscale, 512×512)
└── Mask Optimization Track
    ├── Input: target layout tile (binary, 512×512)
    └── Output: optimized mask (binary, 512×512)
```

**Ground Truth 생성 파이프라인:**
```
Layout → [Hopkins Optical Model (TCC, 15 kernels)] → Aerial Image
       → [Variable Threshold Resist Model] → Wafer Image

Layout → [Gradient-based ILT optimizer] → Optimized Mask
       → [Lithography Simulator] → Verify EPE < threshold
```

**평가 지표:**
- 리소그래피 시뮬레이션: Pixel Difference (PD), L2 Distance
- 마스크 최적화: Edge Placement Error (EPE), Process Variation Band (PVBand)
```
EPE = mean(|edge_simulated - edge_target|)
PVBand = Area(Wafer_defocus ⊕ Wafer_nominal) - Area(Wafer_defocus ⊖ Wafer_nominal)
```

**벤치마크 모델 종류:**
- CNN 기반: U-Net, FCN, ResNet
- GAN 기반: Pix2Pix, LithoGAN
- Fourier Neural Operator (FNO)
- Physics-informed 모델

**데이터셋 규모:**
- 총 120,000+ 타일
- 타일 크기: 2048nm × 2048nm (공정 노드 별)
- 훈련/검증/테스트 분할: 8:1:1

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC GNN-OPC 모델 학습 및 평가를 위한 표준 데이터셋으로 활용 가능. `tests/` 디렉토리의 테스트 케이스를 LithoBench 형식으로 확장하면 산업 표준 비교가 가능. TorchResist 논문에서도 LithoBench를 평가 기준으로 사용. EPE, PVBand 지표는 SKOPC 모델 평가 메트릭 구현에 직접 참조 가능. GitHub에서 데이터셋 다운로드 후 `skopc/modeling/gnn/` 학습에 활용 권장.

## 참고문헌 (핵심)
- Yang, H. et al., "GAN-OPC," DAC 2018
- Ye, C. et al., "LithoGAN," DAC 2019
- Chen, G. et al., "DAMO," ICCAD 2020
- Liu, X. et al., "Neural-ILT 2.0," TCAD 2022
- Li, Y. et al., "Large scale mask optimization via convolutional Fourier neural operator," arXiv:2207.04056 (2022)

## 태그
`Model`, `OPC`, `Dataset`, `Benchmark`, `LithoBench`, `NeurIPS`, `LithographySimulation`, `MaskOptimization`, `ILT`, `EPE`, `PVBand`, `OpenSource`, `DeepLearning`
