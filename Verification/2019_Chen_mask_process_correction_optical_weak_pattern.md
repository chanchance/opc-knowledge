# Mask Process Correction for Optical Weak Pattern Improvement

## 메타데이터
- **저자**: Pai Chi Chen 외 (상세 저자 목록은 SPIE 원문 참조)
- **연도**: 2019
- **게재지**: Proc. SPIE 11178, Photomask Japan 2019, 2535770
- **DOI/URL**: https://doi.org/10.1117/12.2535770

## 핵심 요약
높은 MEEF(Mask Error Enhancement Factor)를 가진 광학적 취약 패턴(optical weak pattern)을 대상으로 MPC(Mask Process Correction)의 효과를 분석한 논문. MPC 적용 유무에 따른 취약 패턴의 광학 거동을 SEM 컨투어와 실제 웨이퍼 공정 윈도우 변화로 비교 검증하였다.

## 주요 기여
1. **높은 MEEF 취약 패턴 식별 및 분류**: MEEF가 높아 마스크 CD 오차에 민감한 패턴을 체계적으로 분류
2. **MPC vs. Non-MPC 광학 거동 비교**: MPC 적용 유무에 따른 취약 패턴의 aerial image 및 프린트 패턴 비교
3. **SEM 컨투어 기반 검증**: 시뮬레이션 컨투어와 실제 SEM 측정 컨투어의 정합성 검증
4. **공정 윈도우 변화 정량화**: MPC 적용 후 취약 패턴의 공정 윈도우(도즈, 포커스 여유) 개선량 측정
5. **마스크 제조와 OPC의 상호작용**: 마스크 CD 오차가 웨이퍼 패터닝에 미치는 영향을 MPC로 완화하는 통합 플로우

## 검증 방법론
- 높은 MEEF 취약 패턴을 선별하여 MPC 적용/비적용 마스크 제작
- CD-SEM으로 실제 웨이퍼 CD 측정 및 SEM 컨투어 추출
- 시뮬레이션 컨투어(OPC/litho 시뮬레이터)와 SEM 컨투어 오버레이 비교
- 포커스-도즈 매트릭스(FEM) 기반 공정 윈도우 면적 비교 (MPC 전후)
- MEEF 값과 공정 윈도우 개선량 간의 상관관계 분석

## OPC 툴 구현 관련성
- SKOPC의 OPC 검증 모듈에서 MEEF 기반 취약 패턴 자동 식별 기능 설계 시 참조
- 마스크 CD 오차(MPC 불완전성)를 OPC 모델 캘리브레이션에서 별도 항목으로 처리하는 근거
- `2005_Kim_MEEF_full_chip_model_based_verification.md`(기수집)의 후속 실용화 연구로, MEEF 검증 계보에서 중요 위치
- 높은 MEEF 패턴에 대한 OPC-MPC 공동 최적화 플로우 설계의 기초 문헌

## 태그
`Verification`, `SPIE`, `MEEF`, `MPC`, `Mask Process Correction`, `Weak Pattern`, `Process Window`, `SEM Contour`, `OPC`
