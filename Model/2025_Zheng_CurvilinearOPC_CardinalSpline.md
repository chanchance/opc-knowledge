# Curvilinear Optical Proximity Correction via Cardinal Spline

## 메타데이터
- **저자**: Su Zheng (CUHK), Xiaoxiao Liang (HKUST-GZ), Ziyang Yu (CUHK), Yuzhe Ma (HKUST-GZ), Bei Yu (CUHK), Martin Wong (HKBU)
- **연도**: 2025
- **게재지**: 2025 62nd ACM/IEEE Design Automation Conference (DAC)
- **DOI/URL**: https://doi.org/10.1109/DAC63849.2025.11133367

## 핵심 요약
Cardinal spline을 이용하여 마스크 패턴을 제어점(control point)으로 표현하고, 리소그래피 시뮬레이션 기반으로 제어점을 반복적으로 조정하는 새로운 curvilinear OPC 프레임워크를 제안한다. ILT 결과를 fitting하고 MRC 위반을 해결하는 알고리즘을 포함하며 OPC/ILT 대안으로의 가능성을 입증한다.

## 주요 기여
- Cardinal spline 기반 마스크 패턴 표현: 제어점 연결로 연속 곡선 마스크 생성
- 리소그래피 시뮬레이션 guided 제어점 반복 최적화
- 포괄적 MRC 준수 방법: width, space, area, curvature 검사 알고리즘
- ILT 결과 fitting 및 MRC 위반 해결 알고리즘
- OPC와 ILT 성능 갭 브릿지: curvilinear OPC의 ILT 대안 가능성 입증

## 모델 수식/아키텍처
- Cardinal spline: 제어점 {P_i}를 통과하는 C1 연속 보간 곡선
  - P(t) = 0.5·[(2P₁) + (-P₀+P₂)t + (2P₀-5P₁+4P₂-P₃)t² + (-P₀+3P₁-3P₂+P₃)t³]
- 제어점 이동: EPE/VPE 기반 gradient 계산 → 제어점 위치 업데이트
- MRC 검사: 곡률(curvature) 제약 κ ≤ κ_max 포함한 통합 마스크 규칙 검증
- ILT fitting: ILT 출력 binary mask → cardinal spline 근사

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC의 curvilinear OPC 엔진 구현 시 cardinal spline 기반 마스크 표현 채택 가능
- ILT 결과를 curvilinear OPC 형태로 변환하는 fitting 모듈 설계 참고
- MRC 준수 알고리즘 (width/space/area/curvature)의 실용적 구현 참조
- GDS 출력을 위한 곡선 마스크 형상 표현에 적용 가능

## 태그
`Model`, `IEEE`, `DAC`, `Curvilinear OPC`, `Cardinal Spline`, `ILT`, `MRC`, `Mask Optimization`, `CUHK`
