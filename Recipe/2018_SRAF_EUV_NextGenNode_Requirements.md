# SRAF Requirements, Relevance, and Impact on EUV Lithography for Next-Generation Beyond 7nm Node

## 메타데이터
- **저자**: (SPIE 10583 - 2018 SPIE Advanced Lithography)
- **연도**: 2018
- **게재지**: Proc. SPIE 10583, Extreme Ultraviolet (EUV) Lithography IX
- **DOI/URL**: https://doi.org/10.1117/12.2297109
- **인용수**: ~30

## 핵심 요약
EUV(극자외선) 리소그래피에서 SRAF(Sub-Resolution Assist Features)의 필요성, 관련성, 공정 영향을 체계적으로 분석한다. EUV(λ=13.5nm)에서 k1 인자, NA, 산란(flare), 마스크 3D 효과 등이 ArF와 다른 SRAF 설계 요구사항을 만든다. 7nm 이하 노드에서 EUV SRAF의 구현 과제와 해결 전략을 제시한다.

## 주요 기여
1. EUV 리소그래피에서 SRAF 필요성의 정량적 분석
2. EUV 고유 효과(flare, mask 3D, shadowing)가 SRAF 성능에 미치는 영향 규명
3. EUV SRAF 설계 규칙 개발 방법론
4. 7nm 이하 노드 EUV 양산을 위한 SRAF 구현 로드맵

## Recipe/Process Flow 상세

### EUV 리소그래피와 SRAF의 상호작용
```
ArF 리소그래피 (193nm):
  NA = 1.35 (액침)
  k1 = 0.25~0.35 (저 k1)
  SRAF: 공정 윈도우 확장에 필수
  SRAF 크기: 마스크 상 ~30-60nm (웨이퍼 상 < 20nm)

EUV 리소그래피 (13.5nm):
  NA = 0.33 (1세대) / 0.55 (High-NA)
  k1 = 0.4~0.5 (상대적으로 높음) → SRAF 필요성 낮을 수 있음?
  그러나 고해상도 패턴(7nm 이하)에서는 여전히 k1 저하
  SRAF 크기: 훨씬 작아짐 (마스크 상 < 20nm) → 마스크 제작 어려움

EUV 고유 도전 과제:
  1. Flare: 산란광 → SRAF 이미징에 영향
  2. 마스크 3D 효과: 흡수체 두께 → 위상 오차 → SRAF 성능 변화
  3. Off-axis illumination shadowing: 비대칭 조명 → SRAF 위치 최적화 재필요
  4. 반사형 마스크: 투과형 ArF 마스크와 다른 OPC 모델 필요
```

### EUV SRAF 설계 방법론
```
EUV SRAF 규칙 도출:
  1. EUV 광학 모델 수립
     - 마스크 3D 효과 포함 엄밀 EM 시뮬레이션
     - Flare 맵 측정 및 모델링
     - Off-axis illumination (dipole, quadrupole) 시뮬

  2. 1D SRAF 최적화
     공정 윈도우 최대화:
       DOF × EL 면적 최대화
       SRAF 위치: 주 패턴 에지에서의 거리
       SRAF 크기: MRC + 인쇄 마진 고려
     EUV 보정 인자:
       Flare 보상 바이어스
       마스크 3D 보상 위상 조정

  3. 2D SRAF 확장
     코너, 끝단(line-end), T-junction 처리
     EUV 마스크 제작 가능성(MRC) 기반 단순화

  4. 전체 칩 SRAF 삽입
     Rule-based: 1D/2D 규칙 테이블 적용
     Model-based: EUV 리소그래피 시뮬 기반 최적화
```

### EUV SRAF 마스크 제작 과제
```
SRAF 크기 요구:
  패턴 피치 16nm (웨이퍼) → 마스크 상 64nm (4× 축소)
  SRAF: 웨이퍼 상 < 8nm → 마스크 상 < 32nm
  현재 e-beam 마스크 작성기 해상도: 약 15-20nm
  → SRAF 마스크 제작이 매우 도전적

해결 방향:
  - SRAF 배치 위치 재최적화 (크기보다 위치로 보상)
  - Phase-Shift SRAF (EUV 위상 변조 활용)
  - Assist feature 없이 소스 최적화(SO)로 대체
  - High-NA EUV (NA=0.55)로 해상도 여유 확보
```

### 7nm 이하 노드 적용 결과
```
공정 윈도우 개선 (EUV SRAF 유무 비교):
  DOF 개선: SRAF 있음 > SRAF 없음
  Exposure Latitude(EL): SRAF로 개선
  MEEF 감소: 보조 패턴으로 마스크 민감도 완화

SRAF 효과가 두드러지는 조건:
  - 반고립(semi-isolated) 패턴
  - 밀도 변화 경계 영역
  - 라인-엔드 패턴
  Low k1 (< 0.4) 상황에서 효과 극대화
```

## OPC 툴 구현 관련성
- **SKOPC EUV 레시피**: `recipes/example_euv.yaml` SRAF 파라미터를 EUV 광학 특성에 맞춰 재설정
- **EUV 마스크 3D 효과**: `skopc/core/litho_engine.py`에 마스크 3D 시뮬레이션 옵션 추가 필요
- **Flare 보정**: EUV flare 맵 기반 OPC 타겟 보정 레이어
- **SRAF 규칙 테이블**: EUV용 별도 Space-Width 테이블 정의 (ArF와 다른 SRAF 크기/간격)

## 참고문헌
- Proc. SPIE 10583, Extreme Ultraviolet (EUV) Lithography IX (2018)
- 관련: Subresolution assist features impact in EUV lithography for beyond 7nm (JMM Vol.18, 2019)
- 관련: SRAF rule extraction and insertion based on ILT (SPIE 10961, 2019)
- 관련: Process window tripling with SRAF placement rules (IEEE, 2016)

## 태그
`Recipe`, `SPIE`, `SRAF`, `EUVLithography`, `NextGenNode`, `7nm`, `Flare`, `Mask3DEffect`, `ProcessWindow`, `EUV-OPC`, `2018`
