# Imaging Evaluation of Low Reflectivity Low-n EUV Mask for LS at 0.33NA

## 메타데이터
- **저자**: (SPIE 13177 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 13177, International Conference on Extreme Ultraviolet Lithography 2024, 131770O (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3032310

## 핵심 요약
0.33NA EUV에서 저반사율 저굴절률(low reflectivity low-n) EUV 마스크의 라인-공간(LS) 패턴 이미징 성능을 평가한다. 앵커 피치 28nm에서 노출 위도(EL)와 MEEF를 측정하고 TaBN 기반 마스크와 비교하여 low-n 마스크의 이미징 이점을 정량화한다.

## 주요 기여
1. **Low 반사율 Low-n 마스크 이미징**: 저반사율 low-n 마스크의 LS 이미징 성능 정량 평가
2. **28nm 앵커 피치 성능**: EUV 0.33NA 28nm 피치에서 EL, MEEF 비교
3. **TaBN 대비 성능 향상**: Low-n 마스크의 EL 향상 및 MEEF 감소 정량화
4. **반사율-이미징 연계**: 마스크 반사율이 이미징 성능에 미치는 영향 분석

## 알고리즘/수식
### Low 반사율 Low-n 마스크 이미징 모델
```
마스크 반사율 정의:
  R_mask = |r_absorber|² (흡수층 반사율)
  TaBN: R ≈ 0.5% (매우 낮음)
  Low-n: R ≈ 0.5~5% (조정 가능)

Low-n 이미징 이점:
  위상 이동 감소: φ_low-n < φ_TaBN
  → NILS 향상 → EL ↑, MEEF ↓

28nm 피치 메트릭 비교:
  EL(low-n) > EL(TaBN) at same dose
  MEEF(low-n) < MEEF(TaBN)

저반사율 효과:
  R 감소 → 배경 강도 감소 → 이미지 대비 향상
  단, R이 너무 낮으면 이미징 이점 소멸
```

### 실험 조건
```
마스크 타입: Low reflectivity low-n vs TaBN
피치: 28nm LS (0.33NA EUV 앵커 피치)
NA: 0.33
조명: 최적화된 소스 형상 (SMO 결과)
측정: EL, MEEF, NILS, DOF
```

## OPC 툴 SMO 구현 관련성
- Low-n 마스크 성능 데이터: SKOPC SMO/OPC에서 low-n 마스크 기대 성능 기준
- 28nm 피치 SMO: 0.33NA EUV 앵커 피치에서 low-n 마스크 소스 최적화
- MEEF 기반 마스크 선택: 동일 노드에서 TaBN vs low-n 마스크 선택 기준
- 반사율 영향 분석: OPC 모델에서 반사율 파라미터의 이미징 영향 정량화

## 태그
`EUV`, `low_n`, `low_reflectivity`, `LS`, `0p33NA`, `MEEF`, `EL`, `28nm_pitch`, `imaging`, `TaBN`, `OPC`, `SMO`, `SPIE`, `2024`
