# OPC Verification Considering CMP-Induced Topography

## 메타데이터
- **저자**: Kim, S. et al. (Samsung Electronics)
- **연도**: 2015
- **게재지**: Proc. SPIE 9661, 35th Annual BACUS Symposium on Photomask Technology
- **DOI/URL**: https://doi.org/10.1117/12.2196646
- **인용수**: ~25

## 핵심 요약
CMP(Chemical Mechanical Planarization) 공정이 유발하는 웨이퍼 토포그래피(topography) 변동이 OPC 검증(verification)에 미치는 영향을 분석한다. 첨단 공정 노드(28nm 이하)에서 CMP 유발 토포그래피는 후속 리소그래피 공정의 공정 윈도우를 감소시키는 주요 요인이 됨을 실험으로 입증한다. CMP 토포그래피를 고려한 개선된 OPC 검증 방법론을 제안한다.

## 주요 기여
1. CMP 토포그래피가 OPC 검증 결과에 미치는 영향 최초 체계적 분석
2. CMP 유발 디싱(dishing) 및 부식(erosion)의 패턴 밀도·폭 의존성 모델링
3. 효과적 포커스 이동(effective focus shift)으로 CMP 토포그래피 영향 통합
4. CMP 인식(CMP-aware) OPC 검증 플로우 개발
5. 실제 28nm 칩 데이터로 CMP 핫스팟 예측 정확도 향상 실증

## 모델 수식/아키텍처

**CMP 토포그래피 모델:**
```
h_CMP(x,y) = h_nominal - Δh_dishing(W, density) - Δh_erosion(density)
```
W = 패턴 폭, density = 로컬 패턴 밀도

**디싱(Dishing) 모델:**
```
Δh_dishing(W) = α · W^β   [폭 의존 함수]
```
α, β = CMP 공정 파라미터 (실험 캘리브레이션)

**부식(Erosion) 모델:**
```
Δh_erosion(ρ) = γ · ρ · (1 - ρ)   [밀도 의존 함수]
```
ρ = 로컬 패턴 밀도 (0~1), γ = 공정 파라미터

**유효 포커스 이동:**
```
ΔBF_CMP(x,y) = h_CMP(x,y) - h_nominal
             = -Δh_dishing(x,y) - Δh_erosion(x,y)
```

**CMP 인식 OPC 검증:**
```
EPE_CMP(x,y) = EPE(focus_nom + ΔBF_CMP(x,y), dose_nom)
```
토포그래피 맵 → 위치별 유효 포커스 이동 → 보정 OPC 검증

**공정 윈도우 감소:**
```
PW_effective = PW_nominal - |ΔBF_CMP_max| - |ΔBF_CMP_min|
```

## 모델 유형
- [x] 광학 모델 (유효 포커스 이동)
- [ ] 레지스트 모델
- [ ] ML/DL
- [x] 하이브리드 (CMP 물리 모델 + 광학 OPC 모델)

## OPC 툴 구현 관련성
- skopc OPC 검증 플로우에 CMP 토포그래피 맵 입력으로 통합
- CMP 토포그래피 맵: TCAD 시뮬레이션 또는 측정 데이터 활용
- 포커스 이동 변환: 토포그래피 맵 → 위치별 디포커스 → OPC 모델 적용
- 28nm 이하 상위 메탈 레이어에서 특히 중요
- 핫스팟 예측: CMP 토포그래피 + OPC 모델 결합으로 정확도 향상

## 참고문헌
- Ye, J. et al., "Fast lithography simulation under focus variations" (2006)
- Sturtevant, J. et al., "Roadmap to sub-nanometer OPC model accuracy" (2012)
- Samsung CMP process modeling papers

## 태그
`Model`, `SPIE`, `CMP`, `Topography`, `OPCVerification`, `FocusShift`, `ProcessWindow`, `28nm`, `2015`
