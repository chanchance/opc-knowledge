# Extending Logic Metal Printing with Sub-Resolution Grating in High and Hyper NA EUV Lithography

## 메타데이터
- **저자**: (SPIE 13424 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 134240R (22 April 2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051144

## 핵심 요약
고NA 및 하이퍼NA EUV 리소그래피에서 서브 해상도 격자(sub-resolution grating)를 이용하여 로직 메탈 인쇄를 확장하는 방법을 제안한다. 포커스 정렬을 위한 서브 해상도 격자 기법으로 피치 간 포커스 변동을 최소화하여 로직 메탈 레이어의 공정 창을 향상시킨다.

## 주요 기여
1. **서브 해상도 격자 포커스 정렬**: 피치 간 BFS 차이를 서브 해상도 격자로 보상
2. **고NA/하이퍼NA 로직 메탈 확장**: 더 작은 피치에서도 충분한 공정 창 달성
3. **Through-pitch 포커스 균일화**: 다양한 피치의 로직 메탈 패턴에서 포커스 조건 균일화
4. **SMO와 격자 최적화 결합**: 서브 해상도 격자와 소스 최적화의 결합 효과

## 알고리즘/수식
### 서브 해상도 격자를 이용한 포커스 정렬
```
고NA/하이퍼NA에서 피치별 BFS 문제:
  BFS(pitch_A) ≠ BFS(pitch_B) (마스크 M3D 효과로 인해)
  → 단일 포커스 설정에서 일부 피치는 포커스 이탈

서브 해상도 격자 원리:
  마스크에 서브 해상도 보조 격자 추가
  → 회절 패턴 변경 → BFS(pitch) 분산 감소

격자 최적화:
  격자 주기 Λ*, 격자 듀티비 DC* = argmin_{Λ, DC} Δ_BFS
  subject to: 격자 자체가 웨이퍼에 인쇄되지 않는 조건 (서브 해상도)

통합 SMO:
  격자 파라미터 + 소스 형상 공동 최적화
  min_{J, Λ, DC} Cost(BFS_uniformity, EPE, PW)
```

## OPC 툴 SMO 구현 관련성
- 서브 해상도 격자 SMO: SKOPC SMO에서 보조 격자 파라미터 최적화 확장
- Through-pitch 포커스: 랜덤 로직 메탈 SMO에서 피치별 BFS 균일화 목표
- 고NA/하이퍼NA 지원: 0.55NA 이상 EUV SMO/OPC 모듈 설계 참조
- 격자-마스크 공동 설계: OPC 마스크에 포커스 정렬용 보조 격자 통합

## 태그
`EUV`, `high_NA`, `hyper_NA`, `sub_resolution_grating`, `focus_alignment`, `BFS`, `through_pitch`, `logic_metal`, `SMO`, `OPC`, `SPIE`, `2025`
