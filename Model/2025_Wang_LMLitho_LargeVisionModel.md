# LMLitho: A Large Vision Model-Driven Lithography Simulation Framework

## 메타데이터
- **저자**: Z. Wang, H. He, T. Wu, X. He, Q. Sun, C. Zhuo, Bei Yu, J. Yu, H. Geng (CUHK)
- **연도**: 2025
- **게재지/학회**: IEEE/ACM International Conference on Computer Aided Design (ICCAD 2025)
- **DOI/URL**: https://ieeexplore.ieee.org/document/11240940; PDF: https://www.cse.cuhk.edu.hk/~byu/papers/C286-ICCAD2025-LMLitho.pdf
- **인용수**: 신규 (2025년 10월)

## 핵심 요약
대형 비전 모델(Large Vision Model, LVM)을 활용한 리소그래피 시뮬레이션 프레임워크 LMLitho를 제안한 논문. 약 10만 개의 조명 맵, 마스크, 레지스트 이미지 삼중(triplet) 데이터로 학습된다. 마스크 인코더, 광원 인코더, 마스크 구동 노광 어텐션 모듈, 레지스트 디코더의 4개 핵심 컴포넌트로 구성된다. 원형, 환형, 불아이, 다이폴, 쿼사, 다중극 등 6가지 대표적 광원 타입을 포함한 포괄적 데이터셋으로 학습하여 다양한 리소그래피 조건에서 일반화된 시뮬레이션을 제공한다.

## 주요 기여
- 대형 비전 모델(LVM)을 리소그래피 시뮬레이션에 최초 적용
- 4개 컴포넌트 아키텍처: Mask Encoder + Source Encoder + Exposure Attention + Resist Decoder
- 10만 개 (조명, 마스크, 레지스트 이미지) 삼중 데이터로 학습
- 6가지 조명 타입 지원으로 폭넓은 리소그래피 조건 커버
- 실제 CPU 설계 레이아웃 패턴 포함

## 모델 아키텍처/수식
**LMLitho 4개 핵심 컴포넌트:**

**1. Mask Encoder:**
```
Input: binary mask (H×W)
Architecture: ViT (Vision Transformer) 기반
Output: mask feature vector f_mask ∈ ℝ^D
```
이진 마스크 → 리소그래피 시뮬레이션에 적합한 compact 특징 벡터

**2. Source Encoder:**
```
Input: illumination source map (N×N, 2D 광원 분포)
Architecture: CNN + MLP
Output: source feature vector f_source ∈ ℝ^d
```
6가지 광원 타입:
- 원형(Circular): 단순 동공, σ = 0.3~0.9
- 환형(Annular): σ_inner/σ_outer
- 불아이(Bull's eye): 특수 다중 고리
- 다이폴(Di-pole): 두 점 광원
- 쿼사(Quasar): 4개 쐐기 모양
- 다중극(Multi-pole): 다중 극점

**3. Mask-Driven Exposure Attention Module (핵심 혁신):**
```
Attention(Q, K, V):
  Q = W_Q · f_mask   (마스크에서 Query)
  K = W_K · f_source  (광원에서 Key)
  V = W_V · f_source  (광원에서 Value)
  A = softmax(Q·K^T / √d_k) · V
```
물리적 의미: 마스크의 각 위치가 광원 분포를 어떻게 변조하는지 어텐션으로 학습

**4. Resist Decoder:**
```
Input: combined features (mask + exposure attention output)
Architecture: Deconvolutional decoder (U-Net style)
Output: resist image (wafer image, 0~1)
```

**전체 포워드:**
```
f_mask = MaskEncoder(mask)
f_source = SourceEncoder(illumination)
f_exposure = ExposureAttention(f_mask, f_source)
wafer_image = ResistDecoder(f_mask, f_exposure)
```

**학습 데이터:**
```
Dataset: ~100,000 triplets
  (illumination_map, mask, resist_image)
광원 타입: 6종 (circular, annular, bull's eye, dipole, quasar, multi-pole)
레이아웃: canonical test structures + actual CPU designs
Ground Truth: 상업용 리소그래피 시뮬레이터
```

**손실 함수:**
```
L = λ₁·||wafer_pred - wafer_GT||²
  + λ₂·||contour_pred - contour_GT||²
  + λ₃·EPE(wafer_pred, target)
```

**성능:**
- 속도: 상업용 시뮬레이터 대비 100×+ 빠름
- 광원 일반화: 학습에 없는 광원 조합에서도 정확
- CPU 레이아웃: 복잡한 실제 패턴에서 검증

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 `LithoEngine` 차세대 대안으로 고려 가능. LMLitho의 조명 어텐션 메커니즘은 SKOPC에서 광원 타입 변경 시 재학습 없이 모델 적응하는 유연한 시뮬레이터로 활용 가능. 특히 `skopc/smo/` SMO 모듈에서 다양한 광원 조합을 빠르게 평가할 때 LMLitho 방식의 광원 인코딩이 유용. 오픈소스 공개 여부 확인 후 SKOPC 통합 검토 권장.

## 참고문헌 (핵심)
- Chen, G. et al., "Open-source differentiable lithography framework," arXiv:2409.15306 (2024)
- He, H. et al., "LithoSim," NeurIPS 2025
- Yang, H. et al., "Dual-band optics-inspired NN," DAC 2022
- Dosovitskiy, A. et al., "An image is worth 16×16 words (ViT)," ICLR 2021
- Wang, Z. et al., "UniTho: Unified multi-task lithography," arXiv:2511.10255 (2025)

## 태그
`Model`, `OPC`, `LargeVisionModel`, `LVM`, `LithographySimulation`, `Transformer`, `ViT`, `AttentionMechanism`, `SourceEncoder`, `MaskEncoder`, `ICCAD`, `CUHK`, `IlluminationGeneralization`
