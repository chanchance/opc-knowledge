# 3D EUV Mask Simulator Based on Physics-Informed Neural Networks: Effects of Polarization and Illumination

## 메타데이터
- **저자**: V. Medvedev, A. Erdmann, A. Rosskopf
- **연도**: 2024
- **게재지**: Proc. SPIE 13023, Computational Optics 2024, 1302304
- **DOI/URL**: https://doi.org/10.1117/12.3013159

## 핵심 요약
EUV 마스크 3D 시뮬레이션을 위한 PINN 기반 시뮬레이터를 편광(polarization) 효과와 가변 조명 조건으로 확장한다. 동일 저자의 2024 SPIE Optical Litho 논문(SPIE 12953)의 후속 연구로 편광 의존성과 다양한 조명 설정을 추가로 검토한다.

## 주요 기여
1. PINN EUV 마스크 시뮬레이터의 편광(TE/TM) 효과 처리 능력 평가
2. 다양한 조명 조건(부분 가간섭도, 조명 형상)에서의 PINN 적용성 검증
3. 편광 의존성이 M3D 효과 예측 정확도에 미치는 영향 분석
4. 가변 조명 파라미터 입력 조건부 PINN 아키텍처 확장
5. Computational Optics 컨퍼런스에서 발표된 후속 검증 연구

## 모델 수식/아키텍처
- **조건부 PINN**: (x,y,z, polarization, illumination_params) → E(x,y,z)
- 편광 입력: TE(s-편광), TM(p-편광) 또는 혼합 편광
- 조명 파라미터: σ_outer, σ_inner, 조명 형상(annular, dipole, quadrupole)
- 물리 제약: 편광별 맥스웰 방정식 경계 조건 적용
- 검증 지표: 편광별 CD 변화, 이미지 대비, M3D 위상 오차

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [x] ML/DL
- [x] 하이브리드

## OPC 툴 구현 관련성
- EUV 편광 조명 최적화(SMO)와 M3D 시뮬레이션의 결합 가능성 탐색
- 다양한 조명 조건에서 재학습 없이 적용 가능한 PINN 구조 참조
- `2024_Medvedev_PINN_M3D_EUV.md`와 쌍으로 읽어야 하는 후속 논문
- High-NA EUV(0.55NA) 편광 효과 시뮬레이션에 확장 적용 가능

## 태그
`Model`, `PINN`, `M3D`, `EUV`, `Polarization`, `Illumination`, `PhysicsInformed`, `Erdmann`, `SPIE`
