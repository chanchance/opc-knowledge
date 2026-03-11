# Model-Based OPC Using the MEEF Matrix III

## 메타데이터
- **저자**: (저자명 미확인 - SPIE 12954 수록)
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 1295418 (2024년 4월)
- **DOI/URL**: https://doi.org/10.1117/12.3010562

## 핵심 요약
"MEEF 행렬을 이용한 모델 기반 OPC" 시리즈의 세 번째 논문으로, 고 MEEF 레이어(특히 컨택 레이어)에서의 OPC 수렴 개선을 위한 Matrix-OPC 방법론의 발전된 내용을 다룬다. Matrix-OPC는 모든 엣지의 교차 MEEF(cross-MEEF)를 고려하면서 엣지 이동을 수행하여 EPE를 제어하는 고급 OPC 알고리즘이다.

## 주요 기여
1. **교차-MEEF 인식 OPC**: 단일 프래그먼트만 제어하는 기존 방식과 달리, EPE 사이트에 영향을 미치는 모든 프래그먼트를 동시에 고려
2. **컨택 레이어 수렴 개선**: 고 MEEF 저대비 조건에서도 더 적은 OPC 반복으로 더 나은 수렴 달성
3. **PSM 적용 확장**: 위상 시프트 마스크(PSM)에서 인접하지 않은 엣지의 영향을 교차-MEEF로 정확하게 처리
4. **생산 레시피 통합**: MatrixOPC 기능이 고객 생산 레시피에 일상적으로 사용될 수 있도록 실용화

## 검증 방법론
- Matrix-OPC 적용 전후의 OPC 수렴 반복 횟수 및 최종 EPE 비교
- 고 MEEF 컨택 레이어에서의 CD 균일성 및 공정 마진 평가
- PSM 레이어에서의 비인접 엣지 영향 보정 효과 측정

## OPC 툴 구현 관련성
- `skopc/modeling/` Model OPC 모듈에서 고 MEEF 컨택 레이어 처리를 위한 Matrix-OPC 알고리즘 구현 시 핵심 참고
- OPC 엔진의 수렴 가속화 전략으로 교차-MEEF 기반 엣지 이동 알고리즘 도입 고려
- 기존 SKOPC `2005_Kim_MEEF_full_chip_model_based_verification.md`의 최신 후속 연구로 연계
- PSM(위상 시프트 마스크) 지원 OPC 구현 시 교차-MEEF 처리 방법으로 활용

## 태그
`Verification`, `SPIE`, `OPC`, `MEEF`, `Matrix_OPC`, `Contact_Layer`, `Convergence`, `PSM`, `2024`
