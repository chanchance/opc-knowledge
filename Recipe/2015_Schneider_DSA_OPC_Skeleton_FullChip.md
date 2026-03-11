# Skeleton-Based OPC Application for DSA Full Chip Mask Correction

## 메타데이터
- **저자**: L. Schneider, V. Farys, E. Serret, C. Fenouillet-Beranger
- **연도**: 2015
- **게재지**: Proc. SPIE 9661, 31st European Mask and Lithography Conference (EMLC 2015), 96610M
- **DOI/URL**: https://doi.org/10.1117/12.2195171

## 핵심 요약
DSA(Directed Self-Assembly) 리소그래피에서 가이딩 템플릿의 full-chip 마스크 보정을 위해 스켈레톤(skeleton) 기반 OPC 접근법을 제안한다. DSA 공정의 특수성을 반영한 OPC 알고리즘으로, 블록 공중합체의 자기 조립 특성과 리소그래피 근접 효과를 동시에 고려한 보정 플로우를 제시한다.

## 주요 기여
1. **스켈레톤 기반 OPC**: DSA 가이딩 템플릿의 형상 중심축(skeleton)을 이용한 보정 접근법
2. **Full-chip 적용**: DSA 마스크 보정의 full-chip 규모 실용화
3. **DSA 특화 모델**: 블록 공중합체 자기 조립 거동을 OPC 모델에 통합
4. **OPC-DSA 인터페이스**: 리소그래피 OPC 툴과 DSA 공정 시뮬레이터의 연동 방법
5. **EMLC 발표**: 유럽 마스크 및 리소그래피 컨퍼런스 발표로 유럽 반도체 관점 제공

## Recipe/Flow 상세
- **DSA Full-Chip 마스크 보정 플로우**:
  1. **DSA 레이아웃 분석**:
     - 블록 공중합체(BCP) 도메인 패턴 목표 정의
     - 가이딩 템플릿 형상 추출 (graphoepitaxy 또는 chemoepitaxy)
  2. **스켈레톤 추출**:
     - 템플릿 패턴의 medial axis transform(MAT) 계산
     - 스켈레톤 기반 fragment 배치 → 균등하고 물리적으로 의미 있는 보정점
  3. **OPC 모델 적용**:
     - 표준 리소그래피 OPC 모델 (템플릿 프린팅용)
     - DSA 자기 조립 시뮬레이션으로 최종 BCP 도메인 위치 예측
  4. **통합 목적함수**:
     - 리소 타겟 EPE 최소화
     - DSA 도메인 위치 오차 최소화
  5. **Full-chip 처리**: 타일 병렬 처리로 full-chip 런타임 달성
- **DSA 공정 특수 고려사항**:
  - BCP 자기 조립: 템플릿 CD/피치 오차 → 도메인 배치 오차 증폭
  - Graphoepitaxy: 함몰부 형상 정확도가 도메인 정렬 좌우
  - Chemoepitaxy: 화학 패턴 CD/위치 정확도가 핵심
- **평가 지표**: 템플릿 CD 오차, BCP 도메인 위치 오차, 결함률

## OPC 툴 구현 관련성
- DSA 가이딩 템플릿 OPC 레시피 설계 참고
- 스켈레톤 기반 fragment 배치 → curvilinear OPC에도 응용 가능
- `dsa_template_opc.py`: 스켈레톤 추출 → OPC + DSA 통합 목적함수 최적화
- DSA 도메인 예측 모델과 OPC 모델의 연동 인터페이스

## 태그
`DSA`, `OPC`, `Skeleton`, `FullChip`, `GuidingTemplate`, `BlockCopolymer`, `SPIE`, `2015`
