# Full Field Stitching-Aware High-NA EUV OPC/RET Flow

## 메타데이터
- **저자**: Zachary Levinson, Yunqiang Zhang, Linghui Wu, Sean Chang, Shaowen Gao, Kevin Yang, Andy Dawes, Kevin Lucas
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250H (22 April 2025)
- **DOI/URL**: https://doi.org/10.1117/12.3052709

## 핵심 요약
2nm 노드 이하 집적회로는 0.55NA 고NA EUV 스캐너의 비대칭(anamorphic) 광학계를 사용하며, 동일한 노출 영역을 달성하기 위해 2회 이상의 스티칭(stitching) 마스크 노출이 필요하다. 이 논문은 스티칭을 인식하는 OPC 및 RET 마스크 합성 단계의 새로운 확장 방법을 제안하고 검증한다.

## 주요 기여
1. **스티칭 인식 OPC 플로우**: 고NA EUV 이중 노출 스티칭 공정에 특화된 OPC 방법론
2. **SRAF 최적 배치**: 포커스 창 향상을 위한 서브 해상도 보조 피처(SRAF) 최적화
3. **격자 피처 배치 최적화**: 이중 노출 효과 감소를 위한 서브 해상도 격자 피처
4. **스티치 경계 패터닝 제어**: 공정 및 마스크 변동을 통한 스티치 경계 충분한 패터닝 제어

## 알고리즘/수식
### 스티칭 인식 OPC 플로우
```
입력: 설계 레이아웃 (2nm 이하 노드)

단계 1: 스티칭 분할
  - 레이아웃을 스티칭 경계로 2개(이상)의 마스크 필드로 분할
  - 각 마스크는 독립적으로 노출

단계 2: 스티칭 경계 인식 OPC
  - 스티칭 영역에서 두 노출의 인코히런트 이미지 합산 고려
  - 이중 노출 중복(overlap) 영역: 공동 비용 함수 최적화
  - 비용 함수 = EPE_mask1 + EPE_mask2 + EPE_stitch_zone

단계 3: RET 옵션
  - SRAF: 스티칭 영역 포함 포커스 창 향상
  - 서브 해상도 격자 피처: 이중 노출 간섭 패턴 억제
  - 소스 최적화(SMO): 스티칭 영역 특화 소스 형상

단계 4: 검증
  - 공정/마스크 변동 포함 몬테카를로 시뮬레이션
  - 스티칭 CD 오차, 오버레이 허용 오차 분석
```

### 핵심 설계 고려사항
- 비대칭 광학계(4× x, 8× y 축소): x/y 방향 OPC 비대칭 처리
- 스티칭 경계 오버레이 예산: ≤1nm 수준 정밀도 요구
- 이중 노출 상호작용: 스티칭 경계에서 이미지 강도 합산

## OPC 툴 SMO 구현 관련성
- 고NA EUV SMO는 반드시 스티칭 제약조건 통합 필요
- SMO 비용 함수: 단일 마스크 노출 → 이중 노출 합산 이미지 기반 비용 함수로 확장
- SRAF 최적화와 SMO 소스 최적화의 연동 필요
- SKOPC에서 고NA EUV 지원 시 스티칭 인식 OPC 모듈 아키텍처 참조

## 태그
`SMO`, `OPC`, `RET`, `EUV`, `high_NA`, `0.55NA`, `stitching`, `anamorphic`, `SRAF`, `2nm_node`, `DTCO`, `SPIE`
