# Metal Layer OPC Repair Flow for 28nm Node and Beyond

## 메타데이터
- **저자**: (IEEE Xplore document 7463975, ISEDA/ASICON 계열 2016)
- **연도**: 2016
- **게재지**: IEEE Conference Publication (ISEDA 또는 관련 EDA 컨퍼런스)
- **DOI/URL**: https://ieeexplore.ieee.org/document/7463975/

## 핵심 요약
28nm 노드 이하에서 금속 배선 레이어는 가장 작은 피치를 가지며 OPC 적용 후 pinching, bridging, coverage 오류가 빈번하게 발생한다. 본 논문은 이러한 오류를 자동으로 분석하고 수정하는 Metal Layer OPC Repair Flow를 제안한다. 오류 위치별 자동 분석 방법론을 바탕으로 OPC repair를 체계적으로 적용한다.

## 주요 기여
1. **자동 오류 분석**: OPC 후 발생하는 pinching, bridging, coverage 오류의 자동 분류 및 위치 특정
2. **레이어별 repair 전략**: 금속 배선 레이어의 오류 유형에 최적화된 repair 방법 제시
3. **28nm 이하 적용성**: 고밀도 금속 피치에서의 OPC 신뢰성 향상
4. **런타임 효율화**: 전체 재처리 대신 오류 영역만 선택적으로 repair하여 TAT 단축

## Recipe/Flow 상세
- **Metal OPC Repair 플로우**:
  1. **OPC 실행**: 표준 model-based OPC 적용
  2. **Post-OPC 검증**: 웨이퍼 이미지 시뮬레이션 수행
  3. **오류 자동 분류**:
     - Pinching: 패턴 내부 협착 (CD < 최소 허용값)
     - Bridging: 인접 패턴 간 연결 (공간 < 최소 허용값)
     - Coverage: 타겟 대비 프린팅 부족
  4. **위치별 repair 전략 적용**:
     - 오류 심각도 및 주변 환경 분석
     - 자동화된 repair rule 선택 및 적용
  5. **재검증**: repair 후 시뮬레이션으로 수정 확인
- **대상 레이어**: Metal 배선 레이어 (M1, M2, BEOL)
- **핵심 파라미터**: 최소 CD, 최소 space, 타겟 커버리지 기준
- **자동화 수준**: 사람 개입 없이 오류 탐지 → 분류 → repair 전 과정 자동화

## OPC 툴 구현 관련성
- Post-OPC 자동 검증 및 repair 루프 구현 참고
- 오류 유형 분류기(pinching/bridging/coverage) 로직
- Metal 레이어 OPC 수렴 실패 시 대응 전략
- `opc_repair.py`: post-verify 오류 감지 → 자동 repair 적용 파이프라인

## 태그
`MetalLayer`, `OPC`, `RepairFlow`, `Pinching`, `Bridging`, `28nm`, `BEOL`, `IEEE`, `2016`
