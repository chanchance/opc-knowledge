# Model-Based Optical Proximity Correction for Immersion Lithography-Based Flat Optics Platform

## 메타데이터
- **저자**: Narak Choi, Keng Heng Lai, Arvind Sundaram, Navab Singh, Yuan Hsing Fu, Lennon Y. T. Lee
- **연도**: 2023
- **게재지**: Proc. SPIE 12432, Optical Microlithography XXXVI (또는 관련 SPIE 볼륨), 1243205
- **DOI/URL**: https://doi.org/10.1117/12.2647686

## 핵심 요약
메타서페이스(metasurface) 기반 평면 광학 소자(flat optics) 제조에 성숙된 OPC 기술을 도입한 연구. 서브파장 나노필러(nanopillar) 어레이로 구성되는 메타서페이스는 가시광선 대응을 위해 ArF 이머젼 리소그래피의 공정 한계에 근접한 CD 수준이 필요하며, 광학 근접 효과에 의한 CD 오차가 평면 광학 소자의 효율 저하를 유발한다. 이를 보정하기 위한 모델 기반 OPC 적용 방법론을 제시한다.

## 주요 기여
1. **메타서페이스 OPC 최초 적용**: 반도체 OPC 기술을 평면 광학 소자 제조에 도입
2. **서브파장 나노필러 보정**: 가시광선 메타서페이스용 나노필러의 광학 근접 효과 모델링
3. **ArF 이머젼 리소그래피 한계 대응**: 공정 한계 근처 CD에서의 OPC 정확도 확보
4. **효율 저하 방지**: OPC로 CD 오차 제거 → 메타서페이스 광학 효율 향상
5. **비반도체 OPC 적용 사례**: 포토닉스/광학 소자 제조에 반도체 OPC 기법 전이

## Recipe/Flow 상세
- **메타서페이스 OPC 플로우**:
  1. **메타서페이스 레이아웃 분석**:
     - 나노필러 어레이 패턴 정의 (크기, 간격, 형상)
     - 광학 효율 목표에 따른 나노필러 CD 타겟
  2. **OPC 모델 캘리브레이션**:
     - ArF 이머젼 리소그래피 공정 파라미터
     - 나노필러 패턴의 근접 효과 측정 및 모델 피팅
     - CD 범위: 가시광선 파장의 절반 수준 (100~200nm)
  3. **Model-based OPC 적용**:
     - 나노필러 위치/크기 보정
     - 고밀도 어레이에서의 패턴 간 상호 영향 보정
     - 코너 라운딩 및 형상 변형 보정
  4. **광학 성능 검증**:
     - OPC 전후 웨이퍼 프린팅 결과 비교
     - 메타서페이스 광학 효율 측정
- **메타서페이스 특수 고려사항**:
  - 매우 규칙적인 어레이 패턴 → 패턴 밀도 균일
  - 다양한 나노필러 크기가 한 필드 내 혼재 → 크기별 서로 다른 OPC 보정량
  - 광학 효율이 CD에 민감하게 의존 → 엄격한 CD 목표
- **적용 플랫폼**: A*STAR (싱가포르 과학기술연구청) 연구

## OPC 툴 구현 관련성
- SKOPC의 포토닉스/광학 소자 레이어 OPC 확장 가능성
- 나노필러 어레이의 규칙적 패턴을 활용한 OPC 최적화
- `photonics_opc.py`: 메타서페이스 나노필러 OPC 레시피 구현
- 반도체 OPC 기법을 비반도체 광학 소자에 적용하는 방법론

## 태그
`FlatOptics`, `Metasurface`, `OPC`, `Nanopillar`, `ImmersionLithography`, `Photonics`, `ModelBased`, `SPIE`, `2023`
