# Affordable Optical Proximity Correction Runtime for EUV Curvilinear Mask Tape-Out Flow

## 메타데이터
- **저자**: (저자명 미확인 - SPIE 12954 수록)
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III
- **DOI/URL**: https://doi.org/10.1117/12.3009981

## 핵심 요약
EUV 리소그래피용 곡선형(freeform/curvilinear) 마스크 테이프아웃 플로우에서 OPC 및 검증 런타임을 실용적인 수준으로 낮추는 방법을 제시한다. 소스 최적화, OPC/검증, 마스크 프로세스 보정(MPC), 데이터 볼륨, 마스크 라이팅 시간 등 다양한 병목을 다중 엔진 연계를 통해 해결한다.

## 주요 기여
1. **다중 엔진 연계 플로우**: 서로 다른 정확도/속도 특성을 가진 엔진들을 조합하여 최적 런타임-정확도 균형 달성
2. **곡선형 마스크 테이프아웃 지원**: 프리폼 마스크의 OPC, MPC, 데이터 프랙처(fracture)까지 통합
3. **런타임 분석**: 소스 최적화 → OPC → 검증 → MPC → 프랙처 각 단계별 런타임 분석 및 병목 해소
4. **실용적 검증 전략**: 정확도를 유지하면서 풀칩 검증 가능한 수준으로 런타임 절감

## 검증 방법론
- 각 플로우 단계별 런타임 측정 및 비교
- EPE 및 CD 정확도를 기준점(reference) 대비 유지 여부 확인
- 곡선형 마스크 OPC 결과물의 마스크 라이팅 적합성(MRC 준수) 검증

## OPC 툴 구현 관련성
- `skopc`의 레시피 러너(Recipe Runner)에서 OPC → 검증 → MPC 순서 자동화와 직접 관련
- 다중 정확도 모드(fast/accurate) 전환 기능을 OPC 엔진에 구현할 때 참고
- 곡선형 마스크 지원 플로우 설계 시 런타임 예산 배분 전략으로 활용
- `skopc/modeling/` 파이프라인의 멀티엔진 조합 아키텍처에 참고

## 태그
`Verification`, `SPIE`, `EUV`, `Curvilinear`, `OPC`, `Runtime`, `Tape-Out`, `MPC`, `2024`
