# Source Mask Optimization (SMO) Study for High-NA EUV Lithography to Achieve Single Patterning on Random Logic Metal

## 메타데이터
- **저자**: (SPIE 12954 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540X (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010869

## 핵심 요약
고NA EUV 리소그래피(0.55NA)에서 SMO를 통해 랜덤 로직 메탈 레이어의 싱글 패터닝 가능성을 평가한다. 최소 피치 24nm, 22nm, 20nm에서의 패터닝 성능을 SMO로 최적화하여 고NA EUV 싱글 패터닝의 실용성을 검증한다.

## 주요 기여
1. **고NA EUV SMO 연구**: 0.55NA EUV에서 랜덤 로직 메탈 싱글 패터닝을 위한 SMO 평가
2. **다중 피치 성능 분석**: 24nm, 22nm, 20nm 피치에서 SMO 최적화 결과 정량화
3. **싱글 패터닝 실현 가능성**: SMO를 통한 고NA EUV 싱글 패터닝 조건 탐색
4. **랜덤 로직 적용**: 반복 패턴이 아닌 실제 랜덤 로직 디자인에 대한 SMO 적용

## 알고리즘/수식
### 고NA EUV SMO 프레임워크
```
목표: 랜덤 로직 메탈 레이어 싱글 패터닝 실현

최적화 변수:
  - 소스 형상 J (픽셀화 조명, 0.55NA 조명 시스템)
  - 마스크 패턴 M (OPC + SRAF)

비용 함수:
  Cost = Σ_i [w_EPE·||EPE_i||² + w_PW·(-DOF·EL)]
  + w_stoch·P_fail + w_LCDU·LCDU²

피치별 최적화:
  min_pitch = 20nm (k1 ~ 0.55 at 0.55NA, λ=13.5nm)
  24nm pitch: 비교적 여유 있는 공정 창
  20nm pitch: 고NA EUV 한계 해상도 근처
```

### 랜덤 로직 SMO 특이 사항
```
랜덤 로직 vs 반복 패턴:
  반복 패턴: 단일 피치 최적화 소스로 충분
  랜덤 로직: 다중 피치 패턴 공존 → through-pitch 소스 최적화 필요

Through-pitch 소스 최적화:
  J* = argmin_J Σ_pitch Cost(pitch)
  → 모든 피치에서 균형잡힌 성능 달성
```

## OPC 툴 SMO 구현 관련성
- 고NA EUV SMO 설계: 0.55NA 지원 SMO 모듈의 핵심 참조
- 랜덤 로직 패턴 SMO: 단일 클립이 아닌 다양한 패턴 혼합 최적화
- 싱글 패터닝 조건 도출: SMO 비용 함수에서 싱글 패터닝 달성 기준 설정
- SKOPC SMO 모듈에서 고NA EUV 랜덤 로직 지원 아키텍처 참조

## 태그
`SMO`, `EUV`, `high_NA`, `single_patterning`, `random_logic`, `metal_layer`, `through_pitch`, `24nm`, `22nm`, `20nm`, `DTCO`, `SPIE`
