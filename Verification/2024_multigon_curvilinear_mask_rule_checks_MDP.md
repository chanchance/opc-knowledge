# Multigon-Based Curvilinear Mask Rule Checks for Advanced Mask Data Preparation Applications

## 메타데이터
- **저자**: Amogh Raj, Rachit Sharma, Ranganadh 등
- **연도**: 2024
- **게재지**: Proc. SPIE 13216, Photomask Technology 2024 (2024년 11월 12일)
- **DOI/URL**: https://doi.org/10.1117/12.3034684

## 핵심 요약
곡선형(curvilinear) 마스크 및 ILT 설계의 고급 노드 적용이 확대됨에 따라 Multigon을 활용한 효율적인 곡선형 데이터 표현 및 처리 방법을 탐색한다. SEMI P39 OASIS 포맷의 확장으로 개발된 Multigon 표현을 마스크 룰 체크(MRC)에 적용하여 곡선형 마스크의 설계 무결성과 제조 가능성을 검증한다.

## 주요 기여
1. **네이티브 Multigon MRC**: 기존 폴리곤 변환 없이 Multigon 형식을 직접 처리하는 마스크 룰 체크 알고리즘 개발
2. **Multigon-to-Multigon 및 Multigon-to-PWL 체크**: 두 가지 유형의 곡선형 MRC를 포괄적으로 평가
3. **SEMI P39 OASIS 통합**: 업계 표준 포맷과의 호환성 확보
4. **제조 가능성 검증**: 곡선형 ILT 결과물의 마스크 제조 적합성을 효율적으로 검증하는 프레임워크 제공

## 검증 방법론
- Multigon 기반 MRC 결과와 기존 PWL(Piecewise Linear) 변환 후 MRC 결과 비교
- 체크 정확도 및 런타임 평가
- 다양한 곡선형 패턴 유형에 대한 검증 효과성 분석

## OPC 툴 구현 관련성
- 곡선형 OPC/ILT 결과물에 대한 MRC 단계에서 Multigon 네이티브 처리 구현 시 참고
- `skopc/modeling/` 또는 레이아웃 에디터에서 MRC 엔진을 곡선형 마스크로 확장할 때 핵심 참고
- OASIS/Multigon 포맷 I/O 지원을 GDS 기반 현재 아키텍처에 추가할 때 활용
- 마스크 데이터 준비(MDP) 플로우 설계 시 검증 단계 통합 방안 참고

## 태그
`Verification`, `SPIE`, `Curvilinear`, `Multigon`, `MRC`, `Mask_Data_Preparation`, `ILT`, `Manufacturability`, `2024`
