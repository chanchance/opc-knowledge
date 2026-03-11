# Source Mask Optimization (SMO) Study for High-NA EUV Lithography to Achieve Single Patterning on Random Logic Metal

## 메타데이터
- **저자**: Soobin Hwang, Werner Gillijns, Stefan de Gendt, Ryoung-han Kim
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540X
- **DOI/URL**: https://doi.org/10.1117/12.3010869

## 핵심 요약
0.55NA High-NA EUV 리소그래피로 랜덤 로직 메탈 레이어를 단일 패터닝(single patterning)으로 구현하기 위한 SMO(Source Mask Optimization) 연구. 24nm, 22nm, 20nm 피치에서 다양한 마스크 옵션(dark-field/bright-field, Ta계/low-n 위상 변이, SRAF 유무)의 8가지 조합을 평가하여, 0.33NA EUV의 3~4중 다중 패터닝을 대체할 0.55NA 단일 패터닝 가능성을 탐색한다.

## 주요 기여
1. **0.55NA 단일 패터닝 SMO 평가**: High-NA EUV 단일 패터닝으로 0.33NA 다중 패터닝 대체 가능성 탐색
2. **8가지 마스크 옵션 비교**: dark/bright field, Ta/low-n 마스크, SRAF 유무 조합 체계적 평가
3. **20~24nm 피치 로직 메탈**: 랜덤 로직 메탈 설계에서 최소 피치별 패터닝 성능 평가
4. **SRAF + SMO 시너지**: SRAF와 SMO 결합 시 DOF 증가 효과 확인
5. **Low-n 마스크 장점**: Low-n 위상 변이 마스크의 High-NA EUV 패터닝 성능 우위 분석

## Recipe/Flow 상세
- **High-NA EUV SMO 플로우**:
  1. **설계 공간 정의**:
     - 타겟 피치: 24nm, 22nm, 20nm (수평 방향)
     - 랜덤 로직 메탈 설계 레이아웃 선정
     - 0.55NA High-NA 스캐너 파라미터 설정
  2. **마스크 옵션 8가지 설정**:
     - Dark-field vs. Bright-field
     - Ta계 이진 마스크 vs. Low-n 위상 변이 마스크(attPSM)
     - SRAF 포함 vs. SRAF 없음
     → 2×2×2 = 8가지 조합
  3. **SMO 수행**:
     - 각 마스크 옵션에 대해 광원(source) 최적화
     - 공정 창(DOF, EL) 최대화를 목적 함수로 설정
     - OPC와 연계하여 마스크 형상 동시 최적화
  4. **패터닝 성능 평가**:
     - NILS(Normalized Image Log Slope) 비교
     - DOF(Depth of Focus) 비교
     - EL(Exposure Latitude) 비교
     - 핫스팟 발생률 평가
  5. **최적 옵션 선정**:
     - 22nm 피치 이하에서 SRAF + low-n attPSM + bright-field 조합 우수
     - 단일 패터닝 실현 가능 피치 범위 도출
- **High-NA EUV 특수 고려사항**:
  - 0.55NA 아나모픽(anamorphic) 렌즈 → X/Y 방향 마스크 배율 비대칭(4×/8×)
  - 마스크 3D 효과(M3D) 더욱 심화 → Low-n 마스크로 완화
  - 조명 azimuthal 각도 변화 → SRAF 방향 최적화 필요
- **결론**: 0.55NA + SRAF + Low-n attPSM 조합으로 22nm 피치까지 단일 패터닝 가능성 확인

## OPC 툴 구현 관련성
- SKOPC SMO 모듈에서 High-NA 0.55NA 스캐너 옵션 추가
- Low-n attPSM 마스크 모델 통합 (마스크 3D 효과 포함)
- SRAF + SMO 공동 최적화 플로우 설계
- 아나모픽 High-NA 렌즈 시스템의 X/Y 비대칭 OPC 처리

## 태그
`HighNA`, `EUV`, `SMO`, `SinglePatterning`, `LogicMetal`, `SRAF`, `LowNMask`, `0.55NA`, `ProcessWindow`, `imec`, `SPIE`, `2024`
