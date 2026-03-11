# From 1D-Spot to 2D-Plain: A Computer Vision-Based Comprehensive Approach for Process Window Qualification

## 메타데이터
- **저자**: Change Xu, Han Yan, Zhaoxia Dai
- **연도**: 2024 (발표: 2024년 12월)
- **게재지**: Proc. SPIE 13423, Eighth International Workshop on Advanced Patterning Solutions (IWAPS 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3052388

## 핵심 요약
공정 윈도우 검증(PWQ)의 기존 한계를 극복하는 컴퓨터 비전 기반 포괄적 PWQ 방법론을 제시한다. 전통적 방법은 임계치수(CD) 같은 스팟(1D 포인트) 특성에 의존하고 Bossung 커브를 활용하지만, LELE 같은 복잡한 멀티-스텝 공정과 복잡한 회로 레이아웃에서는 부족함을 보인다. 새로운 접근법은 전체 회로 레이아웃을 스캔하여 브릿징, 단선 등 결함 취약 영역을 2D 평면(2D-plain) 수준에서 파악한다.

## 주요 기여
1. **1D-스팟 → 2D-평면** 패러다임 전환: CD 포인트 측정에서 전체 레이아웃 스캔으로
2. 컴퓨터 비전 기반 결함 취약 영역 자동 식별 (브릿징, 단선 등)
3. LELE(Litho-Etch-Litho-Etch) 등 복잡한 멀티-스텝 공정에 적용 가능한 PWQ 방법론
4. 기존 Bossung 커브 기반 PWQ의 한계를 극복하는 포괄적 공정 윈도우 평가
5. 전체 회로 레이아웃 기반 체계적 결함 발생 영역 탐색 자동화

## 검증 방법론
- **전통적 PWQ**: CD 측정 + Bossung 커브 (1D 스팟 기반)
- **새 방법**: 컴퓨터 비전으로 전체 레이아웃 스캔 → 2D 결함 취약 영역 탐지
- **대상 결함**: 브릿징(Bridge), 단선(Break) 등 리소그래피 핫스팟
- **공정 범위**: FEM(Focus Exposure Matrix) 전 범위에서 2D 평가
- **멀티-스텝 적용**: LELE 시퀀스 포함한 복잡한 공정 가능
- **자동화**: 수작업 검사 대비 포괄적 자동 스캔

## OPC 툴 구현 관련성
- OPC 후 PWQ 수행 시 1D CD 측정만으로 부족한 경우 2D 컴퓨터 비전 기반 검증 보완 필요
- LELE 등 다중 패터닝 공정의 OPC 검증에 2D PWQ 방법 활용 가능
- 브릿징/단선 핫스팟 검출을 OPC 검증 flow에 통합하는 방법론 제시
- 풀칩 OPC 후 공정 윈도우 검증의 자동화 파이프라인 구축 참조

## 태그
`Verification`, `PWQ`, `ProcessWindow`, `ComputerVision`, `Hotspot`, `LELE`, `MultiPatterning`, `FEM`, `SPIE`, `IWAPS`, `2024`
