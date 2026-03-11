# EUV Single Patterning Validation of Curvilinear Routing

## 메타데이터
- **저자**: Fergo Treska, Dongbo Xu, Yasser Sherazi, Werner Gillijns
- **연도**: 2023
- **게재지**: Proc. SPIE 12494, Optical and EUV Nanolithography XXXVI, 124940I
- **DOI/URL**: https://doi.org/10.1117/12.2654633
- **소속**: imec

## 핵심 요약
EUV 단일 패터닝 환경에서 커브형(curvilinear) 라우팅의 OPC 검증에 집중한 논문. 트랜지스터 피치 스케일링으로 인한 라우팅 혼잡 문제를 해결하기 위해 1.5D 또는 커브형 라우팅이 연구되었으며, EUV 단일 패터닝 재도입과 멀티빔 마스크 라이터(MBMW)의 진정한 커브형 마스크 구현으로 커브형 라우팅이 실용화 가능해진 상황에서 이 설계 방식의 OPC 과제를 검증한다.

## 주요 기여
1. **커브형 라우팅 EUV OPC 검증**: 커브형 배선 설계의 OPC 수행 및 검증 결과
2. EUV 단일 패터닝 + MBMW 커브형 마스크 조합에서 커브형 라우팅 실현 가능성 실증
3. 라우팅 혼잡 해소 + DRC(설계 규칙 검사) 완화를 위한 커브형 라우팅의 OPC 도전 과제 분석
4. 기존 맨해튼(직각) 라우팅 대비 커브형 라우팅의 OPC 복잡도 비교
5. 고급 노드에서 커브형 라우팅 OPC 적용을 위한 실무 가이드

## 검증 방법론
- **리소그래피**: EUV 단일 패터닝 (0.33NA EUV)
- **마스크**: MBMW(Multi-Beam Mask Writer) 커브형 마스크
- **설계**: 커브형 라우팅을 포함한 배선 레이아웃
- **OPC 과제 분석**: 커브형 형상의 OPC 분절화, 수렴성, 피델리티
- **검증 항목**: OPC 후 패턴 피델리티, 공정 윈도우, MRC 준수
- **비교**: 맨해튼 라우팅 대비 커브형 라우팅 OPC 복잡도 및 성능

## OPC 툴 구현 관련성
- 커브형 배선 설계의 OPC 처리 방법론 - 직각 OPC 대비 커브형 OPC의 차이점
- MBMW 커브형 마스크 + EUV OPC 검증 플로우 통합 방법
- 커브형 라우팅 OPC에서 분절화(fragmentation) 전략 설계 기준
- 라우팅 단계부터 OPC 검증까지 커브형 설계 플로우 전체 맥락 이해

## 태그
`Verification`, `EUV`, `Curvilinear`, `Routing`, `SinglePatterning`, `MBMW`, `OPCValidation`, `DesignRule`, `imec`, `SPIE`, `2023`
