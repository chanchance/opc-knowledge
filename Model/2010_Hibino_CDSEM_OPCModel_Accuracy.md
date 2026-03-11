# High-Accuracy OPC-Modeling by Using Advanced CD-SEM Based Contours in the Next-Generation Lithography

## 메타데이터
- **저자**: Hibino, T. et al. (Toshiba Corporation)
- **연도**: 2010
- **게재지**: Proc. SPIE 7638, Metrology, Inspection, and Process Control for Microlithography XXIV
- **DOI/URL**: https://doi.org/10.1117/12.846025
- **인용수**: ~45

## 핵심 요약
기존 1D CD 측정 기반 OPC 모델 캘리브레이션의 한계를 극복하기 위해 고급 CD-SEM 컨투어(2D 엣지 프로파일)를 활용하는 고정밀 OPC 모델 캘리브레이션 방법론을 제안한다. SEM 컨투어 기반 캘리브레이션이 1D 전용 캘리브레이션 대비 2D 패턴(코너, T자형 등) 예측 정확도를 크게 향상시킴을 실증한다.

## 주요 기여
1. CD-SEM 컨투어 추출 → OPC 모델 캘리브레이션 통합 플로우 구축
2. 1D 전용 캘리브레이션 vs. 1D+2D 하이브리드 캘리브레이션 비교
3. 2D 구조(코너, T-junctions) 예측 오차 50% 이상 감소
4. 컨투어 수축 보정(shrink correction) 적용으로 RMS 오차 12% 추가 감소
5. 차세대 리소그래피(10nm 노드 이하)를 위한 메트롤로지 요구사항 제시

## 모델 수식/아키텍처

**SEM 컨투어 추출:**
```
contour(x,y) = {(x,y) | I_SEM(x,y) = I_threshold}
```
I_threshold = SEM 이미지 강도 임계값 (자동 결정)

**컨투어 수축 보정 (Shrink Correction):**
```
CD_corrected = CD_SEM + ΔCD_shrink(dose_SEM, material)
```
ΔCD_shrink: SEM 전자빔에 의한 레지스트 수축 보정값

**하이브리드 캘리브레이션 목적함수:**
```
min_{θ} [ w_1D · ||CD_1D_sim(θ) - CD_1D_meas||²
         + w_2D · ||contour_sim(θ) - contour_SEM||²_Hausdorff ]
```
- w_1D, w_2D = 1D/2D 가중치
- Hausdorff 거리: 두 컨투어 간 최대 최소 거리

**EPE 계산 (컨투어 기반):**
```
EPE(s) = signed_distance(contour_sim(s), contour_ref(s))
```
s = 컨투어 호 길이 파라미터

## 모델 유형
- [ ] 광학 모델
- [x] 레지스트 모델 (컨투어 기반 캘리브레이션)
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- OPC 모델 캘리브레이션 게이지: 1D 라인/스페이스 외 2D 구조 반드시 포함
- SEM 컨투어 활용으로 게이지 포인트 수 감소하면서도 2D 정확도 향상
- skopc/modeling/calibration/ 구현 시 컨투어 기반 EPE 메트릭 추가
- 실제 생산 환경: 게이지 포인트 수백~수천 개 필요

## 참고문헌
- Cobb, N. et al., "SEM image contouring for OPC model calibration" (2007)
- Zuniga, C. et al., "CM1 standard process model" (2007)
- Mentor Graphics Calibre contour-based calibration

## 태그
`Model`, `SPIE`, `CDSEM`, `Contour`, `OPCModel`, `Calibration`, `2D`, `EPE`, `10nmNode`, `2010`
