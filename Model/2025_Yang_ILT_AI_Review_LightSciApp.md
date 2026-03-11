# Advancements and Challenges in Inverse Lithography Technology: A Review of Artificial Intelligence-Based Approaches

## 메타데이터
- **저자**: Yang et al. (Tsinghua University 연구팀)
- **연도**: 2025
- **게재지/학회**: Light: Science & Applications, Vol. 14, Article 250 (Nature Publishing Group)
- **DOI/URL**: https://doi.org/10.1038/s41377-025-01923-w; PubMed: 40701983
- **인용수**: 신규 (2025년 7월 발표)

## 핵심 요약
역리소그래피 기술(ILT)과 AI 기반 접근법의 최신 동향을 체계적으로 정리한 포괄적 리뷰 논문. ILT의 기본 원리부터 CNN, GAN, VAE, GCN 등 다양한 딥러닝 모델의 응용까지 광범위하게 다룬다. AI가 ILT의 계산 비용, 마스크 복잡도, 두꺼운 마스크 근거리장 시뮬레이션, 레지스트 효과 모델링, 에칭 공정 최적화에 어떻게 적용되는지 정리하며, 물리 내재형(physics-embedded) 딥러닝, 곡선형 마스크, 자동화 워크플로우 등 미래 방향을 제시한다.

## 주요 기여
- ILT + AI 분야 2025년 기준 최신 포괄적 리뷰
- CNN, GAN, VAE, GCN 등 다양한 AI 아키텍처의 ILT 적용 체계적 분류
- 두꺼운 마스크 근거리장 시뮬레이션의 딥러닝 가속 방법 정리
- 레지스트 효과 모델링 AI 방법 체계적 분류
- 에칭 공정 + AI 최적화 방법 포함
- 물리 내재형 딥러닝의 미래 방향 제시

## 모델 아키텍처/수식
**리뷰된 AI 방법 분류 체계:**

**1. 리소그래피 시뮬레이션 AI:**
- CNN 기반 마스크→웨이퍼 매핑:
  ```
  I_wafer = CNN_θ(mask)   (surrogate 시뮬레이터)
  ```
- GAN 기반 (LithoGAN):
  ```
  G: mask → wafer,  D: real vs. generated
  ```
- Fourier Neural Operator (FNO):
  ```
  y = IFFT(R_θ · FFT(x))  (주파수 공간 학습)
  ```

**2. 마스크 최적화 AI:**
- CNN/UNet 기반 ILT:
  ```
  mask = UNet_θ(layout)
  ```
- GAN-OPC 계열:
  ```
  mask = G_θ(layout),  학습: L_adv + L_litho
  ```
- Neural-ILT 계열 (레벨셋 보정 포함):
  ```
  mask = UNet_θ(layout) + ILT_correction(mask, litho_model)
  ```
- Diffusion 모델 (MODiff):
  ```
  mask = Denoise_θ(noise, layout_condition)
  ```

**3. 두꺼운 마스크 근거리장 시뮬레이션:**
- RCWA (Rigorous Coupled-Wave Analysis) AI 가속
- FCN으로 마스크 근거리 EMF 계산 가속
  ```
  E_near = FCN_θ(mask_3D)   (Maxwell 방정식 근사)
  ```

**4. 레지스트 모델링 AI:**
- 화학 확산 PDE Neural ODE 근사 (DeePEB):
  ```
  dA/dt ≈ f_θ(A, B, t)
  ```
- 확률론적 효과 ML 모델
- Hybrid 물리+데이터 모델

**5. 에칭 모델링 AI:**
- SVM, 신경망으로 에칭 프로파일 예측
- 공정 파라미터 → 최종 패턴 형상 매핑

**AI vs. 전통 방법 성능 비교 (리뷰 기준):**
| 방법 | 속도 | 정확도 | 일반화 |
|------|------|--------|--------|
| 전통 ILT | 느림 | 최선 | 좋음 |
| CNN/UNet | 빠름 | 보통 | 제한적 |
| GAN-OPC | 빠름 | 양호 | 중간 |
| Physics-DL | 빠름 | 양호 | 좋음 |
| Diffusion | 빠름 | 양호 | 중간 |

**미래 방향:**
1. 물리 내재형 딥러닝 (interpretability + consistency)
2. 다중 빔 마스크 묘화(MBMW)로 곡선형 마스크 제조
3. 자동화 마스크 생성 워크플로우
4. 다중 스케일 물리 모델링 프레임워크

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 전체 AI/ML OPC 모듈 개발 방향 설정에 핵심 참조. 이 리뷰에서 정리한 물리 내재형 딥러닝 접근법이 SKOPC GNN-OPC의 다음 세대 아키텍처 방향. 특히 곡선형 마스크(curvilinear mask) 대응을 위한 SKOPC 확장 로드맵 수립에 활용. 에칭 모델 AI 접근법은 SKOPC의 PPC(Post-Pattern Correction) 기능 추가 시 참조.

## 참고문헌 (핵심)
- Yang, H. et al., "GAN-OPC," DAC 2018
- Liu, X. et al., "Neural-ILT 2.0," TCAD 2022
- Yang, H. et al., "Dual-band optics-inspired NN," DAC 2022
- Zou, N. et al., "MODiff," SPIE 2025
- Wang, Q. et al., "DeePEB," ICCAD 2022

## 태그
`Model`, `OPC`, `ILT`, `Review`, `AI`, `DeepLearning`, `CNN`, `GAN`, `Diffusion`, `PhysicsInformed`, `ResistModel`, `EtchModel`, `CurvilinearMask`, `Nature`, `LightSciApp`
