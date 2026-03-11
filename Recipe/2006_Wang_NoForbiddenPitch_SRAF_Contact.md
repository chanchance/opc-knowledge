# No-Forbidden-Pitch SRAF Rules for Advanced Contact Lithography

## 메타데이터
- **저자**: Wang, Liu, Zhang, Hung (et al.)
- **연도**: 2006
- **게재지**: Proc. SPIE 6349, Photomask Technology 2006, 63494K
- **DOI/URL**: https://doi.org/10.1117/12.685071
- **인용수**: ~30

## 핵심 요약
콘택 레이어 리소그래피에서 SRAF 삽입이 어려운 금지 피치(forbidden pitch) 범위를 제거하는 대각선 서브해상도 보조 피처(DAF, Diagonal sub-resolution Assist Feature) 기반 SRAF 규칙 설계 방법론을 제시한다. 특정 피치 범위에서 수평/수직 방향 SRAF로는 공정 윈도우를 개선할 수 없는 금지 피치 현상을 분석하고, 대각선 SRAF로 이를 극복하여 전 피치 범위에서 균일한 공정 윈도우를 달성한다.

## 주요 기여
1. 콘택 레이어 금지 피치 현상의 물리적 분석
2. DAF(Diagonal Assist Feature)를 이용한 금지 피치 해소 방법론
3. 전 피치 범위에서 균일한 공정 윈도우 달성하는 SRAF 규칙 도출
4. 고 NA OAI + att-PSM 콘택 공정에서의 검증

## Recipe/Process Flow 상세

### 금지 피치(Forbidden Pitch) 현상
```
콘택 레이어 리소그래피 특성:
  - OAI(Off-Axis Illumination): 환형(annular), 쿼드러폴
  - att-PSM (attenuated Phase-Shift Mask) 사용
  - 이중 회절 모드 (0차 + ±1차)

피치에 따른 회절 분류:
  밀집 피치 (Dense pitch):
    0차 + ±1차 동시 통과 → 높은 NILS
    SRAF로 밀집 환경 모사 → 고립 패턴 개선 가능

  고립 패턴 (Isolated):
    0차만 통과 → 낮은 NILS
    SRAF로 밀집화 → 큰 공정 윈도우 향상

  금지 피치 (Forbidden Pitch):
    특정 중간 피치 범위
    SRAF 삽입 위치 없음 (물리적 간격 부족)
    또는 SRAF 삽입해도 공정 윈도우 향상 없음
    → 전체 피치 범위의 균일한 공정 윈도우 불가

금지 피치 발생 원인:
  조명 특성(σ_out, σ_in)과 피치의 상호작용
  특정 피치에서 SRAF의 항공 이미지 기여가 주 패턴과 파괴적 간섭
  → SRAF가 없는 것보다 나쁜 결과
```

### DAF(Diagonal Assist Feature) 기반 해결법
```
표준 SRAF (수평/수직):
  콘택 홀 주변에 수평 또는 수직 방향 막대 보조 피처
  → 금지 피치 범위에서 효과 없거나 역효과

DAF (대각선 방향 SRAF):
  콘택 홀 주변에 45도 또는 135도 방향 보조 피처
  물리적 이유:
    - 대각선 방향 회절 패턴이 수평/수직과 다른 조명 조건 활성화
    - 쿼드러폴 조명의 대각선 방향 극(pole)을 활용
    - 금지 피치 범위에서도 강건한 이미지 형성

DAF 규칙 도출:
  1. 쿼드러폴/환형 조명 모델링
  2. 피치 범위별 항공 이미지 시뮬레이션
  3. 수평/수직 SRAF vs. DAF 효과 비교
  4. 금지 피치에서 DAF 최적 크기/위치 결정
  5. 전 피치 범위 Space-Width-Orientation 테이블 작성
```

### 콘택 레이어 SRAF 규칙 체계
```
전 피치 범위 SRAF 전략:

밀집 피치 (Dense):
  SRAF 불필요 (이미 밀집 환경)

반밀집 피치 (Semi-Dense):
  표준 수평/수직 SRAF 삽입
  1 또는 2개 SRAF per gap

금지 피치 (Forbidden):
  DAF 삽입 (45° 대각선 방향)
  DAF 크기: 금지 피치 범위에서 최적화
  DAF 위치: 콘택 홀 대각선 방향 거리 테이블

고립 피치 (Isolated):
  표준 SRAF 또는 DAF
  2-3개 SRAF로 밀집 환경 모사

SRAF 규칙 테이블 구조:
  Columns: Pitch 범위
  Rows: SRAF 유형 (H/V vs. Diagonal)
  Values: SRAF 크기 (CD), 거리 (Space)
```

### 성능 결과 (고 NA OAI + att-PSM 공정)
```
기존 수평/수직 SRAF만 사용:
  금지 피치 범위: DOF 현저히 감소
  피치 의존 공정 윈도우 불균일

DAF 포함 SRAF 규칙 사용:
  금지 피치 범위: DOF 개선
  전 피치 범위 균일한 공정 윈도우 달성
  EL (Exposure Latitude): 개선
```

## OPC 툴 구현 관련성
- **SKOPC SRAF 규칙 테이블**: `skopc/modeling/sraf_generator.py` SRAF 방향 파라미터 추가 (H/V + Diagonal)
- **피치 의존 SRAF 전략**: SRAF 삽입 시 패턴 피치를 감지하여 적절한 SRAF 유형 선택
- **콘택 레이어 레시피**: YAML 레시피에 forbidden_pitch 범위와 DAF 파라미터 정의
- **금지 피치 진단**: OPC 레시피 개발 시 금지 피치 범위 자동 감지 도구

## 참고문헌
- Proc. SPIE 6349, Photomask Technology 2006
- 관련: Understanding the forbidden pitch and assist feature placement (SPIE 4562, 2002)
- 관련: Assist feature OPC for 130nm with KrF and no forbidden pitches (SPIE 4691, 2002)
- 관련: Optimal SRAF placement for process window enhancement (SPIE 6520, 2007)

## 태그
`Recipe`, `SPIE`, `SRAF`, `ForbiddenPitch`, `DiagonalAssistFeature`, `DAF`, `ContactLayer`, `OAI`, `QuadrupolePole`, `ProcessWindow`, `2006`
