# Verification Methods for Curvilinear and Real-Curve Geometries

## 메타데이터
- **저자**: Kokoro Kato
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950J
- **DOI/URL**: https://doi.org/10.1117/12.2661609

## 핵심 요약
ILT OPC 결과물인 커비리니어(curvilinear) 마스크 레이아웃의 검증 방법론을 체계적으로 논의한 논문. 기존 맨해튼(Manhattan) 레이아웃 대비 복잡성·데이터 용량 증가 문제와 검증 방법 부재 문제를 해결하기 위해, MULTIGON 레코드 기반 실곡선(real-curve, parametric curve) 표현 방식을 도입하고 해당 데이터에 적합한 검증 방법론을 제안하였다.

## 주요 기여
1. **커비리니어 검증의 핵심 과제 정의**: 형상 복잡성, 대용량 데이터, 미확립된 검증 방법의 세 가지 도전을 체계적으로 정리
2. **실곡선(Real-Curve) 데이터 표현**: 매개변수 곡선(parametric curve)을 사용하여 마스크 데이터 용량을 획기적으로 줄이는 MULTIGON 레코드 정의
3. **MULTIGON 레코드 특성 분석**: 신규 마스크 데이터 포맷의 특성 설명과 마스크 산업에서의 적용 로드맵 제시
4. **커비리니어 전용 기초·실용 검증 방법**: 복잡한 곡선 형상에 적합한 MRC(Mask Rule Check) 및 형상 검증 알고리즘 제안
5. **마스크 산업 표준화 방향 제시**: 커비리니어 및 실곡선 데이터 처리를 위한 업계 협력 필요성 및 전망 논의

## 검증 방법론
- 커비리니어 레이아웃에 대한 기하학적 검증(MRC) 알고리즘 비교
- MULTIGON 레코드 기반 실곡선 데이터와 폴리곤 근사 데이터 간의 검증 결과 비교
- 데이터 용량 감소율 정량 분석 (실곡선 vs. 다각형 분절 표현)
- 커비리니어 형상별 검증 커버리지(coverage) 및 false alarm 분석

## OPC 툴 구현 관련성
- SKOPC에서 ILT/커비리니어 OPC 출력물에 대한 마스크 검증 모듈 설계 시 필수 참조
- `2024_Wang_integrated_verification_flow_curvilinear.md`의 선행 이론 논문
- MULTIGON 레코드 지원 여부를 SKOPC 마스크 데이터 준비(MDP) 모듈의 장기 로드맵 항목으로 고려
- `2025_Yi_Bspline_curvilinear_mask_ILT_optimization.md`과 연계하여 커비리니어 OPC-검증 통합 파이프라인 설계의 기초

## 태그
`Verification`, `SPIE`, `Curvilinear`, `MRC`, `ILT`, `Mask Data`, `MULTIGON`, `Real-Curve`, `OPC`
