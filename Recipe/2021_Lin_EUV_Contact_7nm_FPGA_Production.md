# Optimization of the EUV Contact Layer Process for 7nm FPGA Production

## 메타데이터
- **저자**: Qi Lin, Toshiyuki Hisamura, Nui Chong, Jonathan Chang
- **연도**: 2021
- **게재지**: Proc. SPIE 11609, Extreme Ultraviolet (EUV) Lithography XII, 116090V
- **DOI/URL**: https://doi.org/10.1117/12.2584288

## 핵심 요약
7nm FPGA 양산에서 EUV 컨택 레이어 공정을 최적화하는 방법을 제시한다. EUV 리소그래피를 7nm 노드 FPGA 제품에 삽입하여 다중 패터닝 ArF의 공정 복잡성을 단순화하고 제품 성능(낮은 접촉 저항)을 향상시킨다. EUV 컨택 결함률, 변동성, 공정 창 최적화 및 양산 관점의 통합 방법을 다룬다.

## 주요 기여
1. **7nm FPGA EUV 컨택 양산 삽입**: FPGA 7nm 노드에 EUV 컨택 레이어 최초 양산 적용 사례
2. **EPE 감소로 성능 향상**: EUV의 낮은 EPE로 컨택 저항 감소 및 트랜지스터 성능 향상
3. **EUV 컨택 결함률 해결**: 양산 환경에서 EUV stochastic 결함 관리 방법 제시
4. **공정 창 최적화**: FPGA CRAM 임베디드 메모리의 EUV 컨택 공정 창 최적화
5. **다중 패터닝 대체 검증**: 복잡한 ArF 다중 패터닝을 EUV 단일 노광으로 대체 실증

## Recipe/Flow 상세
- **7nm FPGA EUV 컨택 최적화 플로우**:
  1. **EUV 컨택 삽입 목표 설정**:
     - 대상 레이어: FPGA 내 CRAM 임베디드 메모리 컨택
     - 목표: ArF 다중 패터닝 대체, EPE 감소, 접촉 저항 향상
     - 성능 지표: CD 균일도, EPE, stochastic 결함률, 수율
  2. **OPC 모델 캘리브레이션**:
     - EUV 컨택 레이어 특화 OPC 모델 구축
     - 7nm 노드 컨택 피치에서 EUV shadowing, flare 모델 포함
     - Stochastic 거동 반영 OPC 전략 수립
  3. **공정 창 최적화**:
     - Focus-Dose 매트릭스 실험
     - 컨택 CD 균일도 및 오버레이 최적화
     - Stochastic 결함 (브리징, 누락 컨택) 최소화 조건 탐색
  4. **Stochastic 결함 관리**:
     - EUV 포톤 통계로 인한 컨택 결함률 측정
     - 결함 예측 모델 및 OPC 보정 전략 수립
     - 도즈 및 레지스트 최적화로 결함률 목표 달성
  5. **양산 검증**:
     - 웨이퍼 레벨 수율 및 제품 성능 측정
     - ArF 다중 패터닝 대비 수율/성능 개선 확인
- **FPGA 컨택 특수 고려사항**:
  - CRAM 셀: 매우 규칙적인 컨택 어레이
  - 메모리-로직 혼재: 다양한 컨택 크기 및 밀도
  - EUV stochastic 결함: 소형 컨택에서 yield killer
- **업계 의의**: EUV 컨택 레이어의 FPGA 양산 최초 사례 중 하나

## OPC 툴 구현 관련성
- SKOPC EUV 컨택 레이어 OPC 모델 캘리브레이션 가이드라인
- Stochastic 결함 최소화를 위한 OPC 전략 (도즈 마진 최대화)
- FPGA/메모리 컨택 어레이 OPC에서 균일 근접 효과 보정
- 7nm 노드 EUV 컨택 공정 창 예측 모델 구현

## 태그
`EUV`, `Contact`, `7nm`, `FPGA`, `Production`, `OPC`, `StochasticDefect`, `ProcessWindow`, `Manufacturing`, `SPIE`, `2021`
