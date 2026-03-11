# High Accuracy OPC Electromagnetic Full-Chip Modeling for Curvilinear Mask OPC and ILT

## 메타데이터
- **저자**: Sakr 등
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III
- **DOI/URL**: https://doi.org/10.1117/12.3013089

## 핵심 요약
곡선형(curvilinear) 마스크 OPC 및 ILT(Inverse Lithography Technology)에서 정확한 전자기(EM) 마스크 3D 효과를 풀칩 수준에서 모델링하는 방법을 제시한다. EUV 리소그래피에서 마스크 위상 지연, 음영 효과, 마스크 흡수체 형상 등의 EM 효과는 OPC 정확도에 직접 영향을 미치며, 이를 풀칩 규모로 효율적으로 처리하는 프레임워크를 제안한다.

## 주요 기여
1. **풀칩 EM 모델링 프레임워크**: 곡선형 마스크 패턴에서의 전자기 회절 효과를 풀칩 규모로 확장 가능한 모델 구축
2. **곡선형 마스크 지원**: 기존 맨해튼(Manhattan) 마스크 전용 EM 모델을 곡선형 ILT 결과물에 적용 가능하도록 확장
3. **OPC/ILT 정확도 향상**: EM 효과를 반영한 OPC 보정으로 EUV 리소그래피의 웨이퍼 패턴 충실도 개선
4. **런타임 최적화**: 풀칩 적용을 위한 계산 효율성 확보

## 검증 방법론
- EUV 마스크의 EM 시뮬레이션 결과와 rigorous RCWA(Rigorous Coupled Wave Analysis) 기준 결과 대비 검증
- 곡선형 마스크 패턴에서 EPE 및 CD 정확도 평가
- 풀칩 런타임 대비 정확도 트레이드오프 분석

## OPC 툴 구현 관련성
- EUV OPC에서 마스크 3D(M3D) 효과 모델링 시 EM 효과 통합 필수
- `skopc/modeling/` 의 옵틱 모델에 M3D EM 보정 레이어 추가 고려
- 곡선형 마스크 지원을 위한 마스크 형상 표현 방식 확장과 연관
- ILT 결과 검증 단계에서 EM 기반 검증 루틴으로 활용 가능

## 태그
`Verification`, `SPIE`, `EUV`, `Electromagnetic`, `Curvilinear`, `Mask3D`, `OPC`, `ILT`, `Full_Chip`, `2024`
