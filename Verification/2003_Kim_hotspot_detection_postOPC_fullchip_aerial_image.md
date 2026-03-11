# Hotspot Detection on Post-OPC Layout Using Full-Chip Simulation-Based Verification Tool: A Case Study with Aerial Image Simulation

## 메타데이터
- **저자**: Juhwan Kim, Minghui Fan
- **연도**: 2003
- **게재지**: Proc. SPIE 5256, 23rd Annual BACUS Symposium on Photomask Technology
- **DOI/URL**: https://doi.org/10.1117/12.517364

## 핵심 요약
OPC 후 레이아웃에서 마스크 테이프아웃(tape-out) 이전에 hotspot을 포착하기 위한 시뮬레이션 기반 풀칩 검증 방법론을 제안한 초기 핵심 논문. 100nm 노드 공정에서 캘리브레이션된 공정 모델과 다중 포커스/임계값 조건을 적용한 여러 광학 모델을 조합하여 post-OPC 레이아웃의 bridging/pinching hotspot을 체계적으로 포착하는 SiVL 기반 완전한 시뮬레이션-분석 플로우를 실증하였다.

## 주요 기여
1. **풀칩 시뮬레이션 기반 OPC 검증 플로우**: SiVL 시뮬레이터를 이용한 완전한 post-OPC 풀칩 검증 및 hotspot 분석 플로우 구성
2. **다중 광학 모델 활용**: 다양한 포커스/임계값 조건에서의 다중 광학 모델을 적용하여 공정 변동 범위 내 hotspot 포착
3. **Bridging/Pinching hotspot 분류**: 공정 조건 이탈 시 발생하는 bridging(연결) 및 pinching(단락) 두 가지 hotspot 유형 식별
4. **마스크 테이프아웃 전 검증**: 마스크 제작 전 OPC 검증으로 리워크 비용 절감 및 개발 시간 단축
5. **100nm 노드 실증**: 당시 최첨단인 100nm 기술 노드에서 방법론의 실용성 검증

## 검증 방법론
- 100nm 노드 공정 캘리브레이션된 컴팩트 공정 모델 구축
- 포커스 변동(±δf), 도즈 변동(±δd) 공정 윈도우 코너 조건에서 시뮬레이션
- SiVL 기반 풀칩 시뮬레이션으로 bridging/pinching hotspot 후보 식별
- 실제 웨이퍼 SEM 검사로 시뮬레이션 기반 hotspot 예측 검증

## OPC 툴 구현 관련성
- SKOPC의 post-OPC 시뮬레이션 기반 검증(LRC/ORC) 모듈의 개념적 기초가 되는 선구적 논문
- `2005_Hung_post_OPC_full_chip_pattern_simulation.md`(기수집)과 함께 풀칩 OPC 검증의 역사적 기반 구성
- SKOPC 검증 모듈에서 다중 공정 윈도우 조건 시뮬레이션 기능 구현 시 원조 방법론으로 참조
- Bridging/pinching 두 가지 hotspot 유형 분류는 SKOPC 검증 리포트의 실패 모드 분류 기준으로 활용

## 태그
`Verification`, `SPIE`, `Hotspot`, `Post-OPC`, `Full Chip`, `Aerial Image`, `Simulation`, `Bridging`, `Pinching`, `100nm`, `BACUS`
