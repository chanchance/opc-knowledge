# Improving OPC Model Accuracy of Dry Resist for Low k1 EUV Patterning

## 메타데이터
- **저자**: Dongbo Xu, Werner Gillijns, Stewart Wu, Shruti Jambaldinni, Benjamin Kam, Anuja De Silva, Germain Fenger
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540L (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010127

## 핵심 요약
저-k1 EUV 패터닝에서 건식 레지스트(dry resist)의 OPC 모델 정확도를 향상하는 방법론을 제시한다. N5 M2 설계(32nm 피치)에서 Calibre CM1 OPC 모델을 건식 레지스트 공정에 적용하고 모델 보정 방법을 개선하여 저-k1 EUV 패터닝에서의 OPC 정확도를 향상시킨다.

## 주요 기여
1. **건식 레지스트 OPC 모델 개선**: Calibre CM1 모델의 dry resist 특화 보정 방법론
2. **N5 M2 레이어 검증**: 32nm 피치 BEOL 레이어에서 dry resist OPC 정확도 검증
3. **저-k1 EUV 특화**: k1 < 0.35 패터닝에서 dry resist 모델 정확도 향상
4. **모델 보정 방법론**: 건식 현상 특성을 반영한 새로운 보정 파라미터 도출

## 알고리즘/수식
### 건식 레지스트 OPC 모델 보정
```
저-k1 EUV 패터닝 조건:
  k1 = pitch × NA / λ = 32nm × 0.33 / 13.5nm ≈ 0.78 (하지만 CD < half pitch)
  실질 k1 = CD_target × NA / λ < 0.35 (저-k1 영역)

Calibre CM1 모델 구조:
  I_aerial = |∑_k σ_k · TCC_k ⊗ M|²  (이미지 강도)
  CD_model = F_resist(I_aerial, θ_resist)

건식 레지스트 특화 파라미터 θ_dry:
  - 건식 현상 속도 계수
  - 도즈-CD 비선형성
  - LWR/LCDU 특성

개선된 보정:
  θ_dry* = argmin Σ_CD ||CD_CM1(θ_dry) - CD_meas||²
  wet resist 보정과 별도로 dry resist 특화 최적화
```

### 모델 정확도 지표
```
N5 M2 (32nm 피치) 검증:
  피처 타입: L/S (dense), 고립 라인, 2D 피처
  평가 지표:
    RMS(CD_error) < 1nm
    3σ < 2nm

저-k1 영역 도전:
  k1 감소 → 광학 콘트라스트 저하
  → OPC 모델 민감도 증가
  → dry resist 특성으로 일부 보상
    (더 높은 도즈 감도, 낮은 LCDU)
```

## OPC 툴 SMO 구현 관련성
- Calibre CM1 호환: SKOPC의 Calibre 호환 OPC 엔진에서 dry resist 모델 지원
- 저-k1 EUV OPC: k1 < 0.35 영역의 정확한 OPC 모델 보정
- N5 M2 기준 데이터: 32nm 피치 BEOL OPC 정확도 벤치마크
- 레지스트 타입 분기: 습식/건식 레지스트별 별도 OPC 모델 보정 전략

## 태그
`OPC`, `dry_resist`, `low_k1`, `EUV`, `Calibre`, `CM1`, `N5`, `M2`, `32nm_pitch`, `model_accuracy`, `SPIE`, `2024`
