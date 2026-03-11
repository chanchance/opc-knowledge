# DAMO: Deep Agile Mask Optimization for Full Chip Scale

## 메타데이터
- **저자**: Guojin Chen, Wanli Chen, Yuzhe Ma, Haoyu Yang, Bei Yu
- **연도**: 2020 (ICCAD), 2021 (TCAD 저널판)
- **게재지/학회**: IEEE/ACM International Conference on Computer-Aided Design (ICCAD 2020); IEEE Transactions on Computer-Aided Design (TCAD 2021)
- **DOI/URL**: https://doi.org/10.1145/3400302.3415705; https://arxiv.org/abs/2008.00806; https://ieeexplore.ieee.org/document/9552247
- **인용수**: 150+

## 핵심 요약
전체 칩 규모(full-chip scale)에서 동작하는 딥러닝 기반 OPC 시스템 DAMO를 제안한 논문. Deep Lithography Simulator (DLS)와 Deep Mask Generator (DMG)의 두 핵심 모듈로 구성된 end-to-end 마스크 최적화 패러다임을 도입한다. DLS는 리소그래피 시뮬레이션을 수행하는 고해상도 신경망이며, DMG는 DLS의 역보정(inverse correction)을 통해 학습하여 직접 고품질 마스크를 생성한다. full-chip 적용을 위한 맞춤형 레이아웃 분할 알고리즘도 함께 제안한다.

## 주요 기여
- DLS(Deep Lithography Simulator): 고해상도 리소그래피 시뮬레이션 신경망
- DMG(Deep Mask Generator): DLS 역보정 기반 마스크 생성 네트워크
- DCGAN-HD 기반 고해상도 이미지 생성 구조 적용
- Full-chip 스케일을 위한 커스텀 레이아웃 분할 알고리즘
- 산업계 및 학계 state-of-the-art 대비 우수한 성능 입증
- 딥러닝이 다양한 레이아웃/마스크 최적화 문제의 대안 솔루션임을 입증

## 모델 아키텍처/수식
**전체 DAMO 파이프라인:**
```
Layout → Layout Splitting → [DLS + DMG] per tile → Mask Assembly → Full-Chip Mask
```

**Module 1: Deep Lithography Simulator (DLS)**
- DCGAN-HD Generator 구조 기반
- 입력: 마스크 이미지 (타일, 512×512)
- 출력: 웨이퍼 시뮬레이션 이미지
- 손실: L1 + perceptual loss
```
L_DLS = ||DLS(mask) - wafer_GT||₁ + λ_p · ||φ(DLS(mask)) - φ(wafer_GT)||₂
```
φ: VGG 특징 추출기 (perceptual loss)

**Module 2: Deep Mask Generator (DMG)**
- DLS와 연동된 조건부 생성 네트워크
- 입력: 타겟 레이아웃
- 출력: 최적화된 마스크
- 학습: DLS를 고정하고 DMG만 역보정 방향으로 학습
```
L_DMG = ||DLS(DMG(layout)) - layout||₂ + λ_c · L_complexity(DMG(layout))
```

**레이아웃 분할 알고리즘:**
- 중첩(overlap) 영역 포함한 타일 분할 (512×512, stride 256)
- 타일 경계 부드러운 블렌딩(blending)을 위한 가중치 마스크 적용
- 분할 시 hotspot 영역 우선 처리

**성능 지표 (ICCAD 2013 벤치마크):**
- EPE RMS: 기존 방법 대비 ~20% 개선
- 처리 속도: gradient ILT 대비 100× 이상

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 GNN-OPC 모듈 개발 시 참조할 중요 논문. DAMO의 DLS 컴포넌트는 SKOPC `LithoEngine`의 신경망 surrogate로 활용 가능하며, DMG의 역보정 학습 방식은 GNN 기반 세그먼트 변위 예측 네트워크 학습에 응용 가능. Full-chip 타일 분할 알고리즘은 SKOPC의 full-chip OPC 처리 파이프라인에 참조.

## 참고문헌 (핵심)
- Yang, H. et al., "GAN-OPC: Mask optimization with lithography-guided GANs," DAC 2018
- Ye, C. et al., "LithoGAN: End-to-end lithography modeling with GANs," DAC 2019
- Wang, T. et al., "High-resolution image synthesis and semantic manipulation with conditional GANs (DCGAN-HD)," CVPR 2018
- Simonyan, K. and Zisserman, A., "Very deep convolutional networks for large-scale image recognition (VGG)," ICLR 2015

## 태그
`Model`, `OPC`, `ILT`, `DeepLearning`, `MaskOptimization`, `FullChip`, `DLS`, `DMG`, `DCGAN`, `ICCAD`, `TCAD`, `SurrogateModel`, `LayoutSplitting`
