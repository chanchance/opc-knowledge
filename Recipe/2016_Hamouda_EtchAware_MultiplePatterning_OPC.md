# Wafer Hotspot Prevention Using Etch-Aware OPC Correction

## 메타데이터
- **저자**: Ayman Hamouda, Dave Power, Mohamed Salama, Ao Chen
- **연도**: 2016
- **게재지**: Proc. SPIE 9781, Design-Process-Technology Co-optimization for Manufacturability X
- **DOI/URL**: https://doi.org/10.1117/12.2220778
- **인용수**: ~25

## 핵심 요약
다중 패터닝(Multiple Patterning) OPC에서 식각(etch) 성분을 포함한 식각 인식 동시 다중 패터닝 OPC(Etch-Aware Simultaneous Multiple-Patterning OPC) 방법론을 제안한다. 리소그래피와 식각 응답을 결합한 집약 모델(lumped model)을 캘리브레이션하고, OPC 적용 시 식각 후 결함(post-etch defect)과 노광 간 핫스팟(inter-exposure hotspot)을 예측 및 보정한다. 기존 다중 패터닝 OPC 대비 식각 후 웨이퍼 핫스팟을 더 효과적으로 방지한다.

## 주요 기여
1. 다중 패터닝 + 식각 인식 통합 OPC 방법론 개발
2. 리소그래피 + 식각 집약 모델(lumped model) 캘리브레이션
3. 노광 간 핫스팟(inter-exposure hotspot) 예측 및 보정
4. 식각 후 핫스팟 방지 효율 개선 실증

## Recipe/Process Flow 상세

### 다중 패터닝 OPC의 식각 문제
```
다중 패터닝 공정 (LELE 또는 SADP):
  노광 1 → 리소그래피 1 → 식각 1
  노광 2 → 리소그래피 2 → 식각 2
  → 최종 패턴: 두 노광의 결합

기존 다중 패터닝 OPC의 한계:
  - 각 노광을 리소그래피 기준으로만 OPC
  - 식각 효과 미포함 → 최종 패턴 오차 발생
  - 노광 1과 2 사이의 식각 상호작용 무시
    → 노광 간 핫스팟(inter-exposure hotspot)

식각 문제의 특성:
  - 식각 바이어스: 패턴 크기/밀도 의존
  - 마이크로 로딩: 주변 밀도에 따른 식각 불균일
  - Inter-layer 영향: 이전 노광의 식각이 다음 노광에 영향
  - 공정 변동: 식각 균일도 웨이퍼 내 변동
```

### 식각 인식 OPC 방법론
```
1단계: 리소그래피+식각 집약 모델 구축
  개념:
    집약 모델 = 리소그래피 시뮬레이션 + 식각 바이어스 모델
    CD_final = CD_litho(mask) + ΔCD_etch(CD, pitch, density)

  캘리브레이션:
    a) 리소그래피 후 CD 측정
    b) 식각 후 CD 측정 (동일 패턴)
    c) 집약 모델 파라미터 최적화:
       최소화: ||CD_model - CD_final_SEM||²
    d) 검증: 미포함 패턴에서 정확도 확인

2단계: 노광 간 상호작용 모델링
  다중 패터닝 상호작용:
    노광 1 패턴 + 노광 2 패턴 → 최종 간격(space) 예측
    inter-exposure 핫스팟 기준:
      두 패턴 사이 거리가 최소 허용 간격 미달

  상호작용 모델:
    - 두 노광의 패턴 배치 + 집약 OPC 모델
    - 최종 결합 패턴에서 bridge/pinch 예측

3단계: 식각 인식 동시 OPC
  목적함수:
    min_M Σ EPE_final(M, etch_model)
    = min_M Σ ||CD_model(M) - CD_target||²

  동시 최적화:
    두 노광 마스크를 식각 집약 모델 기반으로 동시 최적화
    → 최종 식각 후 CD가 설계 타겟에 수렴

  핫스팟 방지:
    OPC 이터레이션 중 inter-exposure 핫스팟 실시간 감지
    → 핫스팟 주변 패턴에 강화된 식각 보정 적용
```

### 집약 모델 캘리브레이션 세부
```
집약 모델 구성:
  f_litho: 컴팩트 리소그래피 모델 (Hopkins + CM1)
  f_etch: 식각 바이어스 모델 (피처 의존)
  집약: f_total = f_litho ∘ f_etch

식각 모델 파라미터:
  - etch_bias_0: 기본 식각 바이어스 (평균)
  - etch_loading_coeff: 밀도 의존 식각 로딩 계수
  - etch_range: 로딩 효과 반경

캘리브레이션 데이터:
  - 다양한 CD/pitch/밀도 테스트 패턴
  - 리소그래피 후 + 식각 후 SEM 측정
  - L2L(로트 간), W2W(웨이퍼 간) 변동 고려
```

### 성능 결과
```
기존 다중 패터닝 OPC 대비:
  식각 후 핫스팟 수: 감소
  inter-exposure 핫스팟: 더 효과적 방지
  최종 CD 정확도 (식각 후): 향상

다중 패터닝 공정 (LELE):
  노광 간 간격 정확도: 집약 모델로 개선
  브릿지/핀치 결함: 감소
```

## OPC 툴 구현 관련성
- **SKOPC 식각 인식 모드**: `skopc/modeling/` 식각 집약 모델을 OPC 목적함수에 통합
- **다중 패터닝 OPC**: `skopc/recipe/` 다중 노광 레이아웃 처리 및 노광 간 상호작용 계산
- **식각 바이어스 모듈**: `skopc/modeling/etch_model.py` (신규) 밀도/CD 의존 식각 바이어스 모델
- **핫스팟 방지**: OPC 이터레이션 중 inter-exposure 간격 실시간 모니터링

## 참고문헌
- Proc. SPIE 9781, Design-Process-Technology Co-optimization X (2016)
- 저자 소속: Mentor Graphics
- 관련: Etch proximity correction through ML-driven etch bias model (SPIE 9782, 2016)
- 관련: Using machine learning etch models in OPC and ILT correction (SPIE 11614, 2021)
- 관련: Enhanced OPC recipe coverage and early hotspot detection (SPIE 10147, 2017)

## 태그
`Recipe`, `SPIE`, `EtchAwareOPC`, `MultiplePatterning`, `LELE`, `LumpedModel`, `EtchBias`, `InterExposureHotspot`, `MentorGraphics`, `2016`
