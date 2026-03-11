# OPC and Modeling Solution to Support 0.55NA EUV Stitching

## 메타데이터
- **저자**: Qinglin Zeng, Dongbo Xu, Xuefeng Zeng, Werner Gillijns, Edita Tejnil, Yuyang Sun, Germain Fenger
- **연도**: 2024
- **게재지**: Proc. SPIE 13215, International Conference on Extreme Ultraviolet Lithography 2024, 1321507; 또한 Journal of Micro/Nanopatterning, Materials, and Metrology Vol. 24, Issue 4, 041203
- **DOI/URL**: https://doi.org/10.1117/12.3034957

## 핵심 요약
ASML이 개발한 High-NA(0.55NA) EUV 리소그래피 장비는 비대칭 투영 시스템(x방향 4×, y방향 8× 축소)을 사용하여 노출 필드 크기가 절반으로 줄어든다. 풀 필드 이상 크기의 다이에는 두 번의 노출 간 in-die 스티칭이 필요하며, 본 논문은 Ta 기반 dark field 마스크를 이용해 스티칭 효과와 OPC/모델링 솔루션을 연구한다.

## 주요 기여
1. **High-NA EUV 스티칭 OPC 플로우**: 0.55NA 비대칭 광학계에서 스티칭 영역 OPC 방법론 개발
2. **스티칭 오버랩 영향 분석**: 두 노출의 중첩 영역에서 발생하는 CD 변동 및 overlay 오차 분석
3. **Ta 기반 dark field 마스크 활용**: 스티칭 영역에서의 마스크 설계 최적화
4. **OPC 모델 확장**: 비대칭 축소율(4× vs 8×)을 반영한 OPC 모델 구축
5. **공정 창 분석**: 스티칭 전/후 공정 창 비교 및 허용 overlay 오차 범위 도출

## Recipe/Flow 상세
- **High-NA EUV 스티칭 OPC 플로우**:
  1. **광학 모델 설정**: 0.55NA 비대칭 시스템(x: 4×, y: 8× 축소) 파라미터 입력
  2. **스티칭 경계 정의**: 반 필드 경계에서 두 노출의 오버랩 영역 설정
  3. **마스크 설계**: Ta 기반 dark field 마스크로 스티칭 영역 패턴 배치
  4. **OPC 적용**: 각 노출 반쪽에 독립적으로 OPC → 스티칭 영역 보정 추가
  5. **스티칭 검증**: 오버랩 영역에서 CD 균일도, overlay 오차, 공정 창 측정
- **주요 과제**:
  - 비대칭 광학계에 의한 x/y 방향 비대칭 OPC 보정량
  - 스티칭 경계에서 두 노출의 광학 이미지 불연속성 보정
  - 마스크 스케일링(8×) 정밀도 요구사항
- **평가 지표**: 스티칭 영역 CD 균일도, overlay, 공정 창 (DOF × EL)

## OPC 툴 구현 관련성
- High-NA EUV 비대칭 광학계 OPC 모델 구현 시 x/y 축소율 분리 처리
- 스티칭 영역 특수 OPC 레시피 설계 방법
- `lithography_model.py`에 high-NA 비대칭 파라미터 추가
- 다중 노출 OPC 플로우 (per-exposure OPC + stitching correction)

## 태그
`HighNA_EUV`, `Stitching`, `OPC`, `0.55NA`, `Anamorphic`, `Mask`, `SPIE`, `2024`
