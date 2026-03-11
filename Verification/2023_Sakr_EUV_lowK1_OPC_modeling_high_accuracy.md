# High Accuracy OPC Modeling for New EUV Low-K1 Mask Technology Options

## 메타데이터
- **저자**: Enas Sakr, Rob DeLancey, Wolfgang Hoppe, Zac Levinson, Robert Iwanow, Ryan Chen, Delian Yang, Kevin Lucas
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950P (2023년 4월 28일)
- **DOI/URL**: https://doi.org/10.1117/12.2658720

## 핵심 요약
EUV 리소그래피가 양산에 도입됨에 따라 새로운 저-k1 마스크 기술 옵션에서의 고정밀 OPC 모델링이 필요하다. EUV 특유의 물리적 현상 — 음영 효과(shadowing), 플레어(flare), 마스크 토포그래피(Mask3D) 효과, 마스크 스택 반사율, 마스크 흡수체 거동 — 을 OPC 모델에 정확하게 반영하는 방법론을 제시한다.

## 주요 기여
1. **EUV 특유 물리 효과 모델링**: 음영, 플레어, Mask3D, 마스크 반사율, 흡수체 거동 등 DUV와 차별화되는 EUV 물리 현상의 포괄적 모델링 방법론 수립
2. **새로운 저-k1 마스크 기술 옵션 지원**: 차세대 저-k1 EUV 마스크 기술(새로운 흡수체 소재 등)에 맞는 OPC 모델 개발
3. **고정밀 예측 능력**: 설계-리소그래피 공정 상호작용 테스트 및 이해를 위한 정확한 예측 모델 구축
4. **체계적/확률적 변동 처리**: DUV 대비 EUV의 추가적 체계적(systematic) 및 확률적(stochastic) 변동 원인 반영

## 검증 방법론
- EUV 마스크 기술 옵션별 OPC 모델 예측값과 실제 웨이퍼 CD/EPE 비교
- 음영, Mask3D 등 개별 EUV 물리 효과 기여분 분리 평가
- 기존 DUV 기반 OPC 모델과 EUV 전용 모델의 예측 정확도 비교
- 새로운 마스크 흡수체 소재 도입 시 OPC 모델 재캘리브레이션 필요성 분석

## OPC 툴 구현 관련성
- `skopc/modeling/` 내 EUV OPC 엔진 구현 시 Mask3D, 음영, 플레어 효과를 별도 서브모델로 통합하는 아키텍처 참고
- LithoEngine에서 EUV 특유의 광학 파라미터(마스크 반사율, 13.5nm 파장 등) 지원을 위한 설계에 활용
- `recipes/example_euv.yaml` 에서 정의하는 EUV 공정 파라미터의 물리적 근거로 활용
- 저-k1 EUV 패터닝에서의 SKOPC 모델 캘리브레이션 데이터 수집 전략 수립에 참고

## 태그
`Verification`, `SPIE`, `EUV`, `Low_K1`, `OPC_Model`, `Mask3D`, `Shadowing`, `Flare`, `Accuracy`, `2023`
