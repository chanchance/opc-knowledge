# MOSAIC: Mask Optimizing Solution With Process Window Aware Inverse Correction

## 메타데이터
- **저자**: Jhih-Rong Gao, Xiaoqing Xu, Bei Yu, David Z. Pan
- **연도**: 2014
- **게재지**: ACM/IEEE Design Automation Conference (DAC) 2014
- **DOI/URL**: https://ieeexplore.ieee.org/document/6881379/ | https://dl.acm.org/doi/10.1145/2593069.2593163

## 핵심 요약
기존 규칙 기반 및 모델 기반 OPC는 명목 공정 파라미터만을 고려하여 공정 변동에 취약하다. MOSAIC는 역리소그래피 기법(ILT)을 기반으로 공정 변동(dosage, focus)을 명시적으로 고려하는 최초의 진정한 공정-변동 인식 OPC(PV-OPC) 프레임워크를 제안한다. 분석적 모델 덕분에 기존 OPC 대비 2~3배의 런타임 증가만으로 훨씬 견고한 포스트-OPC 결과를 달성한다.

## 주요 기여
1. **최초의 PV-OPC 프레임워크**: 공정 창(process window) 내 dose 및 focus 변동을 OPC 최적화 목적 함수에 명시적으로 통합
2. **ILT 기반 공정 창 최적화**: 역리소그래피 방법을 공정 창 최대화 관점에서 재정식화
3. **효율적 분석적 모델 활용**: 수치적 방법 대신 분석적 모델을 사용하여 PV-OPC를 실용적 런타임(기존 대비 2-3배)으로 구현
4. **견고한 포스트-OPC 결과**: 단순 명목 조건 OPC 대비 포커스·노광량 변동에서의 패턴 성능 대폭 향상

## 검증 방법론
- 명목 조건 및 포커스/노광량 코너 조건에서 포스트-OPC 패턴 성능(EPE, CD) 비교
- 기존 모델 기반 OPC 및 표준 ILT 대비 공정 창 크기(DOF × EL) 비교
- 런타임 분석: 기존 OPC 대비 2~3배 이내 증가 확인

## OPC 툴 구현 관련성
- `skopc/pwo/` NSGA-II 기반 PWO 모듈의 이론적 선행 연구로, 공정 창 인식 OPC 설계 패턴 제공
- `skopc/modeling/` 내 Model OPC 모듈에 공정 변동 고려 옵션 추가 시 핵심 참고
- OPC 목적 함수를 공정 창 최대화 방향으로 확장하는 알고리즘 설계에 활용
- SMO 모듈과 OPC의 공동 최적화(co-optimization) 프레임워크 설계 시 이론적 기반으로 활용

## 태그
`Verification`, `IEEE`, `DAC`, `OPC`, `ILT`, `Process_Window`, `PV_OPC`, `Dose`, `Focus`, `2014`
