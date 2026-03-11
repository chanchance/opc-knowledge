# 3D EUV Mask Simulator Based on Physics-Informed Neural Networks: Effects of Polarization and Illumination

## 메타데이터
- **저자**: V. Medvedev, A. Erdmann, A. Rosskopf
- **연도**: 2024
- **게재지**: Proc. SPIE 13023, Computational Optics 2024, 1302304 (2024년 6월 17일)
- **DOI/URL**: https://doi.org/10.1117/12.3013159

## 핵심 요약
`2024_PINN_3D_mask_simulation_lithographic_imaging_EUV.md`(SPIE 12953)의 후속 연구로, PINN 기반 EUV 마스크 3D 시뮬레이터를 편광(polarization) 효과 및 가변 조명(variable illumination) 설정으로 확장한다. 단일 훈련으로 임의의 마스크 형상과 조명 조건에 대해 밀리초 단위 응답을 제공하는 범용 PINN 기반 마스크 솔버를 구현한다.

## 주요 기여
1. **편광 효과 모델링**: 흡수체 엣지 근방 및 다층막 내부의 상대적으로 작지만 주목할 만한 편광 효과를 PINN으로 정확하게 예측
2. **가변 조명 지원**: 조명 방향 및 노광 파장 변화에 따른 반사 EUV 광의 영향을 PINN으로 시뮬레이션
3. **범용 솔버 구현**: 재훈련 없이 임의의 마스크 형상과 조명 조건에 대해 밀리초 수준 마스크 산란 응답 예측
4. **다색광(polychromatic) 효과 모델링**: 협대역이 아닌 스펙트럼 범위의 EUV 광원에서의 효과까지 확장

## 검증 방법론
- PINN 예측 편광 효과와 rigorous EMF 솔버(RCWA) 결과 비교
- 경사 조명(oblique illumination) 및 다색광 효과 예측 정확도 정량 평가
- 재훈련 없는 일반화 성능: 다양한 마스크 형상 및 조명 조건에서 검증

## OPC 툴 구현 관련성
- `2024_PINN_3D_mask_simulation_lithographic_imaging_EUV.md`와 연계하여 PINN 기반 EUV 마스크 3D 솔버 개발 로드맵 구성
- `skopc/modeling/` LithoEngine의 EUV 광학 시뮬레이션에서 빠른 M3D 응답 계산기로 통합 가능
- 편광 효과를 고려한 EUV OPC 모델의 정확도 향상에 직접 활용
- 재훈련 없는 범용 솔버 특성은 다양한 EUV 공정 조건 탐색에 유리

## 태그
`Verification`, `SPIE`, `EUV`, `PINN`, `Physics_Informed`, `Mask3D`, `Polarization`, `Illumination`, `Universal_Solver`, `2024`
