# Effective OPC Model Calibration Using Machine Learning

## 메타데이터
- **저자**: Huang, Y.-H., Yeh, S.-S., Mai, Y.-C., Lin, C.-C., Lai, J.-C.
- **연도**: 2022
- **게재지**: Proc. SPIE 12052, DTCO and Computational Patterning I
- **DOI/URL**: https://doi.org/10.1117/12.2611337
- **인용수**: ~20

## 핵심 요약
OPC 모델 캘리브레이션의 게이지 샘플링(gauge sampling)을 머신러닝으로 최적화하는 방법을 제안한다. 피처 수가 많은 공중상 기반 특성에 데이터 전처리·특성 변환·클러스터링을 적용하여 대표적 게이지 패턴을 효율적으로 선택한다. 동일한 모델 정확도를 달성하면서 SEM 측정 데이터 수집 시간을 크게 단축한다.

## 주요 기여
1. ML(클러스터링) 기반 OPC 게이지 샘플링 최적화 플로우
2. 공중상 특성(aerial image features) 기반 패턴 대표성 정량화
3. 중복 게이지 제거로 SEM 측정 비용 절감
4. 동일 정확도 달성 시 게이지 수 50% 이상 감소 실증
5. 다양한 기술 노드(ArF immersion, EUV)에 적용 가능한 범용 프레임워크

## 모델 수식/아키텍처

**게이지 패턴 특성 벡터 추출:**
```
feature(pattern_i) = [I_peak, S_edge, ΔI, pitch, CD, orientation,
                      I_min, I_max, NILS, curvature, loading_term, ...]
```
NILS = Normalized Image Log Slope = (CD/I) · |dI/dx|_edge

**특성 공간 변환 (PCA/정규화):**
```
z_i = (feature_i - μ) / σ   [Z-score 정규화]
z'_i = PCA(z_i)             [분산 95% 유지하는 주성분 선택]
```

**K-means 클러스터링:**
```
min_{C₁,...,C_K} Σ_k Σ_{i∈C_k} ||z'_i - μ_k||²
```
각 클러스터에서 대표 패턴 1개 선택 → 게이지 집합 구성

**캘리브레이션 품질 메트릭:**
```
RMS_residual = sqrt(1/N · Σ_i (CD_sim,i - CD_meas,i)²)
Coverage_score = 특성공간에서 선택된 게이지의 분산/전체분산
```

**효율성 평가:**
```
Efficiency = (RMS_original / RMS_ML_sampled) / (N_ML / N_original)
```

## 모델 유형
- [ ] 광학 모델
- [ ] 레지스트 모델
- [x] ML/DL (클러스터링 기반 게이지 선택)
- [x] 하이브리드 (ML 보조 + 물리 모델 캘리브레이션)

## OPC 툴 구현 관련성
- skopc 캘리브레이션 모듈에 ML 기반 게이지 선택 기능 추가 가능
- 게이지 패턴 특성 벡터: 공중상 계산 후 자동 추출
- 클러스터링으로 중복 패턴 제거 → 캘리브레이션 효율 향상
- 실제 생산 환경에서 SEM 측정 비용 절감에 직접 기여
- K-means 외 DBSCAN, GMM 등 다른 클러스터링 알고리즘도 적용 가능

## 참고문헌
- Zuniga, C. et al., "CM1 standard process model" (2007)
- Hibino, T. et al., "High-accuracy OPC modeling using CD-SEM contours" (2010)
- Huang et al., Synopsys OPC calibration ML papers

## 태그
`Model`, `SPIE`, `MachineLearning`, `Calibration`, `GaugeSampling`, `Clustering`, `OPCModel`, `Efficiency`, `2022`
