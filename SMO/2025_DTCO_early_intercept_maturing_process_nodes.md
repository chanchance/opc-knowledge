# Design Technology Co-Optimization for Early Intercept on Maturing Process Nodes

## 메타데이터
- **저자**: Raj Varada et al.
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250S (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051953

## 핵심 요약
성숙해가는 공정 노드에서 조기 개입(early intercept)을 위한 설계-기술 공동 최적화(DTCO) 방법론을 제시한다. 성숙한 노드에서 OPC/RET 기법의 지속적 개선과 설계 규칙 최적화를 통해 추가 기술 투자 없이 수율과 성능을 향상시키는 DTCO 전략을 다룬다.

## 주요 기여
1. **성숙 노드 DTCO 전략**: 기존 공정 노드에서 추가 가치를 창출하는 DTCO 방법론
2. **조기 개입 방법론**: 공정 성숙 단계에서의 수율/성능 개선 조기 식별
3. **OPC/RET 지속 최적화**: 성숙 노드에서도 OPC/RET 개선으로 패터닝 성능 향상
4. **설계 규칙 정제**: DTCO를 통한 성숙 노드 설계 규칙 최적화

## 알고리즘/수식
### 성숙 노드 DTCO 프레임워크
```
성숙 노드 DTCO 목표:
  기술 전환 없이 성능/수율 향상
  OPC/SMO 개선 → 추가 설계 자유도
  설계 규칙 완화 → 라우팅 밀도 향상

조기 개입 방법론:
  1. 패터닝 핫스팟 분석:
     전체 칩에서 수율 제한 패턴 식별
  2. OPC/RET 최적화:
     핫스팟 패턴에 타겟화된 OPC 개선
  3. 설계 규칙 업데이트:
     OPC 개선 결과로 제약 완화
  4. 수율 영향 평가:
     DTCO 전후 수율 개선 측정

비용-이익 분석:
  DTCO 투자 비용 vs 수율 향상 이익
  조기 개입 타이밍 최적화
```

### OPC-설계 규칙 공동 최적화
```
설계 규칙 완화 가능성:
  기존 OPC 한계 → 보수적 설계 규칙
  OPC 개선 → 더 공격적인 규칙 가능

DTCO 루프:
  OPC 성능 평가 → 설계 규칙 제안
  설계 규칙 적용 → 레이아웃 밀도 향상
  → 수율 재평가 → 최적점 탐색

성숙 노드 특유의 이점:
  풍부한 공정 데이터 → 정확한 모델
  OPC 미세 조정 기회 풍부
  → DTCO 효과 극대화 가능
```

## OPC 툴 SMO 구현 관련성
- 성숙 노드 OPC 최적화: SKOPC에서 기존 노드의 OPC 지속 개선 지원
- DTCO 설계 규칙 인터페이스: OPC 성능을 설계 규칙 완화에 연계하는 DTCO 플로우
- 조기 핫스팟 탐지: 전체 칩 OPC 결과에서 수율 제한 패턴 자동 식별
- 수율 기반 OPC: 수율 개선을 목표로 하는 OPC 최적화 전략

## 태그
`DTCO`, `OPC`, `SMO`, `design_rules`, `yield`, `early_intercept`, `mature_node`, `hotspot`, `patterning`, `SPIE`, `2025`
