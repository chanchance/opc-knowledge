# OPC Resist Model Separability Validation After SMO Source Change

## 메타데이터
- **저자**: Gillijns, W., Van de Kerkhove, J., Trivkovic, D., De Bisschop, P., Rio, D., Hsu, S., Feng, M., Zhang, Q., Liu, H.-Y. (imec / Synopsys / TSMC)
- **연도**: 2013
- **게재지**: Proc. SPIE 8683, Optical Microlithography XXVI
- **DOI/URL**: https://doi.org/10.1117/12.2011879
- **인용수**: ~40

## 핵심 요약
SMO(Source-Mask Optimization)를 위해 분리 가능한(separable) 레지스트 모델이 필요하다는 전제 하에, 완전히 캘리브레이션된 레지스트 모델에서 출발하여 새로운 광원으로 교체한 후 레지스트 모델 파라미터를 변경하지 않고도 신뢰할 수 있는 OPC 모델을 얻을 수 있는지 검증한다. 광원 교체 전/후 레지스트 모델 분리 가능성의 한계와 조건을 실험적으로 규명한다.

## 주요 기여
1. SMO 광원 변경 후 레지스트 모델 파라미터 재사용 가능성 실험적 검증
2. 레지스트 모델 분리 가능성의 조건(이미지 특성 분포 유사성) 정량적 평가
3. 분리 가능 모델로 SMO 워크플로우 가속화하는 실용적 프레임워크 제시
4. 광원 변경 크기에 따른 모델 재사용 가능성 한계 분석
5. 재캘리브레이션 필요 여부 자동 판단 기준 제안

## 모델 수식/아키텍처

**분리 가능 OPC 모델 전제:**
```
CD = g_resist(I_aerial(mask, source), θ_resist)
```
I_aerial = 광원·마스크 의존 공중상
θ_resist = 광원과 독립적인 레지스트 파라미터

**광원 교체 테스트:**
```
Source_1 (초기 광원) → 캘리브레이션 → θ_resist^1
Source_2 (SMO 후 최적 광원)
검증: CD_sim(mask, Source_2, θ_resist^1) ≈ CD_meas(mask, Source_2)?
```

**이미지 특성 분포 비교:**
```
Feature_distribution(Source) = {NILS, contrast, image_slope, ...}
Δdistribution = KL_divergence(Feature_dist_1, Feature_dist_2)
→ Δdistribution < threshold → 모델 재사용 가능
```

**분리 가능성 한계 메트릭:**
```
RMS_reuse(Source_2) = sqrt(mean((CD_sim(θ_resist^1) - CD_meas)²))
RMS_recal(Source_2) = sqrt(mean((CD_sim(θ_resist^2) - CD_meas)²))
Separability_OK: RMS_reuse < 1.1 × RMS_recal
```

**광원 변경 범위별 결과:**
```
Small SMO change (σ < 5%): Separability OK → 재사용 가능
Large SMO change (σ > 15%): Separability FAIL → 재캘리브레이션 필요
Moderate change: 패턴별 평가 필요
```

## 모델 유형
- [x] 광학 모델 (SMO 광원 모델)
- [x] 레지스트 모델 (분리 가능성 검증)
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- skopc SMO + OPC 통합 플로우에서 레지스트 모델 재사용 여부 자동 판단
- SMO 후 이미지 특성 분포 비교 → 분리 가능성 테스트 자동화
- 재사용 가능한 경우: SMO → 광학 커널 업데이트만으로 새 OPC 모델 완성
- 재캘리브레이션 필요한 경우: 새 SEM 측정 데이터 수집 → 재캘리브레이션
- imec/TSMC SMO 워크플로우의 레지스트 모델 관리 핵심 논문

## 참고문헌
- Liu, Y. et al., "Separable OPC models for computational lithography" (2008)
- Zuniga, C. et al., "CM1 standard process model" (2007)
- Adam, K. et al., "Calibration of physical resist models" (2009)

## 태그
`Model`, `SPIE`, `SMO`, `ResistModel`, `Separability`, `OPCModel`, `SourceChange`, `Portability`, `2013`
