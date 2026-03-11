# Pushing the Boundaries of Random Logic Metal Patterning with Low-N EUV Single Exposure

## 메타데이터
- **저자**: Syamashree Roy, Arame Thiam, Kaushik Sah, et al.
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 129530X
- **DOI/URL**: https://doi.org/10.1117/12.3010868

## 핵심 요약
2nm 로직 기술 노드를 향한 랜덤 로직 메탈 패터닝의 한계를 low-n EUV 단일 노광으로 확장하는 연구. Low-n 마스크가 Ta계 마스크 대비 LCDU 개선, 마스크 3D 효과 감소, 광학 대비 향상을 제공함을 실증하고, 32nm 피치 PnR(Place and Route) 구조에서 LCDU 5.5nm, CGDU 5.5nm를 달성하는 우수한 패터닝 성능을 보인다.

## 주요 기여
1. **Low-n 마스크 랜덤 로직 메탈 한계 확장**: 32nm 피치에서 low-n EUV 단일 노광의 랜덤 로직 메탈 패터닝 한계 실증
2. **LCDU 5.5nm 달성**: 32nm 피치 PnR 구조에서 LCDU 및 CGDU 5.5nm 달성
3. **Low-n vs. Ta계 마스크 정량 비교**: LCDU, M3D 효과, 광학 대비 등 정량 비교
4. **2nm 노드 확장성**: BEOL 인터커넥트 피치 스케일링을 위한 EUV 단일 노광 경로 제시
5. **OPC + Low-n 마스크 시너지**: OPC와 low-n 마스크 결합 패터닝 전략

## Recipe/Flow 상세
- **Low-n EUV 랜덤 로직 메탈 패터닝 플로우**:
  1. **Low-n 마스크 선택**:
     - Low-n attPSM: 굴절률 n이 낮은 흡수체 (n < 0.9)
     - 마스크 3D 효과(M3D) 감소: 낮은 n으로 shadowing 완화
     - 광학 대비 향상: 위상 변이 효과로 NILS 증가
  2. **PnR 레이아웃 테스트**:
     - Place and Route로 생성된 랜덤 로직 메탈 레이아웃
     - 최소 피치 32nm 타겟
     - 다양한 방향(수평/수직/대각선) 및 T자/L자 형태 포함
  3. **SMO + OPC**:
     - Low-n 마스크에 최적화된 조명 조건 SMO
     - EUV OPC 모델 캘리브레이션 (마스크 3D 효과 포함)
     - LCDU 최소화를 위한 OPC 전략
  4. **패터닝 성능 측정**:
     - LCDU(Local CD Uniformity): 5.5nm 달성
     - CGDU(Contact Grid CD Uniformity): 5.5nm 달성
     - 공정 창 측정 및 핫스팟 분석
  5. **Ta계 vs. Low-n 비교**:
     - 동일 조건에서 두 마스크 성능 정량 비교
     - Low-n 마스크의 M3D 감소 효과 측정
     - 실제 웨이퍼 결과로 시뮬레이션 예측 검증
- **Low-n 마스크 EUV 물리 원리**:
  - 굴절률 n이 낮을수록 마스크 흡수체 내 광 전파 경로 변화 감소
  - M3D shadowing 오차 감소 → across-slit CD 변동 감소
  - 위상 변이로 이미지 대비 향상 → NILS 증가 → stochastic 개선
- **목표 노드**: 2nm 로직 BEOL, 32nm 피치 메탈

## OPC 툴 구현 관련성
- SKOPC EUV 메탈 레이어 OPC에서 low-n attPSM 마스크 모델 지원
- Low-n 마스크 M3D 감소 효과를 OPC 모델에 반영
- LCDU 최적화 OPC 전략: stochastic-aware 보정과 low-n 마스크 시너지
- 2nm 노드 BEOL OPC 레시피 설계 기준 (32nm 피치)

## 태그
`EUV`, `LowNMask`, `LogicMetal`, `SinglePatterning`, `OPC`, `LCDU`, `M3D`, `2nmNode`, `BEOL`, `RandomLogic`, `SPIE`, `2024`
