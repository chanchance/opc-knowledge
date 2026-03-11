# Reducing Systematic LCDU of Dense Contact Hole Arrays on Wafer via Source Optimization

## 메타데이터
- **저자**: Joern-Holger Franke, Lieve Van Look, Andreas Frommhold, Alberto Colina, Gijsbert Rispens, David Rio, Eelco van Setten, Mark Maslow
- **소속**: imec (벨기에), ASML
- **연도**: 2023
- **게재지**: Proc. SPIE 12915, Photomask Japan 2023: XXIX Symposium on Photomask and Next-Generation Lithography Mask Technology, 1291508 (29 September 2023)
- **DOI/URL**: https://doi.org/10.1117/12.2685814

## 핵심 요약
EUV 리소그래피 메모리 응용의 콘택트 홀 변동성 문제에서 배경 회절 강도(BGI, Background diffraction Intensity)가 마스크 변동성에 의해 유발하는 공중 이미지 LCDU를 분석하고, 소스 최적화로 체계적 LCDU를 감소하는 방법을 제시한다. 대구경(large sigma) 동공이 소구경 동공 대비 LCDU를 효과적으로 줄임을 이론 및 실험으로 검증한다.

## 주요 기여
1. **BGI 기반 LCDU 분석**: 마스크 변동성이 야기하는 배경 회절 강도(BGI)의 웨이퍼 LCDU 예측 모델
2. **대구경 동공 우월성 입증**: 대구경(large sigma) 동공이 BGI 전달을 억제하여 LCDU 감소
3. **소스 최적화 LCDU 제어**: 소스 형상 최적화로 체계적 LCDU 감소 전략
4. **실험적 검증**: 예측된 웨이퍼 LCDU와 실험 데이터 비교 검증

## 알고리즘/수식
### BGI 기반 LCDU 분석
```
배경 회절 강도 (BGI):
  BGI 스펙트럼 = 콘택트 홀 형상에 의한 공간 주파수 성분
  → 주로 작은 공간 주파수에 집중

렌즈 전달 함수 의존성:
  LCDU_wafer ∝ Σ_{f} BGI(f) × |H(f, pupil_σ)|²

대구경(large sigma) 동공 효과:
  σ_large: BGI 전달 감소 → LCDU ↓
  σ_small: BGI 전달 증가 → LCDU ↑

소스 최적화 목표:
  min_{J} LCDU_wafer(J)
  = min_{J} Σ_f BGI(f) × T_BGI(f, J)

  여기서 T_BGI(f, J): 소스 J에서의 BGI 전달률
```

### LCDU 예측 모델
```
마스크 변동성 → BGI 스펙트럼 계산
BGI × 동공 전달 함수 → 공중 이미지 LCDU 예측
공중 이미지 LCDU → 웨이퍼 LCDU (레지스트 모델 포함)
```

## OPC 툴 SMO 구현 관련성
- EUV 콘택트 홀 SMO에서 LCDU 항목을 비용 함수에 명시적 포함 필요
- BGI 기반 LCDU 분석: 소스 설계 시 BGI 전달 최소화 조건 통합
- 소스 시그마(sigma) 크기가 LCDU에 미치는 영향: SMO 소스 파라미터 설계 지침
- 메모리 콘택트 홀 레이어의 소스 최적화에서 LCDU가 주요 메트릭

## 태그
`source_optimization`, `EUV`, `LCDU`, `contact_hole`, `BGI`, `mask_variability`, `sigma`, `pupil`, `DRAM`, `imec`, `ASML`, `SPIE`
