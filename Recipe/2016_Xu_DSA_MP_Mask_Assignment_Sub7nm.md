# Mask Assignment and DSA Grouping for DSA-MP Hybrid Lithography for Sub-7nm Contact/Via Holes

## 메타데이터
- **저자**: (IEEE Xplore document 7579198, 2016)
- **연도**: 2016
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD)
- **DOI/URL**: https://ieeexplore.ieee.org/document/7579198/

## 핵심 요약
DSA(Directed Self-Assembly)는 sub-7nm 기술 노드에서 매우 유망한 패터닝 후보이며, 가이딩 템플릿 인쇄를 위해 Multiple Patterning(MP)이 필요하다. 본 논문은 두 가지 DSA-MP 하이브리드 공정 방식에 대해 DSA 그루핑과 마스크 할당을 동시에 최적으로 수행하는 ILP(Integer Linear Program) 및 확장 가능한 휴리스틱 알고리즘을 제안한다.

## 주요 기여
1. **DSA-MP 공동 최적화**: DSA 그루핑과 마스크 할당을 동시에 고려하는 최초의 통합 최적화 프레임워크
2. **ILP 최적해**: Integer Linear Program으로 최적 해 보장
3. **확장 가능한 휴리스틱**: ILP 대비 4×–213× 빠른 속도로 4%–29% 위반 증가만으로 근사 최적해 달성
4. **두 가지 DSA-MP 방식 지원**: 서로 다른 hybrid 공정 흐름에 모두 적용 가능
5. **Sub-7nm Contact/Via 대상**: 극소 contact/via hole 패터닝에 특화

## Recipe/Flow 상세
- **DSA-MP 하이브리드 리소그래피 플로우**:
  1. **Contact/Via 분석**: 레이아웃의 모든 contact/via hole 추출
  2. **DSA 가능성 평가**: 각 contact 쌍에 대해 DSA self-assembly 가능 여부 판단
     - 피치, 거리, 방향 제약 확인
  3. **DSA 그루핑**: DSA로 한 번에 패터닝 가능한 contact 그룹 결정
  4. **MP 마스크 할당**: 각 그룹의 가이딩 템플릿을 복수 마스크에 배정
     - 충돌(conflict) 없는 마스크 분리 보장
  5. **ILP 최적화** (소규모) 또는 **휴리스틱** (대규모):
     - 목적함수: 마스크 수 최소화 + DSA 그루핑 최대화
     - 제약: 마스크 간 최소 피치, DSA 가능 거리
  6. **OPC 적용**: 각 마스크의 가이딩 템플릿에 OPC 보정
- **지원 DSA-MP 방식**:
  - 방식 1: Chemoepitaxy 기반 (화학적 패턴)
  - 방식 2: Graphoepitaxy 기반 (형상 패턴)
- **평가 지표**: 마스크 수, 위반(violation) 수, 런타임

## OPC 툴 구현 관련성
- DSA 기반 contact/via 레이어 OPC의 가이딩 템플릿 보정 전략
- Contact/via hole을 DSA 그룹으로 분류하는 전처리 로직
- MP 마스크 할당 결과를 각 마스크별 OPC 레시피에 연결
- `dsa_layout_decompose.py`: DSA 그루핑 + 마스크 할당 통합 모듈

## 태그
`DSA`, `MultiPatterning`, `Contact`, `Via`, `MaskAssignment`, `Sub7nm`, `ILP`, `IEEE`, `2016`
