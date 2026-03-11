# High Accuracy OPC Electromagnetic Full-Chip Modeling for Curvilinear Mask OPC and ILT

## 메타데이터
- **저자**: Enas Sakr, Zac Levinson, Rob DeLancey, C. Jay Lee, Jinguang Li, Ryan Chen, Robert Iwanow, Delian Yang, Wolfgang Hoppe, Folarin Latinwo, Kevin Lucas, Peng Liu
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540N
- **DOI/URL**: https://doi.org/10.1117/12.3013089

## 핵심 요약
Curvilinear 마스크 OPC 및 ILT(Inverse Lithography Technology)에서 요구되는 고정밀 전자기(EM) 모델을 full-chip 규모로 구현하는 방법을 연구한다. 곡선 형상의 마스크에서 발생하는 마스크 3D 전자기 효과를 정확하게 캡처하면서도 full-chip OPC 런타임을 허용 가능한 수준으로 유지하는 접근법을 제시한다.

## 주요 기여
1. **Curvilinear 마스크 EM 모델**: 곡선 형상 마스크의 전자기 효과(마스크 3D)를 정확히 모델링
2. **Full-chip 확장성**: RCWA 등 rigorous EM 시뮬레이션의 full-chip OPC 적용 가능성 확보
3. **EUV 마스크 특화**: EUV 특유의 반사형 마스크 구조(흡수체, 다층막)의 EM 효과 처리
4. **OPC-ILT 통합**: OPC와 ILT 양쪽에서 동일한 EM 모델 활용
5. **모델 정확도 검증**: 웨이퍼 프린팅 결과와의 비교를 통한 EM 모델 정확도 평가

## Recipe/Flow 상세
- **Curvilinear Mask EM 모델 기반 OPC 플로우**:
  1. **EM 모델 구축**:
     - EUV 마스크 스택 파라미터 입력 (흡수체 두께/재질, 다층막 구조)
     - RCWA 기반 rigorous EM 시뮬레이션으로 기준 데이터 생성
     - 컴팩트 EM 모델 피팅 (Hopkins 보정항 + 마스크 3D 보정)
  2. **Curvilinear 형상 처리**:
     - 베지어/폴리곤 기반 curvilinear 마스크 형상의 EM 효과 분석
     - 곡률에 따른 EM 효과 변화 캡처
  3. **Full-chip OPC 적용**:
     - 컴팩트 EM 모델로 full-chip OPC 수행 (런타임 허용 범위)
     - 임계 위치에만 rigorous EM 재계산 (하이브리드 방식)
  4. **ILT 통합**:
     - EM 모델 기반 ILT 목적함수 계산
     - Curvilinear ILT 결과의 EM 보정 검증
  5. **검증**: SEM 측정 및 웨이퍼 프린팅 결과와 EM 모델 예측 비교
- **EUV 마스크 EM 효과**:
  - 흡수체 사이드월 각도 → 비대칭 이미지
  - 다층막 위상 효과 → CD 오차
  - 근접 패턴 간 EM 간섭 → 2D 형상 오차

## OPC 툴 구현 관련성
- SKOPC의 EUV OPC 모델에 마스크 3D EM 보정 추가
- Curvilinear 마스크 OPC 모델 정확도 향상 전략
- `euv_em_model.py`: RCWA 기반 EM 효과 컴팩트 모델 구현
- Full-chip EM 모델 OPC에서 rigorous와 compact 하이브리드 전환 기준

## 태그
`EUV`, `ElectromagneticModel`, `CurvilinearMask`, `OPC`, `ILT`, `FullChip`, `Mask3D`, `SPIE`, `2024`
