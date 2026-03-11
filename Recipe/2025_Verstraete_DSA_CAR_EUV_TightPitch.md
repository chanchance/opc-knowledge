# Enabling Chemically Amplified Resists towards Tight Pitch EUV Patterning by Directed Self-Assembly

## 메타데이터
- **저자**: Lander Verstraete, Rémi Vallat, Julie Van Bel, Min-Gi Jo, Philippe Bézard, Hyo Seon Suh
- **연도**: 2025
- **게재지**: Proc. SPIE 13427, Novel Patterning Technologies 2025, 134270D
- **DOI/URL**: https://doi.org/10.1117/12.3051663

## 핵심 요약
지향성 자기조립(DSA)을 화학증폭 레지스트(CAR)와 결합하여 타이트 피치 EUV 리소그래피 패터닝의 효과를 향상시키는 방법을 제시한다. DSA는 EUV CAR 패턴의 에지 거칠기와 공정 창을 개선하는 정류(rectification) 기능을 수행한다. 24nm 피치 라인/스페이스에서 SiCN/비정질 탄소 이중층 언더레이어가 라인 위글링(wiggling) 최소화에 최적임을 확인하고, 30nm 피치 PS-b-PMMA 헥사고날 컨택홀 패턴에서 두꺼운 BCP 필름이 패턴 배치 정확도 향상에 효과적임을 보인다.

## 주요 기여
1. **DSA-CAR 통합 EUV 패터닝**: CAR 레지스트 패턴 위에 DSA를 적용하는 이중 단계 패터닝 전략
2. **24nm L/S 라인 위글링 최소화**: SiCN/비정질 탄소 이중층 언더레이어로 DSA 라인 위글링 억제
3. **30nm 컨택홀 배치 정확도 향상**: 두꺼운 BCP 필름으로 헥사고날 컨택홀 패턴의 배치 정밀도 향상
4. **EUV CAR 한계 극복**: 광자 수 제한(photon-limited) EUV에서 CAR의 stochastic 노이즈를 DSA로 완화
5. **imec 공정 라인 실증**: imec의 DSA 공정 라인에서 EUV + DSA 통합 실증

## Recipe/Flow 상세
- **DSA-EUV 통합 타이트 피치 패터닝 플로우**:
  1. **EUV CAR 리소그래피**:
     - EUV 노광: 화학증폭 레지스트(CAR) 사용
     - 타이트 피치(24nm, 30nm) 패턴의 EUV stochastic 결함 발생
     - CAR LWR/LER 특성화: 개선 필요 수준 파악
  2. **DSA 언더레이어 최적화**:
     - 24nm L/S 패턴 언더레이어 비교: SiO₂, Si, SiCN, 비정질 탄소 등
     - SiCN/비정질 탄소 이중층: 라인 위글링 최소화에 최적 확인
     - 언더레이어 두께 및 표면 에너지 최적화
  3. **BCP 필름 최적화**:
     - PS-b-PMMA 블록 공중합체(BCP) 필름 두께 최적화
     - 두꺼운 BCP 필름 → 30nm 컨택홀 패턴 배치 정확도 향상
     - 분자량, 블록 비율, 어닐링 조건 최적화
  4. **DSA 정류(Rectification)**:
     - CAR 정의 가이드 위에 BCP 자기 조립
     - BCP의 도메인이 CAR 가이드에 정렬: 피치 분할 또는 에지 개선
     - DSA가 CAR의 LWR 거칠기를 평활화(rectification)
  5. **패터닝 성능 평가**:
     - DSA 적용 전후 LWR/LER 비교 측정
     - 컨택홀 배치 정확도(CDU, 위치 오차) 측정
     - EUV 도즈 감소 가능성: DSA 정류로 stochastic 보완
- **DSA 정류의 OPC 영향**:
  - EUV 도즈 2배 감소 가능: DSA가 stochastic 결함 보완
  - LWR 개선: DSA 자기조립이 에지 거칠기 평활화
  - 공정 창 확장: DSA 정류로 오버레이 공정 창 2.5 nm → 4.0 nm
- **소속 기관**: imec (벨기에) + Seoul National University of Science and Technology (대한민국)

## OPC 툴 구현 관련성
- SKOPC DSA-EUV 통합 패터닝 모델 지원
- DSA 정류 효과를 OPC 시뮬레이션 모델에 통합: CAR 후 DSA 처리 효과 예측
- EUV 도즈 최적화: DSA 사용 시 낮은 도즈 OPC 레시피 설계 가이드
- stochastic 결함 감소 전략: DSA + stochastic-aware OPC 공동 최적화 기준

## 태그
`DSA`, `DirectedSelfAssembly`, `CAR`, `EUV`, `TightPitch`, `Rectification`, `BlockCopolymer`, `LWR`, `Stochastic`, `OPC`, `imec`, `SPIE`, `2025`
