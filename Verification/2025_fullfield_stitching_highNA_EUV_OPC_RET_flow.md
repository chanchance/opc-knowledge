# Full Field Stitching-Aware High-NA EUV OPC/RET Flow

## 메타데이터
- **저자**: Zachary Levinson, Yunqiang Zhang 등
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV (SPIE Advanced Lithography + Patterning 2025, San Jose, CA, 2025년 4월 22일)
- **DOI/URL**: https://doi.org/10.1117/12.3052709

## 핵심 요약
2nm 이하 디바이스 노드에서는 비대칭 광학계(anamorphic optics)를 탑재한 High-NA EUV 스캐너가 사용되며, 이 스캐너로 노광되는 레이어는 두 개 이상의 스티칭(stitched) 마스크 노광이 필요하다. 스티칭된 High-NA EUV 패턴 칩은 OPC 및 RET(Resolution Enhancement Technology) 마스크 합성 단계에 새로운 확장이 필요하며, 이를 위한 풀필드 스티칭 인식 OPC/RET 플로우를 제안한다.

## 주요 기여
1. **스티칭 인식 OPC**: 스티치 경계(stitch boundary)에서 패턴 연속성 및 CD 균일성을 유지하는 OPC 알고리즘 확장
2. **High-NA RET 옵션 검토**: 스티치 친화적(stitch-friendly) 패터닝을 위한 다양한 OPC/RET 옵션 분석
3. **2nm 이하 노드 적용**: 차세대 반도체 노드를 위한 실용적 마스크 합성 플로우 제시
4. **스티치 경계 EPE 관리**: 스티칭으로 인한 추가적인 EPE 오차 원인 분석 및 보정 전략

## 검증 방법론
- 스티치 경계 영역과 비경계 영역에서의 EPE 및 CD 정확도 비교
- 다양한 OPC/RET 옵션에 대한 스티칭 성능 평가
- High-NA EUV 시뮬레이션을 통한 스티칭 아티팩트 예측 및 검증

## OPC 툴 구현 관련성
- High-NA EUV 지원을 위한 OPC 엔진에 스티칭 경계 처리 기능 필수
- `skopc/modeling/` 내 광학 모델에 비대칭 NA(anamorphic optics) 시뮬레이션 지원 필요
- SMO 모듈에서 High-NA 스티칭 인식 소스 최적화 확장 시 참고
- 레시피 러너에서 멀티-마스크 스티칭 플로우 관리 방안으로 활용

## 태그
`Verification`, `SPIE`, `High_NA`, `EUV`, `Stitching`, `OPC`, `RET`, `2nm`, `2025`
