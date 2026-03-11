# Advancing the Curvilinear ILT and OPC Ecosystem for Low-K1 DUV and EUV Lithography

## 메타데이터
- **저자**: Guangming Xiao, Kevin Hooker, Yunqiang Zhang, Ji Li, Thuc Dam, Yu-Po Tang, Linghui Wu, WooJoo Sim, Kevin Lucas
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 1295413
- **DOI/URL**: https://doi.org/10.1117/12.3014637

## 핵심 요약
저-K1 DUV 및 EUV 리소그래피를 위한 curvilinear ILT 및 OPC 생태계의 발전을 종합적으로 소개한다. Synopsys 플랫폼에서 통합 곡선 기반 ILT/OPC(integrated curve-based ILT/OPC)를 개발하여, 다양한 응용 분야에서 품질과 계산 비용 요구사항을 충족하는 curvilinear 마스크 솔루션을 제공한다.

## 주요 기여
1. **통합 곡선 기반 ILT/OPC**: ILT와 OPC를 곡선 형상 기반으로 통합한 단일 플로우 개발
2. **저-K1 DUV 및 EUV 포괄**: DUV(ArF 이머젼)와 EUV 양 플랫폼에서 curvilinear 마스크 활용
3. **품질-비용 트레이드오프 최적화**: 다양한 레이어/응용 분야에 맞는 curvilinear OPC 품질 수준 선택
4. **Synopsys 플랫폼 통합**: Proteus, Sentaurus 등 Synopsys EDA 툴 생태계와 curvilinear 통합
5. **Curvilinear 마스크 생태계 성숙화**: OPC부터 MDP, 검증까지 전체 curvilinear 워크플로우 구축

## Recipe/Flow 상세
- **통합 곡선 기반 ILT/OPC 플로우**:
  1. **응용 분야 및 품질 요구사항 정의**:
     - 레이어 유형: 게이트, 메탈, 컨택, via
     - 요구 품질 수준: ILT급(최고 품질) vs. OPC+곡선 보정(중간 품질)
     - 허용 런타임 및 마스크 복잡도
  2. **Curvilinear 마스크 생성 전략 선택**:
     - 풀 ILT: 최고 공정 창, 가장 복잡한 마스크
     - 통합 곡선 OPC: OPC 기반에 곡선 세그먼트 추가
     - 곡선 SRAF: SRAF만 곡선화, 주 패턴은 직선
  3. **DUV (저-K1 ArF 이머젼) 적용**:
     - k1 < 0.3 조건에서 공정 창 향상
     - 기존 Manhattan ILT 대비 PV 밴드 개선
     - 28nm 이하 ArF 이머젼 레이어에 curvilinear 활용
  4. **EUV 적용**:
     - EUV 특화 마스크 3D 효과 포함 curvilinear 최적화
     - Stochastic 효과 최소화 curvilinear SRAF 설계
     - EUV BEOL 메탈/via 레이어 curvilinear OPC
  5. **전체 생태계 통합**:
     - MDP (마스크 데이터 준비): 곡선 형상 → MBMW 기록 형식
     - MRC 검증: 곡선 형상 전용 마스크 룰 체크
     - 웨이퍼 프린터빌리티: 시뮬레이션 기반 최종 검증
- **통합 곡선 기반 접근법 장점**:
  - 순수 ILT 대비 낮은 런타임, 순수 OPC 대비 높은 품질
  - 설계 레이어 특성에 맞는 유연한 곡선화 수준 선택
  - Synopsys 전체 EDA 스택과의 원활한 통합
- **소속 기관**: Synopsys, Inc. (미국), Synopsys Taiwan, Synopsys Korea

## OPC 툴 구현 관련성
- SKOPC curvilinear OPC 모듈에서 ILT 품질 수준 옵션 추가
- `curvilinear_opc_ilt.py`: 풀 ILT ~ OPC+곡선 보정 스펙트럼에서 선택 가능한 통합 모듈
- 레이어별 curvilinear 품질 수준 자동 선택 레시피
- DUV 저-K1 및 EUV 레이어 모두 지원하는 curvilinear 파라미터 데이터베이스

## 태그
`CurvilinearOPC`, `ILT`, `LowK1`, `DUV`, `EUV`, `MaskOptimization`, `ProcessWindow`, `Synopsys`, `Ecosystem`, `SPIE`, `2024`
