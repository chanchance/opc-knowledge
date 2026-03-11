# Development of an OPC Compact Model Integrating Underlayer Effects

## 메타데이터
- **저자**: (SPIE 13425 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 1342513 (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3050104

## 핵심 요약
하층(underlayer) 효과를 통합한 OPC 컴팩트 모델 개발을 다룬다. EUV 리소그래피에서 레지스트 아래 기판 스택의 반사율 변동이 패터닝에 미치는 영향을 OPC 모델에 통합하여, 기판 토포그래피와 층 두께 변동에 강건한 OPC 보정을 구현한다.

## 주요 기여
1. **언더레이어 인식 OPC 모델**: 기판 스택 반사율 변동을 OPC 컴팩트 모델에 통합
2. **층 두께 변동 보정**: 기판 층 두께 변화에 따른 CD 변동 OPC 보정
3. **기판 토포그래피 효과**: 3D 기판 구조가 리소그래피에 미치는 영향 모델링
4. **강건한 OPC 정확도**: 다양한 기판 조건에서 일관된 OPC 보정 품질

## 알고리즘/수식
### 언더레이어 효과 OPC 모델
```
기판 스택 반사율:
  R(λ, θ) = f(n_1, k_1, d_1, n_2, k_2, d_2, ...)
  → 층 두께 d_i 변동 → 반사율 R 변동
  → CD 변동 유발

언더레이어 인식 OPC:
  CD_model = F(I_aerial, R_stack, θ_resist)
  I_aerial: 공중 이미지 강도
  R_stack: 기판 스택 반사율 (층 두께 함수)

컴팩트 모델 통합:
  기존 OPC 모델에 R_stack 항 추가:
    CD = CD_base(I_aerial) + ΔCD_underlayer(R_stack)
  ΔCD_underlayer: 기판 반사율 변동에 의한 CD 보정
```

### 모델 보정 및 검증
```
보정 데이터:
  다양한 기판 조건(층 두께 변동) 측정
  → 언더레이어 효과 분리 및 정량화

검증:
  3σ(CD_model - CD_meas) < 목표값
  다양한 기판 스택 조건에서 일관된 정확도

OPC 적용:
  기판 변동 지도(map) 기반 OPC 보정 조정
  위치별 기판 두께 → 위치별 OPC 바이어스
```

## OPC 툴 SMO 구현 관련성
- 언더레이어 OPC: SKOPC에서 기판 스택 반사율 변동을 고려한 OPC 모델 지원
- 기판 두께 맵 OPC: 웨이퍼 위치별 기판 두께 지도 기반 공간 변동 OPC 보정
- 강건 OPC: 기판 변동에 강건한 OPC 보정으로 수율 향상
- SMO 기판 인식: 기판 반사율이 소스 최적화에 미치는 영향 통합

## 태그
`OPC`, `compact_model`, `underlayer`, `substrate`, `reflectivity`, `layer_thickness`, `EUV`, `CD_variation`, `SPIE`, `2025`
