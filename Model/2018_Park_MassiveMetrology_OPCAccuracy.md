# Massive Metrology Using Fast E-Beam Technology Improves OPC Model Accuracy by >2x at Faster Turnaround Time

## 메타데이터
- **저자**: Park, C. et al. (Samsung Electronics / KLA)
- **연도**: 2018
- **게재지**: Proc. SPIE 10585, Metrology, Inspection, and Process Control for Microlithography XXXII
- **DOI/URL**: https://doi.org/10.1117/12.2299971
- **인용수**: ~35

## 핵심 요약
고속 전자빔(fast e-beam) 메트롤로지 기술을 활용하여 대규모 OPC 모델 캘리브레이션 게이지 측정을 가능하게 함으로써 OPC 모델 정확도를 2배 이상 향상시키면서도 처리 속도(TAT)를 단축하는 방법론을 제시한다. 기존 단일 컬럼 CD-SEM 대비 다중 컬럼 e-beam 시스템으로 동일 시간에 10× 이상 많은 게이지 측정이 가능함을 실증한다.

## 주요 기여
1. 다중 컬럼 고속 e-beam으로 OPC 게이지 측정 처리량 10× 향상
2. 게이지 수 증가(1K→10K+)에 따른 OPC 모델 정확도 향상 스케일링 분석
3. 대규모 게이지에서의 통계적 노이즈 감소 및 모델 견고성 향상
4. 게이지 수 vs. 모델 정확도의 수렴 분석 (수확 체감 구간 도출)
5. 양산 환경에서 대규모 메트롤로지 기반 OPC 워크플로우 구축 가이드

## 모델 수식/아키텍처

**측정 노이즈 vs. 게이지 수 관계:**
```
σ_model_error ∝ σ_measurement / √N_gauges
```
→ 게이지 수 4× 증가 시 측정 노이즈 기여도 2× 감소

**모델 정확도 스케일링:**
```
RMS_model(N) = RMS_floor + (RMS_0 - RMS_floor) · exp(-N/N_half)
```
RMS_floor = 게이지 무한대 시 최소 RMS (공정 고유 변동)
N_half = 정확도 절반 달성 게이지 수

**게이지 대표성 평가:**
```
Coverage(N) = fraction of feature-space covered by N gauges
→ N이 증가하면서 Coverage 포화 → 최적 N 결정
```

**고속 e-beam 처리량:**
```
Throughput_multi-column = K × Throughput_single-column
K = 컬럼 수 (예: 9~16 컬럼)
TAT_reduction ≈ 1/K  (동일 게이지 수 기준)
```

**OPC 모델 RMS 개선:**
```
RMS(1K gauges): ~2.0nm
RMS(10K gauges): ~0.9nm  (>2× 개선)
```

## 모델 유형
- [ ] 광학 모델
- [ ] 레지스트 모델
- [ ] ML/DL
- [x] 하이브리드 (메트롤로지 인프라 + OPC 모델 캘리브레이션)

## OPC 툴 구현 관련성
- OPC 모델 정확도는 게이지 수에 크게 의존 → 대규모 메트롤로지 투자 필요
- skopc 캘리브레이션 모듈: 게이지 수 스케일링 분석 기능 추가
- 최적 게이지 수: 수확 체감 분석으로 비용 대비 최적 N 결정
- 고속 e-beam(KLA eSL10, ASML HMI): 대규모 메트롤로지 표준 툴
- 게이지 다양성(1D/2D, pitch/CD/방향) + 충분한 수량이 모델 품질 결정

## 참고문헌
- Hibino, T. et al., "High-accuracy OPC modeling with CD-SEM contours" (2010)
- Huang, Y.-H. et al., "Effective OPC model calibration using ML" (2022)
- Zuniga, C. et al., "CM1 standard process model" (2007)

## 태그
`Model`, `SPIE`, `Metrology`, `EBeam`, `MassiveMetrology`, `OPCCalibration`, `GaugeCount`, `Accuracy`, `2018`
