# Advancing Semiconductor Patterning with EUV Hyper NA: Opportunities and Challenges

## 메타데이터
- **저자**: Gerardo Bottiglieri, Pieter Woltgens, Reinier van der Meer, Sander Blok, Bram Slachter, John McNamara, Mark van de Kerkhof, Jan van Schoot, Michael Patra, Jens Timo Neumann, Heiko Feldmann
- **소속**: ASML (네덜란드)
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 1342404 (22 April 2025)
- **DOI/URL**: https://doi.org/10.1117/12.3050509

## 핵심 요약
EUV 하이퍼 NA(0.55NA 이상) 리소그래피가 2030년 이후 선진 로직 노드에서 패턴 축소를 가능하게 함을 시연한다. 더 큰 NA에서 증강된 마스크-3D 효과와 감소된 DOF 등의 고유한 도전 과제를 분석하고, 하이퍼 NA가 가져다주는 해상도 향상 기회를 정량화한다.

## 주요 기여
1. **하이퍼 NA 해상도 향상**: EUV 하이퍼 NA(>0.55NA)에서 선진 로직 노드 패턴 축소 시연
2. **M3D 증강 효과 분석**: 더 큰 NA에서 마스크-3D 효과 강화와 그 완화 전략
3. **DOF 감소 과제**: 높은 NA에서의 DOF 감소 및 공정 창 관리 방법
4. **2030년 이후 로드맵**: 하이퍼 NA EUV 기반 기술 로드맵 제시

## 알고리즘/수식
### 하이퍼 NA EUV 이미징 특성
```
이미징 해상도:
  CD_min ∝ k1 × λ / NA
  하이퍼 NA (NA > 0.55): CD_min 추가 축소

마스크-3D 효과 증강:
  EUV 입사각: θ_inc = arcsin(NA_mask / n_medium)
  더 큰 NA → 더 큰 입사각 → 더 강한 그림자 효과

DOF 스케일링:
  DOF ∝ λ / NA²
  NA 증가 시 DOF 급격 감소: DOF ∝ 1/NA²

공정 창 관리:
  ΔCD(defocus) = ΔCD(M3D) + ΔCD(aberration) + ΔCD(stochastic)
  하이퍼 NA: 모든 항목 증가 → 엄격한 SMO 필요
```

### 하이퍼 NA 도전 과제
1. M3D 효과: NA 증가로 EUV 마스크 그림자/위상 효과 강화
2. DOF 감소: NA² 비례 DOF 감소 → 공정 창 축소
3. 마스크 흡수층: 하이퍼 NA 최적화된 새로운 흡수층 재료 필요
4. 조명 설계: 하이퍼 NA 특화 최적 조명(소스) 형상 재설계

## OPC 툴 SMO 구현 관련성
- 하이퍼 NA SMO는 0.55NA SMO보다 더 엄격한 M3D 보상 필요
- DOF 급감으로 SMO 비용 함수에서 DOF 항의 가중치 증가 필요
- 하이퍼 NA용 새로운 소스 형상 설계: 기존 0.33NA/0.55NA 소스 재사용 불가
- SKOPC 장기 로드맵에서 하이퍼 NA 지원을 위한 아키텍처 확장 방향

## 태그
`SMO`, `EUV`, `hyper_NA`, `high_NA`, `M3D`, `DOF`, `resolution`, `2030_roadmap`, `ASML`, `SPIE`
