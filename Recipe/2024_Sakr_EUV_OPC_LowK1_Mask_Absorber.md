# High Accuracy OPC Modeling for New EUV Low-K1 Mask Technology Options

## 메타데이터
- **저자**: Enas Sakr, Rob DeLancey, Wolfgang Hoppe, Zac Levinson, Robert Iwanow, Ryan Chen, Delian Yang, Kevin Lucas
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950P
- **DOI/URL**: https://doi.org/10.1117/12.2658720

## 핵심 요약
EUV 리소그래피가 volume manufacturing에 성공적으로 진입한 이후, 차세대 저-K1 EUV 마스크 기술 옵션(저반사율 흡수체, 고투과 흡수체 등)에 대해 정확한 OPC 모델링을 구현하는 방법을 연구한다. EUV 특유의 물리 현상(shadowing, flare, 마스크 토포그래피 효과, 마스크 스택 반사율, 흡수체 거동)을 OPC 모델에 통합하는 접근법을 제시한다.

## 주요 기여
1. **EUV 특화 물리 효과 모델링**: shadowing, flare, mask topography, stack reflectivity, absorber behavior를 OPC 모델에 통합
2. **저-K1 마스크 옵션 평가**: 저반사율 흡수체(low-n), 고투과 흡수체(AttPSM-like) 등 신규 마스크 스택 비교
3. **설계-리소그래피 상호작용**: 레이아웃 패턴과 EUV 공정 파라미터 간 정확한 예측 능력 향상
4. **OPC 모델 캘리브레이션 전략**: EUV 마스크 옵션별 최적 캘리브레이션 방법론

## Recipe/Flow 상세
- **대상 기술**: EUV 리소그래피 (차세대 저-K1 마스크 옵션)
- **마스크 스택 옵션**:
  - 표준 TaN 흡수체 마스크
  - 저반사율(low-n) 흡수체 마스크
  - Binary mask 대비 AttPSM 계열 신규 흡수체
- **모델링 요소**:
  - Shadowing 효과: 경사 조명 + 흡수체 두께에 의한 CD 오차
  - Flare: 산란광에 의한 패턴 밀도 의존 CD 오차
  - Mask 3D 효과: Hopkins 근사 대비 rigorous 시뮬레이션 보정항
- **캘리브레이션 데이터**: SEM 측정 + 웨이퍼 프린팅 결과
- **검증**: 다양한 레이아웃 타입(line/space, via, 2D)에 대한 예측 정확도

## OPC 툴 구현 관련성
- EUV OPC 모델에 마스크 3D 효과 보정항 추가 방법
- Shadowing 보정 bias 계산 로직
- 마스크 스택별 OPC 레시피 파라미터 분리
- `euv_mask_model.py`: reflectivity, shadowing, flare 모델 통합 구현 참고

## 태그
`EUV`, `MaskAbsorber`, `OPC`, `Modeling`, `LowK1`, `Shadowing`, `SPIE`, `2023`
