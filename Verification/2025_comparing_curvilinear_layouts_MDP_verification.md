# Comparing Curvilinear Layouts for the Verification of Mask Data Preparation

## 메타데이터
- **저자**: Masakazu Hamaji, Taigo Fujii, Ryunosuke Miyake, Rie Funoki, Aki Shigeta, Tomokazu Hayashi, Shuichiro Ohara
- **연도**: 2025
- **게재지**: Proc. SPIE 13655, Photomask Japan 2025: XXXI Symposium on Photomask and Next-Generation Lithography Mask Technology (2025년 7월 21일, 요코하마)
- **DOI/URL**: https://doi.org/10.1117/12.3070335

## 핵심 요약
곡선형(curvilinear) 레이아웃의 마스크 데이터 준비(MDP: Mask Data Preparation) 검증을 위해 서로 다른 곡선형 레이아웃 표현 방식을 비교 분석한다. 곡선형 마스크가 고급 노드에서 표준화됨에 따라 MDP 검증 단계에서의 레이아웃 충실도 평가 방법론을 체계화한다.

## 주요 기여
1. **곡선형 레이아웃 표현 비교**: 베지어 곡선, Multigon, PWL(Piecewise Linear) 등 다양한 표현 방식의 MDP 검증 관점에서 차이점 분석
2. **MDP 검증 방법론 체계화**: 곡선형 레이아웃의 MDP 검증을 위한 포괄적 비교 프레임워크 제시
3. **레이아웃 충실도 평가**: 원본 OPC/ILT 결과물과 MDP 처리 후 레이아웃의 차이를 정량적으로 측정
4. **실용적 검증 기준 제시**: 다양한 표현 방식에서 허용 가능한 MDP 오차 기준 설정

## 검증 방법론
- 서로 다른 곡선형 레이아웃 표현 형식 간 기하학적 차이 측정
- MDP 전후 레이아웃의 EPE 및 윤곽선 편차 분석
- 마스크 제조 공정 시뮬레이션을 통한 최종 패턴 충실도 비교

## OPC 툴 구현 관련성
- 곡선형 OPC/ILT 출력물의 MDP 검증 플로우 설계 시 직접 참고
- 레이아웃 에디터 모듈에서 곡선형 마스크 표현 형식 선택 기준으로 활용
- `skopc/modeling/` 내 테이프아웃 검증 단계에 곡선형 레이아웃 비교 기능 추가 시 참고
- OASIS/Multigon/PWL 형식 간 변환 충실도 테스트 방법론으로 활용

## 태그
`Verification`, `SPIE`, `Curvilinear`, `Mask_Data_Preparation`, `MDP`, `Layout_Comparison`, `ILT`, `OPC`, `2025`
