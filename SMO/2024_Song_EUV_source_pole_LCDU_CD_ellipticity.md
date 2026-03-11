# EUV Source Pole Control for LCDU and CD Ellipticity Handling in Hexagonal Contact Arrays

## 메타데이터
- **저자**: Jieun Song, Janghun Kim, Hyung Jong Bae, et al.
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 1295309 (April 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010718

## 핵심 요약
육각형 콘택트 배열(hexagonal contact arrays) 패턴에서 EUV 동공(pupil)의 중심 시그마(center sigma) 위치 제어를 통한 LCDU 개선 방법을 제시한다. 소스 점이 동공 외측 가장자리에 위치할 때 NILS와 무관하게 LCDU가 향상되며, CD 타원율(CD ellipticity) 제어를 통해 LCDU를 추가 개선하거나 결함 소스를 줄일 수 있음을 실험으로 검증한다.

## 주요 기여
1. **시그마 중심 위치 제어**: 동공 내 소스 점의 시그마 중심 위치가 LCDU에 미치는 영향 정량화
2. **LCDU-CD 타원율 상관관계**: LCDU와 ADI(After Development Inspection) CD 타원율의 상관관계 검증
3. **3-빔 이미징 최적화**: 3-빔 이미징 영역 중심 방향 이동에 따른 CD 타원율 변화 활용
4. **DRAM 콘택트 최적화**: 육각형 피치 40nm 콘택트 배열에서의 실험적 검증

## 알고리즘/수식
### 시그마 중심 위치와 LCDU 관계
```
동공 좌표: (σ_x, σ_y) ∈ 단위 원

LCDU 관계:
  LCDU_outer < LCDU_inner
  (외측 가장자리 소스 < 내측 소스)

  이유: BGI(배경 회절 강도) 전달 감소
       외측 sigma → 더 넓은 spatial frequency 필터링

3-빔 이미징 영역:
  HEX 배열 특수 조명: 3개의 회절 차수가 렌즈 통과
  중심 이동: σ_center → 3-빔 영역 중심
           → CD_critical_direction 증가
           → CD 타원율(ellipticity) 변화
```

### CD 타원율 제어
```
CD_ellipticity = CD_x / CD_y  (또는 CD_y / CD_x)

목표:
  LCDU 개선: |CD_ellipticity - 1| 최소화
  또는
  결함 소스 감소: 특정 방향 CD 증가로 브리징/오픈 여유 확보

최적화:
  min_{σ_center} LCDU(σ_center)
  subject to: CD_ellipticity ∈ [허용 범위]
```

## OPC 툴 SMO 구현 관련성
- 육각형 콘택트 배열 EUV 소스 최적화: DRAM SNLP/BLP 레이어의 SMO 비용 함수에 LCDU 항 포함
- 시그마 중심 위치: 소스 파라미터 최적화에서 동공 가장자리 편향 조건 고려
- CD 타원율 제어: SMO 비용 함수에 방향별 CD 차이 패널티 항 추가
- 3-빔 이미징 특수 조건: 육각형 피치 패턴에서 SMO 조명 표현 방법 특수화 필요

## 태그
`source_optimization`, `EUV`, `LCDU`, `CD_ellipticity`, `hexagonal_contact`, `sigma_control`, `DRAM`, `3_beam_imaging`, `pupil`, `SPIE`
