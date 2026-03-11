# High Accuracy OPC Electromagnetic Full-Chip Modeling for Curvilinear Mask OPC and ILT

## 메타데이터
- **저자**: Enas Sakr, Zac Levinson, Rob DeLancey, C. Jay Lee, Jinguang Li, Ryan Chen, Robert Iwanow, Delian Yang, Wolfgang Hoppe, Folarin Latinwo, Kevin Lucas, Peng Liu
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540N
- **DOI/URL**: https://doi.org/10.1117/12.3013089

## 핵심 요약
커비리니어 마스크 OPC 및 ILT(Inverse Lithography Technology) 워크플로우를 위한 고정밀 전자기(EM) 풀칩 모델링 방법론을 제안한 논문. 맨해튼 마스크 대비 커비리니어 마스크의 복잡한 3D 전자기 효과를 효율적으로 풀칩 수준에서 계산하는 접근법으로, EUV OPC 정확도를 향상시켰다.

## 주요 기여
1. **커비리니어 마스크 전용 EM 풀칩 모델**: 커비리니어 형상에서 발생하는 3D 마스크 전자기 효과를 풀칩 수준 OPC에 통합하는 고정밀 모델
2. **OPC 및 ILT 통합 적용**: 커비리니어 OPC와 ILT 두 워크플로우 모두에 적용 가능한 일반화된 EM 모델링 프레임워크
3. **계산 효율성 확보**: 3D EM 정밀도를 유지하면서도 풀칩 런타임에 적합한 컴팩트 모델 근사 방법
4. **EUV 마스크 물리 통합**: 마스크 섀도잉, 마스크 3D 효과(M3D), 흡수체 특성 등 EUV 고유 물리를 EM 모델에 통합
5. **커비리니어 OPC 정확도 검증**: 맨해튼 OPC 대비 커비리니어 OPC의 웨이퍼 프린터빌리티 개선을 EM 모델 기반으로 검증

## 검증 방법론
- EUV 커비리니어 마스크 패턴에 대한 리고러스 EM 시뮬레이션과 컴팩트 EM 모델의 정확도 비교
- 풀칩 OPC 플로우에서 EM 모델 적용 전후 EPE 분포 비교
- 맨해튼 vs. 커비리니어 마스크의 웨이퍼 CD 예측 정확도 비교 (EM 모델 기반)
- 런타임 벤치마크: 리고러스 EM vs. 컴팩트 EM 모델의 계산 시간 비교

## OPC 툴 구현 관련성
- SKOPC에서 커비리니어/ILT OPC 모듈의 마스크 3D 효과 모델링 구현 시 핵심 참조
- `2025_Eskin_WGNO_EUV_mask_3D_electromagnetic_simulation.md`(기수집)과 함께 EUV EM 모델링 계보 구성
- `2024_Wang_integrated_verification_flow_curvilinear_mask.md`와 연계하여 커비리니어 OPC-검증 통합 파이프라인의 모델링 계층 설계
- `2023_Sakr_EUV_low_k1_OPC_modeling_accuracy.md`(기수집)의 직접 후속 연구로 커비리니어 특화 확장

## 태그
`Verification`, `SPIE`, `EUV`, `Curvilinear`, `ILT`, `OPC`, `Electromagnetic Modeling`, `M3D`, `Full Chip`, `Mask 3D`
