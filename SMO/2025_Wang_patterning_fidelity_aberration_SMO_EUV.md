# Patterning Fidelity Enhancement and Aberration Mitigation in EUV Lithography Through Source–Mask Optimization

## 메타데이터
- **저자**: (Wang et al., 상세 저자 정보 MDPI Micromachines 2025)
- **연도**: 2025 (접수: 2025-09-08, 수정: 2025-10-01, 승인: 2025-10-13)
- **게재지**: MDPI Micromachines, Vol. 16, Issue 10, 1166
- **DOI/URL**: https://doi.org/10.3390/mi16101166 (PMC: https://pmc.ncbi.nlm.nih.gov/articles/PMC12566352/)

## 핵심 요약
EUV 리소그래피에서 3nm 이하 기술 노드로의 스케일링 시 발생하는 수차(aberration) 제어와 패터닝 충실도(patterning fidelity) 문제를 SMO를 통해 동시에 해결하는 종합적 최적화 프레임워크를 제안한다. CD, EL, MEF를 포함하는 비용 함수로 40nm 최소 피치(2nm 노드 BEOL 대표 패턴)에서 정량적 개선을 시연한다.

## 주요 기여
1. **수차 인식 SMO 프레임워크**: Zernike 수차를 명시적으로 고려한 소스-마스크 공동 최적화
2. **다중 메트릭 최적화**: CD 균일성, 노출 위도(EL), 마스크 오차 인수(MEF) 동시 최적화
3. **복합 수차 보상**: 고립 수차와 무작위 고차 성분을 포함한 복합 혼합 모드 오차 보상
4. **정량적 성능 개선** (40nm 피치, 2nm 노드 BEOL):
   - CD 균일성 변동 4.02% 감소
   - 노출 위도(EL) 1.48% 향상
   - 마스크 오차 인수(MEF) 5.45% 감소

## 알고리즘/수식
### 수차 인식 SMO 비용 함수
```
Cost = w_CD · ||CD_sim - CD_target||²
     + w_EL · max(0, EL_min - EL_current)²
     + w_MEF · ||MEF - MEF_target||²
     + w_ab · Σ_k (∂CD/∂Z_k)² · σ_k²

여기서:
- Z_k: k번째 Zernike 계수
- σ_k: k번째 Zernike 계수의 불확실성
- w_*: 각 메트릭 가중치
- ∂CD/∂Z_k: CD의 수차 민감도
```

### 최적화 대상
- 소스(source): 픽셀화 조명 분포 J(k_x, k_y)
- 마스크(mask): 이진/attPSM 마스크 패턴 M(x, y)

### 수차 유형 분류
1. **고립 수차**: 단일 Zernike 항 (예: Z8 코마, Z9 구면수차)
2. **복합 혼합 수차**: 무작위 고차 Zernike 성분 조합
- 두 경우 모두에서 SMO가 효과적임을 시연

### 타겟 패턴
- 40nm 최소 피치 패턴
- 2nm 노드 BEOL(Back-End-Of-Line) 대표 패턴

## OPC 툴 SMO 구현 관련성
- EUV SMO 비용 함수에 Zernike 수차 민감도 항 통합 필요
- 수차 인식 SMO는 하드웨어 기반 수차 보정의 보완책으로 필수화 추세
- SKOPC SMO 모듈에서 수차 파라미터를 비용 함수에 포함하는 설계 방향 제시
- sub-3nm 노드에서 SMO가 수차 완화의 핵심 계산 리소그래피 기법임을 확인
- CD/EL/MEF 트리플 메트릭 최적화: 단일 메트릭 최적화 대비 공정 안정성 대폭 향상

## 태그
`SMO`, `EUV`, `aberration`, `Zernike`, `patterning_fidelity`, `MEF`, `exposure_latitude`, `CD_uniformity`, `2nm_node`, `BEOL`, `MDPI`
