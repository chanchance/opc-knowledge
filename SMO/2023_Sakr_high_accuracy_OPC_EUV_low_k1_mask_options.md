# High Accuracy OPC Modeling for New EUV Low-K1 Mask Technology Options

## 메타데이터
- **저자**: Enas Sakr, Rob DeLancey, Wolfgang Hoppe, Zac Levinson, Robert Iwanow, Ryan Chen, Delian Yang, Kevin Lucas
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950P (2023)
- **DOI/URL**: https://doi.org/10.1117/12.2658720

## 핵심 요약
저-k1 EUV 리소그래피를 위한 새로운 마스크 기술 옵션에 대한 고정밀 OPC 모델링을 제시한다. EUV 특유의 물리적 거동(그림자 효과, 플레어, 마스크 토포그래피 효과, 마스크 스택 반사율, 마스크 흡수층 거동)을 OPC 모델에 통합하여 저-k1 EUV 패터닝 정확도를 향상시킨다.

## 주요 기여
1. **EUV 특화 OPC 모델링**: 그림자, 플레어, M3D, 반사율 등 EUV 고유 효과 통합
2. **마스크 기술 옵션 평가**: TaBN vs Low-n vs AttPSM 마스크 옵션별 OPC 정확도
3. **저-k1 EUV OPC**: k1 < 0.35 영역에서의 고정밀 OPC 모델 방법론
4. **생산 준비 OPC**: 실제 EUV 볼륨 생산에 적용 가능한 OPC 모델 검증

## 알고리즘/수식
### EUV 특화 OPC 모델 구성
```
EUV 고유 물리 효과:
  1. 그림자(shadowing) 효과:
     비직각 입사 (6°) → 마스크 피처 그림자
     수평/수직 피처 CD 비대칭 → H/V 바이어스

  2. 플레어(flare):
     장거리 산란광 → 균일하지 않은 배경 강도
     CD 위치 의존성 → 공간 변동 OPC 보정

  3. 마스크 3D (M3D) 효과:
     TaBN 두께 → 위상 오차 및 CD 이동
     → M3D 인식 OPC 모델 필요

  4. 마스크 스택 반사율:
     Mo/Si 다층 반사율 변동
     → 언더레이어 효과 보정

OPC 모델 통합:
  CD_model = F(I_aerial, shadow, flare, M3D, R_stack)
```

### 마스크 기술 옵션 OPC 비교
```
TaBN 표준 마스크:
  OPC 모델: 성숙한 보정 방법론
  M3D: 중간 수준

Low-n 마스크:
  OPC 모델: 다른 반사율 특성 반영 필요
  M3D: TaBN 대비 감소
  → 별도 OPC 모델 보정 필요

AttPSM (감쇠 위상 이동):
  OPC 모델: 위상 이동 효과 추가
  NILS 향상: OPC 마진 증가
  → 위상 효과 포함 OPC 모델

정확도 검증:
  3σ(CD_model - CD_meas) < 1.5nm
  다양한 마스크 기술에서 일관된 정확도
```

## OPC 툴 SMO 구현 관련성
- 마스크 타입별 OPC: SKOPC에서 TaBN/Low-n/AttPSM 마스크 타입별 OPC 모델 지원
- EUV 고유 효과 통합: 그림자, 플레어, M3D 등 EUV 특화 효과를 OPC 모델에 통합
- 저-k1 EUV OPC: 첨단 EUV 노드에서의 고정밀 OPC 모델링 방법론
- SMO 마스크 연계: 마스크 기술 선택과 SMO 최적화의 통합된 접근

## 태그
`OPC`, `EUV`, `low_k1`, `mask_technology`, `TaBN`, `low_n`, `AttPSM`, `M3D`, `flare`, `shadowing`, `high_accuracy`, `SPIE`, `2023`
