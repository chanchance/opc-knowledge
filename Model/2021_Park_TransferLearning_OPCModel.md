# Accurate Litho Model Tuning Using Design-Based Defect Binning and Transfer Learning

## 메타데이터
- **저자**: Park, J. et al. (Samsung Electronics / Synopsys)
- **연도**: 2021
- **게재지**: Proc. SPIE 11614, Optical and EUV Nanolithography XXXIV
- **DOI/URL**: https://doi.org/10.1117/12.2583101
- **인용수**: ~18

## 핵심 요약
설계 기반 결함 분류(design-based defect binning)와 전이 학습(transfer learning)을 결합하여 리소그래피 모델을 정밀 튜닝(fine-tuning)하는 방법론을 제안한다. 기존에 캘리브레이션된 OPC 모델을 소스 도메인으로 활용하고, 새로운 공정 조건(다른 레이어, 다른 노드)의 소량 측정 데이터로 신속하게 도메인 적응(domain adaptation)을 수행한다. 전이 학습 적용 시 새 도메인에서의 모델 정확도가 처음부터 재캘리브레이션하는 것과 동등하면서 데이터/시간은 60% 절감함을 실증한다.

## 주요 기여
1. OPC 리소그래피 모델에 전이 학습 적용 최초 체계적 연구
2. 설계 기반 결함 분류로 전이 학습 타겟 패턴 효율적 선별
3. 소스→타겟 도메인 전이: 60% 데이터 절감으로 동등 모델 정확도
4. 공정 변화(도즈, 포커스, 레이어) 에 따른 전이 가능성 분석
5. 양산 환경에서의 모델 유지보수(maintenance) 비용 절감 실증

## 모델 수식/아키텍처

**소스 도메인 모델 (기학습):**
```
f_source(x; θ_source): pattern → CD_prediction
θ_source = [θ_optical, θ_resist, θ_etch]   [사전 학습 파라미터]
```

**전이 학습 (파인튜닝):**
```
θ_target = θ_source + Δθ
min_{Δθ} L_target(θ_source + Δθ) + λ · ||Δθ||²
```
λ = 정규화 계수 (소스 파라미터로부터의 이탈 억제)

**도메인 적응 손실:**
```
L_total = L_target_data + λ_reg · L_regularization + λ_align · L_domain_align
L_domain_align = MMD(features_source, features_target)
```
MMD = Maximum Mean Discrepancy (두 분포 간 거리)

**설계 기반 결함 분류 (타겟 패턴 선별):**
```
defect_score(pattern) = sim_distance(pattern, known_hotspot_library)
→ 상위 K% 패턴 선별 → 전이 학습 캘리브레이션 게이지로 사용
```

**데이터 효율성:**
```
N_transfer = 0.4 × N_full_calibration  (60% 절감)
RMS_transfer ≈ RMS_full   (동등 정확도)
```

## 모델 유형
- [ ] 광학 모델
- [ ] 레지스트 모델
- [x] ML/DL (전이 학습, 도메인 적응)
- [x] 하이브리드 (물리 OPC 모델 + 전이 학습 파인튜닝)

## OPC 툴 구현 관련성
- 새 공정 노드/레이어 전환 시 OPC 모델 재캘리브레이션 비용 절감
- skopc 모델 유지보수 모듈에 전이 학습 파인튜닝 기능 추가 가능
- 소스 도메인: 동일 툴의 이전 레이어 또는 이전 노드 모델
- 타겟 도메인: 새 레이어/노드 소량 SEM 측정 데이터
- 결함 분류 기반 게이지 선별: 핫스팟 패턴에 집중하여 전이 효율 극대화

## 참고문헌
- Huang, Y.-H. et al., "Effective OPC model calibration using ML" (2022)
- Hibino, T. et al., "High-accuracy OPC modeling with CD-SEM contours" (2010)
- Pan, S.J. and Yang, Q., "Survey on transfer learning" (IEEE TKDE, 2010)

## 태그
`Model`, `SPIE`, `TransferLearning`, `DomainAdaptation`, `OPCModel`, `FineTuning`, `MachineLearning`, `Calibration`, `2021`
