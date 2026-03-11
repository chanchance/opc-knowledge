# Pupil Optimization of EUV Low-n Attenuated Phase Shift Mask for Improvement of Random Contact Hole Patterning

## 메타데이터
- **저자**: (SPIE 13424 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 3050373 (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3050373

## 핵심 요약
EUV low-n 감쇠 위상 이동 마스크(attenuated PSM)의 퓨필 최적화를 통해 랜덤 컨택 홀 패터닝 성능을 향상시킨다. Low-n AttPSM의 위상 이동 효과와 퓨필(소스) 형상을 공동으로 최적화하여 컨택 홀의 공정 창을 최대화하고 LCDU를 최소화하는 전략을 제시한다.

## 주요 기여
1. **퓨필-Low-n PSM 공동 최적화**: 소스 퓨필 형상과 low-n AttPSM을 동시에 최적화
2. **랜덤 컨택 홀 패터닝 향상**: 비주기적 2D 컨택 홀 어레이에서 공정 창 개선
3. **위상 이동 + 저굴절률 시너지**: AttPSM의 위상 효과와 low-n NILS 향상의 결합
4. **LCDU 감소**: 퓨필 최적화로 컨택 홀 크기 균일성 향상

## 알고리즘/수식
### Low-n AttPSM 퓨필 최적화
```
Low-n AttPSM 특성:
  굴절률 n < n_TaBN (예: n ≈ 0.87 @ 13.5nm)
  흡수 계수 k → 위상 이동 + 감쇠 동시 구현
  위상 이동: φ = 4π/λ × n × t (마스크 두께 t)
  → 배경 필드와 위상 차이 → 이미지 콘트라스트 향상

퓨필 최적화:
  max_{J(fx,fy)} NILS(contact_hole)
  subject to: pupil_constraints, source_shape_rules

  컨택 홀용 최적 소스:
    - 환형(annular) 또는 퀘이사(Quasar)
    - Low-n PSM 위상 이동각에 맞는 결간섭 조건
    - 수직/수평 주기적 + 비주기적 컨택 동시 최적화
```

### 랜덤 컨택 최적화 지표
```
랜덤 컨택 홀 성능:
  LCDU: 국소 CD 균일성 (3σ)
  EL (Exposure Latitude): 도즈 허용 범위
  DOF: 포커스 허용 범위

Low-n AttPSM + 퓨필 최적화 효과:
  NILS_opt > NILS_TaBN (동일 퓨필)
  EL_opt > EL_TaBN
  LCDU_opt < LCDU_TaBN
  → 컨택 홀 수율 향상
```

## OPC 툴 SMO 구현 관련성
- Low-n AttPSM SMO: SKOPC SMO에서 low-n 감쇠 위상 이동 마스크 광학 모델 지원
- 컨택 홀 SMO: 비주기적 2D 컨택 홀 레이아웃을 위한 소스-마스크 최적화
- 퓨필 최적화 통합: SMO 비용 함수에 컨택 홀 NILS/LCDU 지표 통합
- 마스크 타입 분기: TaBN vs Low-n AttPSM에 따른 SMO 전략 분기 지원

## 태그
`pupil_optimization`, `low_n`, `attenuated_PSM`, `EUV`, `contact_hole`, `LCDU`, `NILS`, `SMO`, `source_optimization`, `SPIE`, `2025`
