# OPC and Modeling Solution to Support 0.55NA EUV Stitching

## 메타데이터
- **저자**: Qinglin Zeng, Dongbo Xu, Xuefeng Zeng, Werner Gillijns, Edita Tejnil, Yuyang Sun, Germain Fenger
- **연도**: 2024
- **게재지**: Proc. SPIE 13215, International Conference on Extreme Ultraviolet Lithography 2024, 1321507
- **DOI/URL**: https://doi.org/10.1117/12.3034957

## 핵심 요약
0.55NA 하이-NA EUV 리소그래피의 비대칭 투영계(x방향 4배, y방향 8배 축소)로 인해 노광 필드가 절반(26×16.5mm²)으로 줄어드는 문제를 해결하기 위한 인-다이 스티칭(in-die stitching) OPC 및 모델링 솔루션을 제안한 논문. Ta 기반 다크필드 마스크를 사용하여 두 노광 간의 스티칭 효과와 솔루션을 포괄적인 마스크 데이터 보정 플로우로 구현하였다.

## 주요 기여
1. **0.55NA 인-다이 스티칭 OPC 플로우**: 반필드 노광 경계에서 발생하는 스티칭 오차를 보정하는 완전한 마스크 데이터 보정 플로우
2. **스티칭 효과 정량화**: 두 노광의 경계 영역에서 발생하는 CD 및 오버레이 오차를 시뮬레이션으로 정량화
3. **Ta 기반 다크필드 마스크 최적화**: 스티칭 요구사항에 최적화된 Ta 흡수체 다크필드 마스크 설계 파라미터
4. **비대칭 광학계 OPC 모델**: 4× (x방향)와 8× (y방향) 다른 배율로 인한 비대칭 이미징 특성을 OPC 모델에 반영
5. **스티칭 라인 OPC 검증**: 스티칭 경계 영역에서의 OPC 검증 방법론 및 허용 기준 정의

## 검증 방법론
- 0.55NA 시뮬레이터로 스티칭 경계 영역의 CD 변화 및 패터닝 오차 정량화
- Ta 다크필드 마스크 기반 OPC 모델 캘리브레이션 및 스티칭 라인에서의 EPE 분포 분석
- 스티칭 OPC 적용 전후 경계 영역 EPE 비교
- 다크필드 vs. 밝은 배경 마스크 스티칭 성능 비교

## OPC 툴 구현 관련성
- SKOPC의 0.55NA 하이-NA EUV 지원 시 인-다이 스티칭 OPC 기능 설계의 핵심 참조
- `2025_Xu_OPC_model_dry_resist_055NA_EUV.md`와 함께 0.55NA EUV OPC 생태계 구성 쌍두 논문
- SKOPC 레시피 시스템에 스티칭 관련 OPC 파라미터(stitching zone 정의, 스티칭 보정 규칙) 추가 시 기준
- `2021_Xu_NXE3400_OPC_process_monitoring_model_validity.md`(동일 Xu 공동저자)와 함께 imec EUV OPC 모델 시리즈

## 태그
`Verification`, `SPIE`, `EUV`, `High-NA`, `0.55NA`, `Stitching`, `OPC`, `Mask`, `Dark Field`, `Ta Absorber`, `In-Die`
