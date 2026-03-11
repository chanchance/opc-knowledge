# 3D Mask Effects in High NA EUV Imaging

## 메타데이터
- **저자**: Andreas Erdmann, Peter Evanschitzky, Gerardo Bottiglieri, Eelco van Setten, Timon Fliervoet
- **연도**: 2019
- **게재지**: Proc. SPIE 10957, Extreme Ultraviolet (EUV) Lithography X, 109570Z
- **DOI/URL**: https://doi.org/10.1117/12.2515678
- **인용수**: ~50

## 핵심 요약
High-NA EUV 리소그래피(NA=0.55)에서 마스크 3D 효과(M3D)의 이해, 특성화, 관리 방법을 체계적으로 분석한다. 단순화된 가간섭 이미징 모델, 리고러스 마스크 회절 시뮬레이션, 하이브리드 마스크 모델을 활용하여 비텔레센트리시티(non-telecentricity), 대비 저하(contrast fading), 최적 포커스 이동(best focus shift) 등의 M3D 유발 이미징 아티팩트 근본 원인을 분석하고, 마스크 및 소스 수정을 통한 이미지 개선 전략을 제시한다.

## 주요 기여
1. High-NA EUV M3D 효과 (비텔레센트리시티, 대비, 포커스 시프트) 체계적 분석
2. 간소화 가간섭 모델 + 리고러스 EMF 시뮬 결합 분석 방법론
3. M3D 유발 아티팩트 보상 전략 (마스크 + 소스 수정)
4. High-NA EUV OPC/SMO에서 M3D 보정 필요성 정량화

## Recipe/Process Flow 상세

### High-NA EUV와 M3D 효과의 심화
```
EUV 리소그래피 시스템:
  현재 NA=0.33 (ASML NXE) → High-NA=0.55 (ASML EXE)
  파장: λ=13.5nm (반사형 광학계)
  마스크: 반사형 (Mo/Si 다층막 + 흡수체)
  조명: 6° 오프-액시스 → 반사광 수집

M3D 효과의 원인:
  마스크 두께 ~ EUV 파장과 비교 가능
  흡수체 두께: 56~75nm (TaN, TaBN)
  → 흡수체 3D 형상이 근접장 전자기 회절에 영향
  → 근접장 스펙트럼 왜곡 → 이미징 아티팩트

High-NA에서 M3D 심화:
  더 큰 조명 각도 범위
  더 높은 해상도 → 작은 피처에서 M3D 비율 증가
  High-NA 광학계 중심 차폐(central obscuration) 추가 효과
```

### 주요 M3D 효과 분석
```
1. 비텔레센트리시티 (Non-telecentricity):
   원인: 경사 조명 + 마스크 3D 형상 → 마스크 면에서 텔레센트릭 벗어남
   현상: 패턴 위치에 따른 이미지 이동 (Image placement error)
   수식:
     δx ≈ -α × (M3D_induced phase gradient)
   High-NA에서 심화: 큰 조명 각도 → 비텔레센트리시티 증가

2. 대비 저하 (Contrast Fading):
   원인: M3D → 마스크 회절 효율 감소 → 이미지 대비 저하
   현상: ILS (Image Log Slope) 감소 → 공정 마진 감소
   패턴 의존성: pitch/CD별 M3D 대비 저하 패턴 다름

3. 최적 포커스 이동 (Best Focus Shift):
   원인: M3D → 주파수별 위상 오차 → 포커스 이동
   현상: H-라인 vs. V-라인 최적 포커스 불일치
   크기: ±수십 nm (NA=0.33), ±더 큼 (NA=0.55)
   OPC 영향: 포커스 시프트 보상 OPC (Z-shift OPC) 필요
```

### 분석 방법론
```
단순화 가간섭 이미징 모델:
  각 소스점에 대한 마스크 회절 스펙트럼 분석
  Zernike 다항식으로 위상 오차 분해
  → M3D 효과를 광학 수차 형태로 표현
  계산: 빠름 → 설계 공간 탐색 유용

리고러스 마스크 회절 시뮬레이션:
  RCWA (Rigorous Coupled Wave Analysis)
  3D 흡수체 형상 완전 모델링
  정확도: 높음, 속도: 느림 → 검증에 활용

하이브리드 마스크 모델:
  리고러스 시뮬 → 보정 계수 추출 → 빠른 모델에 적용
  방법: Hopkins 모델에 M3D 보정항 추가
    I_hybrid(M) = I_Hopkins(M) × M3D_correction(pattern)
  OPC 루프: 하이브리드 모델로 M3D 보정 OPC 실용화
```

### M3D 보정 전략
```
마스크 수정:
  흡수체 두께 최소화: M3D 효과 감소 → 비텔레센트리시티 감소
  Alternative 흡수체: 낮은 n, 높은 k 흡수체 (M3D 최소화)
  마스크 바이어스: 패턴별 M3D 보정 마스크 CD 조정

소스 수정 (SMO):
  조명 최적화로 M3D 유발 비대칭 보상
  EUV SMO: 비텔레센트리시티 보상 소스 설계
  제한: 소스-마스크 동시 최적화 필요

OPC 통합:
  M3D 인식 OPC: 흡수체 두께 기반 M3D 보정 OPC 오프셋
  H-V 포커스 시프트 보상: 방향별 OPC 차별화
  패턴 위치 보정: 비텔레센트리시티 유발 IPE OPC 보정
```

### High-NA EUV에서의 추가 M3D 과제
```
중심 차폐 (Central Obscuration):
  High-NA EUV 투영 광학계의 구조적 특성
  조명 각도 범위 변화 → 마스크 근접장 구조 변경
  M3D 효과 패턴 변화 → 재최적화 필요

마스크 방향성 (Mask Orientation):
  H-라인 vs. V-라인 M3D 효과 다름
  설계 규칙: Critical layer에서 방향 제한 고려 필요
```

## OPC 툴 구현 관련성
- **SKOPC EUV M3D OPC**: `skopc/modeling/litho_engine.py`에 M3D 보정 계수 통합
- **하이브리드 M3D 모델**: Hopkins 기반 OPC에 M3D 보정항 추가 (패턴별 오프셋)
- **H-V 비대칭 OPC**: 방향별 OPC 바이어스로 M3D 포커스 시프트 보상
- **SMO 통합**: EUV M3D 인식 SMO로 소스 + 마스크 동시 M3D 보정

## 참고문헌
- Proc. SPIE 10957, EUV Lithography X (March 2019)
- 저자 소속: Fraunhofer IISB + ASML
- 관련: EUV OPC modeling requirements (SPIE 9048, 2014)
- 관련: EUV M3D generative network prediction (JMM 2021)
- 관련: 3D mask effects high-k absorber (EUV Symposium 2023)

## 태그
`Recipe`, `SPIE`, `EUV`, `HighNA`, `Mask3D`, `M3D`, `NonTelecentricity`, `BestFocusShift`, `ContrastFading`, `OPC`, `SMO`, `Fraunhofer`, `ASML`, `2019`
