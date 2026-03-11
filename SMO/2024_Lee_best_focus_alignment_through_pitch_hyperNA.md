# Best Focus Alignment Through Pitch Strategies for Hyper-NA EUV Lithography

## 메타데이터
- **저자**: Inhwan Lee et al.
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 129530O (10 April 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010846

## 핵심 요약
하이퍼NA EUV 리소그래피에서 다양한 피치 패턴 간 원하지 않는 최적 포커스(BF) 변동을 최소화하기 위한 through-pitch 포커스 정렬 전략을 제시한다. 마스크 3D(M3D) 효과로 인한 피치별 BF 변동이 패턴 방향과 마스크 톤(밝은/어두운 필드)에 따라 어떻게 달라지는지 분석한다.

## 주요 기여
1. **Through-pitch BF 정렬 전략**: 피치별 BF 이동을 최소화하는 마스크/소스 전략
2. **방향-톤별 M3D BF 분석**: 패턴 방향(H/V)과 마스크 톤이 M3D BF에 미치는 영향
3. **하이퍼NA 포커스 예산**: 하이퍼NA에서 M3D BF 분산이 포커스 예산에 미치는 영향
4. **SMO와 BF 정렬**: 소스 형상 최적화로 through-pitch BF 변동 완화 가능성

## 알고리즘/수식
### Through-pitch BF 정렬 분석
```
피치별 BF 이동 (M3D 효과):
  BFS(pitch, orientation, tone) = f(n_abs, k_abs, t_abs, pitch, NA)

하이퍼NA에서 BFS 증가:
  BFS_hyperNA > BFS_highNA > BFS_0.33NA
  → 피치별 BFS 분산 Δ_BFS 증가

방향 의존성:
  BFS_H(pitch) ≠ BFS_V(pitch)
  → H/V 패턴이 혼재하는 2D 설계에서 동시 최적화 불가

톤 의존성:
  BFS_bright(pitch) ≠ BFS_dark(pitch)
  → 밝은 vs 어두운 필드 마스크 선택이 BFS에 영향

Through-pitch 정렬 전략:
  1. 흡수층 박막화 (low-n, 24nm): BFS(pitch) 분산 감소
  2. 소스 최적화: 특정 피치 BFS 우선 최소화
  3. 서브 해상도 격자: BFS 보상 격자 추가
```

### BF 정렬 최적화
```
목표:
  min_{strategy} Δ_BFS = max_{pitch} BFS(pitch) - min_{pitch} BFS(pitch)

전략 평가:
  각 전략별 Δ_BFS 감소량 비교
  → 하이퍼NA에서 실용적인 포커스 예산 유지
```

## OPC 툴 SMO 구현 관련성
- Through-pitch BF SMO: SKOPC SMO에서 BFS 균일화를 비용 함수 항으로 추가
- 하이퍼NA 포커스 전략: >0.55NA EUV SMO/OPC 모듈 설계 참조
- 방향-톤 선택: SMO에서 마스크 톤 + 패턴 방향 공동 최적화
- 흡수층-SMO 연계: 박막 low-n 마스크와 SMO 결합으로 BFS 분산 최소화

## 태그
`EUV`, `hyper_NA`, `BFS`, `through_pitch`, `M3D`, `focus`, `SMO`, `orientation`, `mask_tone`, `SPIE`, `2024`
