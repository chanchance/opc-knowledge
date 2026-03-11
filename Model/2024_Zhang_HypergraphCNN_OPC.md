# Model-Driven Optical Proximity Correction via Hypergraph Convolutional Neural Networks and Its Experimental Demonstration

## 메타데이터
- **저자**: Shengen Zhang, Xu Ma, Chaojun Huang, Fuli Wang, Gonzalo R. Arce
- **연도**: 2024
- **게재지/학회**: Optics and Lasers in Technology (ScienceDirect), Vol. 183, 2025
- **DOI/URL**: https://doi.org/10.1016/j.optlastec.2024.111199; https://www.sciencedirect.com/article/pii/S0030399224016578
- **인용수**: 신규 (2024년 발표)

## 핵심 요약
하이퍼그래프 합성곱 신경망(HGCN: Hypergraph Convolutional Neural Network)을 이용한 모델 기반 OPC 방법(MHGCN)을 제안한 논문. 기존 픽셀 기반 OPC 알고리즘의 계산 비용 문제를 해결하기 위해, 레이아웃 패턴의 고차(high-order) 관계를 하이퍼엣지(hyperedge)로 모델링하는 MHGCN 인코더와 리소그래피 이미징 모델 기반 디코더를 결합한다. 디지털 마이크로미러 장치(DMD) 무마스크 리소그래피 테스트베드에서 실험적으로 검증하여 시뮬레이션과 실제 공정 모두에서 우수한 성능을 입증했다.

## 주요 기여
- OPC에 하이퍼그래프 신경망(HGCN) 최초 적용
- 레이아웃 피처의 고차 관계를 하이퍼엣지로 모델링하여 예측 정확도 향상
- 모델 기반 리소그래피 디코더와 HGCN 인코더의 결합 (모델-데이터 하이브리드)
- DMD 무마스크 리소그래피 실험 테스트베드 구축 및 실증
- 계산 효율성과 리소그래피 이미지 충실도 동시 개선

## 모델 아키텍처/수식
**MHGCN 전체 구조 (3단계):**
```
Stage 1: Feature Matrix Extraction (Dense Concentric Circle Sampling, DCCS)
Stage 2: Encoder - HGCN (Hypergraph Convolutional Network)
Stage 3: Decoder - Lithography Imaging Model (물리 기반)
```

**Stage 1: DCCS 특징 추출**
동심원 샘플링으로 마스크 엣지 세그먼트 주변 피처 추출:
```
F_i = [I(r₁,θ₁), I(r₁,θ₂), ..., I(rₙ,θₘ)]
```
r₁,...,rₙ: 동심원 반경들; θ₁,...,θₘ: 각도 샘플링 위치

**Stage 2: HGCN 인코더**
하이퍼그래프 G = (V, E) 구성:
- V: 마스크 세그먼트(노드)
- E: 하이퍼엣지 (여러 세그먼트 간 고차 관계)

하이퍼그래프 합성곱:
```
H^(l+1) = σ(D_v^(-1/2) · H · B · D_e^(-1) · H^T · D_v^(-1/2) · H^(l) · W^(l))
```
- H: 인시던스 행렬 (vertex-hyperedge)
- D_v, D_e: vertex/hyperedge degree 대각 행렬
- B: 하이퍼엣지 가중치 행렬
- W^(l): l번째 레이어 학습 파라미터

출력: 각 세그먼트의 OPC 변위 예측값 Δd_i

**Stage 3: 리소그래피 디코더**
물리 기반 이미징 모델로 마스크 이미지 재구성:
```
I_wafer = Σₙ λₙ |Φₙ ⊗ M_corrected|²
M_corrected = M_original + Δd (HGCN 예측 변위 적용)
```

**손실 함수:**
```
L = ||I_wafer - I_target||² + λ_reg · ||Δd||²
```

**DMD 실험 검증:**
- Digital Micromirror Device (DMD) 기반 무마스크 리소그래피
- 이미징 모델 보정: 학습 레이아웃 패턴으로 DMD 시스템 PSF 보정
- 실험/시뮬레이션 결과 일치 확인

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 `skopc/modeling/gnn/` GNN-OPC 모듈과 매우 밀접하게 관련됨. SKOPC의 GNN이 ResGNN 기반 세그먼트 변위 예측을 수행하는 것처럼, MHGCN도 세그먼트 변위(Δd)를 예측한다. 하이퍼그래프 구조는 일반 GNN보다 복잡한 패턴 간 상호작용 모델링에 우수하며, SKOPC GNN 아키텍처 고도화 시 참조 가능. DCCS 특징 추출 방법은 SKOPC의 레이아웃 특징 추출 개선에 직접 적용 가능.

## 참고문헌 (핵심)
- Zhang, S. et al., "Fast OPC via model-driven GCN (MGCN)," Optics Express (2023)
- Feng, Y. et al., "HyperGCN: Hypergraph neural networks," NeurIPS 2019
- Ma, X. et al., "Sparse concentric circle GCN for OPC," Optics Express (2022)
- Yang, H. et al., "GAN-OPC," DAC 2018
- Chen, G. et al., "DAMO," ICCAD 2020

## 태그
`Model`, `OPC`, `GNN`, `HypergraphNN`, `HGCN`, `MaskOptimization`, `ModelDriven`, `SegmentDisplacement`, `DCCS`, `DMD`, `ExperimentalValidation`, `Hybrid`
