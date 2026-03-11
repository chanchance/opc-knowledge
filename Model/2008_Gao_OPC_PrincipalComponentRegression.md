# Optical Proximity Correction with Principal Component Regression

## 메타데이터
- **저자**: Peiran Gao, Allan Gu, Avideh Zakhor (University of California, Berkeley)
- **연도**: 2008
- **게재지/학회**: SPIE Optical Microlithography XXI, Vol. 6924
- **DOI/URL**: https://doi.org/10.1117/12.773208; PDF: http://www-video.eecs.berkeley.edu/papers/gao/SPIE-2008.pdf
- **인용수**: 80+

## 핵심 요약
통계적 머신러닝 기법인 주성분 회귀(PCR: Principal Component Regression)를 OPC 프래그먼트 이동 예측에 적용한 선구적 논문. OPC에서 마스크 엣지 프래그먼트(fragment)의 최적 이동량을 결정하는 문제를 고차원 회귀 문제로 정식화하고, PCA로 차원을 축소한 후 선형 회귀로 프래그먼트 이동량을 예측한다. 기존 모델 기반 OPC가 다수의 반복(iteration)을 필요로 하는 것에 비해, PCR 기반 예측으로 반복 횟수를 줄여 처리 속도를 향상시킨다. 이는 이후 ML 기반 OPC 연구의 초기 선구자적 논문이다.

## 주요 기여
- OPC 프래그먼트 이동량 예측에 통계적 ML(PCR) 최초 적용
- 고차원 이미지 특징을 PCA로 저차원 표현으로 압축
- 선형 회귀로 OPC 이동량 직접 예측
- 기존 반복적 model-based OPC의 초기화 품질 향상
- 반복 횟수 감소를 통한 OPC 처리 속도 향상

## 모델 아키텍처/수식
**문제 정식화:**

각 마스크 프래그먼트 i에 대해:
- 특징 벡터: x_i ∈ ℝᵈ (주변 이미지 강도 샘플)
- 예측 대상: δᵢ ∈ ℝ (최적 프래그먼트 이동량)

**주성분 회귀 (PCR) 절차:**

Step 1: 특징 추출
```
x_i = [I(r₁,θ₁), I(r₁,θ₂), ..., I(rₙ,θₘ)]
```
프래그먼트 i 주변의 동심원 샘플링으로 이미지 강도 특징 추출 (d = n×m 차원)

Step 2: PCA 차원 축소
```
X = [x₁, x₂, ..., xₙ_train]ᵀ  (N_train × d 행렬)
[U, Σ, V] = SVD(X - X̄)
X_pca = (X - X̄) · V_k           (상위 k개 주성분)
```
k < d로 차원 축소 (보통 k = 20~50)

Step 3: 선형 회귀
```
δ = X_pca · β + ε
β = argmin_β ||δ_train - X_pca_train · β||²
  = (X_pca_train^T · X_pca_train)^{-1} · X_pca_train^T · δ_train
```

Step 4: 예측 및 OPC 적용
```
δ_pred,i = (x_i - X̄) · V_k · β
M_corrected = M_original + δ_pred   (프래그먼트 이동)
```

**학습 데이터:**
- 훈련 패턴: model-based OPC 결과 (이미지 특징 → 최적 이동량)
- 패턴 다양성: 다양한 CD, pitch, 2D 형상 포함

**성능:**
- 반복 횟수: 기존 OPC 대비 30~50% 감소
- EPE RMS: 기존 방법과 동등 수준
- 처리 속도: 반복 감소로 전체 속도 향상

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [ ] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 GNN-OPC 모듈의 역사적 선구자. PCR이 사용하는 동심원 특징 샘플링(concentric circle sampling)은 현재 GNN-OPC의 DCCS(Dense Concentric Circle Sampling) 특징 추출의 직접적 선구자다. 선형 회귀에서 GNN으로의 발전 과정을 이해하는 데 필수적인 참조 논문. SKOPC의 rule-based OPC에서 model-based OPC로, 그리고 GNN-OPC로 이어지는 기술 발전 계보를 확인할 수 있다.

## 참고문헌 (핵심)
- Gu, A. and Zakhor, A., "Optical proximity correction with linear regression," IEEE Trans. Semicond. Manuf. (2008)
- Cobb, N. and Zakhor, A., "Variable threshold resist model," SPIE 3679 (1999)
- Jolliffe, I.T., "Principal component analysis," Springer (2002)
- Hastie, T. et al., "The elements of statistical learning," Springer (2001)

## 태그
`Model`, `OPC`, `MachineLearning`, `PCR`, `PrincipalComponentRegression`, `PCA`, `LinearRegression`, `FragmentMovement`, `EarlyML`, `Berkeley`, `SPIE`, `ConcentricCircleSampling`
