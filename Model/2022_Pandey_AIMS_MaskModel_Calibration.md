# Aerial Image Metrology (AIMS) Based Mask-Model Accuracy Improvement for Computational Lithography

## 메타데이터
- **저자**: Pandey, N. et al. (ASML / Carl Zeiss SMT / imec)
- **연도**: 2022
- **게재지**: Proc. SPIE 12293, Photomask Technology 2022
- **DOI/URL**: https://doi.org/10.1117/12.2641724
- **인용수**: ~15

## 핵심 요약
ZEISS AIMS EUV 툴을 이용한 직접 공중상 측정(aerial image metrology)으로 컴퓨테이셔널 리소그래피 OPC 모델 정확도를 향상시키는 방법을 연구한다. EPE(엣지 배치 오차) 버짓에 영향을 미치는 마스크 효과를 정량화하고, OPC 모델 캘리브레이션에 AIMS 측정을 활용하는 실현 가능성을 입증한다. EUV 마스크 패턴 변동성의 정확한 메트롤로지 방법론을 제시한다.

## 주요 기여
1. AIMS EUV 직접 공중상 측정 → OPC 모델 정확도 향상 루프 구축
2. 마스크 패턴 변동성이 EPE 버짓에 미치는 영향 정량화
3. CD-SEM 대비 AIMS 기반 OPC 모델 캘리브레이션의 장단점 분석
4. EUV 마스크 3D 효과를 AIMS 측정으로 검증하는 방법론
5. 고NA EUV 리소그래피를 위한 마스크 모델 정확도 향상 경로 제시

## 모델 수식/아키텍처

**AIMS 측정 기반 공중상 비교:**
```
AIMS_image(x,y) ≈ I_litho_tool(x,y)  [스케일링 후]
```
AIMS: 리소그래피 툴의 광학 조건(NA, σ, 파장)을 재현하여 마스크 이미지 측정

**모델 캘리브레이션 목적함수 (AIMS 기반):**
```
min_θ Σ_patterns ||I_sim(θ, mask_pattern) - I_AIMS(mask_pattern)||²_L2
```
I_sim = 시뮬레이션 공중상, I_AIMS = AIMS 측정 공중상

**CD 편차 (마스크 변동성 기여):**
```
ΔCD_mask = ∂CD/∂CD_mask · ΔCD_mask + ∂CD/∂phase · Δphase
```
마스크 CD 변동 및 위상 오차의 인쇄 CD에 대한 감도

**EPE 버짓 분해:**
```
σ_EPE_total² = σ_optical² + σ_resist² + σ_mask_3D² + σ_mask_CD² + σ_process²
```
AIMS 측정으로 σ_mask_3D 및 σ_mask_CD 직접 정량화 가능

**마스크 모델 검증 메트릭:**
```
Model_accuracy = 1 - ||I_sim - I_AIMS||² / ||I_AIMS||²
```

## 모델 유형
- [x] 광학 모델 (마스크 3D 모델 검증)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- AIMS 측정 데이터를 OPC 마스크 모델 캘리브레이션 입력으로 활용
- 기존 CD-SEM만으로는 마스크 3D 효과를 분리하기 어려움
- skopc 마스크 모델 캘리브레이션 시 AIMS 데이터 지원 고려
- EUV 고NA(0.55NA)로 전환 시 마스크 3D 효과 더욱 중요
- 마스크 패턴 변동성 → OPC 모델 파라미터 불확도로 연결

## 참고문헌
- Szucs, A. et al., "Advanced OPC Mask-3D and Resist-3D modeling" (2014)
- Erdmann, A. et al., "Mask 3D effects on resist model calibration" (2009)
- Neureuther, A.R. et al., "EUV OPC modeling requirements" (2014)

## 태그
`Model`, `SPIE`, `AIMS`, `MaskModel`, `EUV`, `Calibration`, `EPE`, `Mask3D`, `Metrology`, `HighNA`, `2022`
