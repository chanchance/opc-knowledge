# EUV OPC Modeling of Dry Photoresist System for Pitch 32nm BEOL

## 메타데이터
- **저자**: Jyun-Ming Chen et al.
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 129530C (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010402

## 핵심 요약
Lam의 EUV 건식 포토레지스트(dry photoresist) 시스템에 대한 OPC 모델 정확도를 32nm 피치 BEOL 배선 공정에서 평가한다. 습식 현상 대신 건식 현상 기법을 사용하여 패턴 붕괴(pattern collapse)에 강건하고 더 높은 도즈 감도를 달성하는 건식 레지스트의 OPC 모델 보정 방법을 제시한다.

## 주요 기여
1. **건식 레지스트 OPC 모델링**: 건식 현상 EUV 레지스트 시스템 전용 OPC 모델 개발
2. **32nm 피치 BEOL 적용**: N5 M2 레이어(32nm 피치)에서 건식 레지스트 OPC 성능 검증
3. **Calibre CM1 모델 정확도**: 건식 레지스트 공정에서 상용 OPC 모델 적용 가능성
4. **건식 레지스트 이점 활용**: 패턴 붕괴 방지 + 높은 처리량의 건식 레지스트 OPC 지원

## 알고리즘/수식
### 건식 레지스트 OPC 모델 특성
```
건식 레지스트(Dry Resist) 특성:
  현상 방법: 건식 현상 (습식 현상 대체)
  이점: 패턴 붕괴 없음 (표면 장력 없음)
  도즈 감도: 높음 → 처리량 향상
  두께/조성: 건식 공정으로 정밀 제어 가능

건식 레지스트 OPC 모델 차이점:
  습식 레지스트 OPC: 현상 후 프로파일 모델 포함
  건식 레지스트 OPC: 건식 현상 메커니즘 → 다른 현상 모델 필요

OPC 모델 보정:
  min_{model_params} Σ_CD ||CD_model - CD_meas||²
  건식 레지스트 특화 파라미터:
    - 건식 현상 계수
    - 도즈-CD 관계 (건식 특성)
    - LWR 특성 (습식 대비 다름)
```

### 건식 레지스트 확률론적 특성
```
건식 레지스트 확률론적 이점:
  두께/조성 정밀 제어 → 레지스트 변동 감소
  → LCDU, LWR 개선 (동일 도즈 기준)
  → 더 낮은 도즈에서 stochastic 요구사항 충족

OPC 모델에서 stochastic 반영:
  P_fail = f(NILS, dose, dry_resist_params)
```

## OPC 툴 SMO 구현 관련성
- 건식 레지스트 OPC 모델: SKOPC EUV OPC 모듈에서 건식 레지스트 타입 지원
- BEOL 배선 OPC: 32nm 피치 BEOL 레이어 OPC 성능 기준 데이터
- 레지스트 타입별 모델 분기: 습식/건식/금속산화물 레지스트별 OPC 모델 선택
- SMO 레지스트 연계: 건식 레지스트 특성에 맞는 SMO 도즈 최적화

## 태그
`OPC`, `EUV`, `dry_resist`, `BEOL`, `32nm_pitch`, `Lam`, `N5`, `metal2`, `Calibre`, `model_calibration`, `SPIE`, `2024`
