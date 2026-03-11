# A Comparison of SALELE with Traditional Lithography and Anti-Spacer Technology

## 메타데이터
- **저자**: David Power, David Conklin, Jodi Grzeskowiak, Michael Murphy (TEL Technology Center), Xuefeng Zeng, Alex Wei, Yuyang Sun (Siemens EDA)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250O
- **DOI/URL**: https://doi.org/10.1117/12.3051131

## 핵심 요약
SALELE(Self-Aligned Litho-Etch Litho-Etch) 공정을 전통적인 리소그래피 방식과 안티-스페이서(anti-spacer) 기술 기반 방식으로 비교한다. 안티-스페이서 기술을 SALELE에 적용함으로써 초기 리소그래피 CD를 설계 피치의 1/4 수준까지 축소 가능하며, 이는 전통 리소그래피 방식의 1/2 피치 대비 현저한 개선이다. TEL-Siemens EDA 협력 연구로 SALELE 공정 플로우 최적화 방법론을 체계화한다.

## 주요 기여
1. **SALELE vs. 전통 리소그래피 비교**: 동일 설계 피치에서 SALELE와 전통 리소그래피의 CD, 공정 창, 복잡도 체계적 비교
2. **안티-스페이서 기반 SALELE**: 안티-스페이서 기술 적용으로 초기 리소그래피 CD를 설계 피치의 1/4 달성
3. **CD 축소 메커니즘 분석**: 전통(1/2 피치) vs. 안티-스페이서(1/4 피치) CD 달성 원리 및 한계 분석
4. **공정 복잡도 평가**: SALELE 방식별 공정 단계 수, 비용, 오버레이 요구사항 비교
5. **TEL-Siemens 공동 연구**: 장비 제조사(TEL)와 EDA 툴(Siemens)의 공동 공정 최적화

## Recipe/Flow 상세
- **SALELE 공정 변형 비교 플로우**:
  1. **전통 SALELE (Traditional)**:
     - 1차 리소그래피 노광: 설계 피치의 1/2 CD 패턴 형성
     - 1차 에치: 하드마스크 또는 기판 식각
     - 스페이서 형성: 1차 패턴 주위에 스페이서 증착 + 에치백
     - 2차 리소그래피 노광: cut/block 패턴 정의
     - 2차 에치: 최종 패턴 완성
     - 결과: 설계 피치의 1/4 최종 CD (스페이서 두께 기준)
  2. **안티-스페이서 기반 SALELE**:
     - 1차 리소그래피 노광: 설계 피치의 1/4 CD 패턴 형성 (안티-스페이서로 CD 축소)
     - 안티-스페이서 공정: 패턴 간격 채우기 + 코어 제거 → 원래 피처 반전(negative) 패턴
     - 1차 에치: 반전 패턴 기반 식각
     - 2차 리소그래피: cut/block 패턴 정의
     - 2차 에치: 최종 패턴 완성
     - 결과: 전통 대비 동일 리소 CD로 더 작은 최종 CD 달성
  3. **OPC 설계 차이**:
     - 전통 SALELE OPC: 1/2 피치 1차 노광 OPC (일반 리소 타겟)
     - 안티-스페이서 SALELE OPC: 1/4 피치 타겟 OPC → 더 공격적인 OPC 전략
     - 두 방식 모두 cut/block 레이어 OPC 별도 최적화
  4. **성능 비교 평가**:
     - CD 균일도(CDU): 전통 vs. 안티-스페이서 방식 비교
     - 공정 창(DOF/EL): 두 방식의 공정 창 비교
     - 오버레이 요구: 추가 에치 및 스페이서 공정의 오버레이 누적 효과
  5. **선택 가이드라인**:
     - 전통 SALELE: 검증된 공정, 더 넓은 공정 창
     - 안티-스페이서 SALELE: 더 작은 CD 달성, 공정 추가 복잡도
- **SALELE 용도**:
  - EUV 단일 패터닝 한계 이하 CD 달성
  - 다중 패터닝 없이 초미세 CD 구현
  - 선폭 균일도(LWR) 개선: 에치 기반 CD 제어
- **소속 기관**: TEL Technology Center (도쿄일렉트론 기술센터) + Siemens EDA (미국)

## OPC 툴 구현 관련성
- SKOPC SALELE 공정 지원: 1차/2차 노광 OPC 분리 설계
- 안티-스페이서 공정 효과를 OPC 모델에 통합: 스페이서 두께 → CD 변환
- SALELE cut/block 레이어 OPC 레시피 설계 기준
- TEL 안티-스페이서 장비 특성 OPC 모델 파라미터 참고

## 태그
`SALELE`, `AntiSpacer`, `MultiPatterning`, `EUV`, `OPC`, `CriticalDimension`, `ProcessIntegration`, `Etch`, `TEL`, `Siemens`, `SPIE`, `2025`
