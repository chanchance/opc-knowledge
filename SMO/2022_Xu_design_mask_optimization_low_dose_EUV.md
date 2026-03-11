# Design and Mask Optimization Toward Low Dose EUV Exposure

## 메타데이터
- **저자**: Dongbo Xu, Werner Gillijns, Ryoung-han Kim
- **소속**: imec (벨기에)
- **연도**: 2022
- **게재지**: Proc. SPIE 12052, DTCO and Computational Patterning, 120520C (26 May 2022)
- **DOI/URL**: https://doi.org/10.1117/12.2614268

## 핵심 요약
EUV 리소그래피의 처리량(throughput) 향상을 위한 저도즈(low dose) 노출을 설계 및 마스크 최적화로 실현하는 방법을 연구한다. 저도즈 노출은 CD 균일성과 선폭 거칠기(LWR)를 악화시키는 문제를 갖지만, 설계-마스크 공동 최적화를 통해 공정 성능을 유지하면서 도즈를 감소하는 방법론을 실험적으로 검증한다.

## 주요 기여
1. **저도즈 EUV 실현 방법론**: 설계 및 마스크 최적화로 도즈 감소-성능 유지 동시 달성
2. **처리량-성능 트레이드오프 분석**: EUV 도즈 감소가 CD 균일성/LWR에 미치는 영향 정량화
3. **설계-마스크 공동 최적화**: 레이아웃 설계와 마스크 OPC를 결합한 저도즈 전략
4. **실험적 검증**: 실제 웨이퍼 실험으로 저도즈 EUV 방법론 유효성 확인

## 알고리즘/수식
### 저도즈 EUV 최적화 프레임워크
```
EUV 처리량:
  Throughput ∝ 1 / Dose_required
  저도즈 목표: Dose_required 최소화

저도즈 문제:
  광자 수 감소 → 샷 노이즈 증가 → LCDU↑, LWR↑
  Σ_photon ∝ Dose × λ / E_photon

설계-마스크 공동 최적화:
  min_{Design, Mask} Dose_required
  subject to:
    CD_uniformity ≤ CD_budget
    LWR ≤ LWR_budget
    EPE ≤ EPE_budget

마스크 최적화:
  NILS 최대화 → 이미지 대비 향상
  → 낮은 도즈에서도 안정적 CD 달성
```

### 저도즈 EUV 메트릭
- **LCDU**: 로컬 CD 균일성 (저도즈에서 악화)
- **LWR**: 선폭 거칠기 (저도즈에서 증가)
- **EL**: 노출 위도 (저도즈에서 감소)
- **Stochastic fail rate**: 확률론적 고장률 (저도즈에서 급증)

## OPC 툴 SMO 구현 관련성
- EUV SMO 비용 함수에 도즈 감소 목표 통합 가능성
- 저도즈 조건에서 NILS 최대화를 SMO 목표로 설정하는 방법론
- 설계-마스크 공동 최적화: DTCO 관점에서의 SMO 확장
- SKOPC의 EUV OPC 모듈에서 저도즈 모드 지원 시 비용 함수 조정 방향

## 태그
`SMO`, `OPC`, `EUV`, `low_dose`, `throughput`, `LCDU`, `LWR`, `DTCO`, `design_mask_coopt`, `imec`, `SPIE`
