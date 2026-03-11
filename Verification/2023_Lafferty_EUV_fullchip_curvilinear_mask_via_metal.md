# EUV Full-Chip Curvilinear Mask Options for Logic Via and Metal Patterning

## 메타데이터
- **저자**: Neal Lafferty, Sagar Saxena, Keisuke Mizuuchi, Yuansheng Ma, Xima Zhang, Pat LaCour, Alexander Tritchkov, Farah Kmiec, John Sturtevant
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950K
- **DOI/URL**: https://doi.org/10.1117/12.2647882

## 핵심 요약
3nm 노드 비아(via) 및 금속(metal) 레이어 예제에서 전체 ILT보다 빠른 런타임으로 커브형(curvilinear) 마스크를 생성하는 다양한 접근법을 비교 검토한다. 하이브리드 ILT, 고밀도 커브형 OPC, 머신러닝 기반 방법 등을 평가하고, 각 방법의 패턴 피델리티와 공정 윈도우, 런타임 트레이드오프를 분석하여 EUV 풀칩 커브형 마스크 생산을 위한 실용적 경로를 제시한다.

## 주요 기여
1. **커브형 마스크 생성 방법 비교**: 하이브리드 ILT vs 고밀도 커브형 OPC vs ML 기반 방법
2. 3nm 노드 비아 + 금속 레이어에서 각 방법의 성능 정량 비교
3. 패턴 피델리티, 공정 윈도우, 런타임의 트레이드오프 분석
4. EUV 풀칩 커브형 마스크 양산을 위한 실용적 접근법 평가
5. 전체 ILT 대비 빠른 런타임으로 커브형 마스크 이점 확보하는 방법 제시

## 검증 방법론
- **기술 노드**: 3nm 노드 비아 및 금속 레이어
- **비교 방법**: 하이브리드 ILT, 고밀도 커브형 OPC, ML 기반 커브형 OPC
- **평가 지표**: 패턴 피델리티, 공정 윈도우, 마스크 규칙 체크(MRC) 준수, 런타임
- **기준선**: 전체 ILT(Full ILT) 성능 대비
- **환경**: EUV 리소그래피, 3nm 노드 로직 레이아웃

## OPC 툴 구현 관련성
- 커브형 OPC 알고리즘 선택 시 (하이브리드 ILT / 고밀도 커브형 OPC / ML) 트레이드오프 분석의 기준 논문
- 3nm EUV 비아/금속 레이어의 커브형 마스크 OPC 검증 방법론
- 런타임 제약 하에서 커브형 마스크 이점을 최대화하는 OPC 전략 설계 참조
- `2024_Sakr_OPC_EM_fullchip_curvilinear_mask_ILT.md`의 전신 연구로 커브형 OPC 생태계 발전 맥락 이해

## 태그
`Verification`, `EUV`, `Curvilinear`, `FullChip`, `HybridILT`, `Via`, `Metal`, `3nm`, `MaskOPC`, `PatternFidelity`, `SPIE`, `DTCO`, `2023`
