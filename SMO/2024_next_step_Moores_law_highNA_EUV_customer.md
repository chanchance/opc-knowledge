# The Next Step in Moore's Law: High-NA EUV Introduction at the Customer

## 메타데이터
- **저자**: (SPIE 12953 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical Microlithography XXXVI, 129530P (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3009070

## 핵심 요약
고NA EUV 리소그래피(0.55NA)의 고객 현장 도입 단계를 다루며, 0.33NA 대비 공정 복잡성 감소, 수율 향상, 고해상도의 이점을 제시한다. 고NA EUV의 핵심 과제인 스티칭 관리, M3D 증강, 소스-마스크 최적화 등의 해결 방향을 논의한다.

## 주요 기여
1. **고NA EUV 고객 도입 현황**: 0.55NA EUV 스캐너의 실제 고객 설치 및 초기 결과
2. **0.33NA 대비 이점 정량화**: 해상도 향상, 공정 복잡성 감소 데이터
3. **핵심 과제 해결**: 스티칭, M3D, 확률론적 효과의 0.55NA 특화 해결책
4. **SMO/OPC 요구사항**: 고NA EUV에서 새로운 SMO/OPC 요구사항 정리

## 알고리즘/수식
### 고NA EUV 이점과 과제
```
이점:
  해상도 향상: NA 0.33 → 0.55 (67% 향상)
  k1 하한 감소: 더 작은 피치 단일 패터닝 가능
  공정 단순화: 다중 패터닝 → 단일 패터닝

주요 과제:

1. 스티칭 (Stitching):
   아나모픽 광학(4x/8x)으로 필드 절반씩 노출
   → OPC: 상/하단 필드 각각 최적화 + 경계 연속성

2. M3D 증강:
   NA 증가 → 경사 입사각 증가 → 마스크 옆면 회절 강화
   M3D_0.55NA >> M3D_0.33NA
   → 더 정밀한 M3D 보정 OPC 필요

3. 확률론적 효과:
   NA 증가 → 픽셀당 광자 수 감소 (동일 도즈 기준)
   → 고NA에서 더 강화된 stochastic OPC 필요

SMO 요구사항:
   새로운 동공(pupil) 형상 최적화: σ, 극수(poles) 등
   소스 편광 최적화: 고NA에서 TE/TM 분리 더 중요
```

## OPC 툴 SMO 구현 관련성
- 고NA EUV 도입 로드맵: SKOPC 고NA 지원 개발 시기 및 우선순위 참조
- 스티칭 OPC: 고NA 스티칭 인식 OPC 필수 기능으로 확인
- M3D 강화 보정: 고NA OPC에서 M3D 보정 비중 증가
- SMO 고NA 모드: 0.55NA에 최적화된 소스 형상 설계

## 태그
`EUV`, `high_NA`, `0p55NA`, `Moores_law`, `customer_introduction`, `stitching`, `M3D`, `stochastic`, `SMO`, `OPC`, `SPIE`, `2024`
