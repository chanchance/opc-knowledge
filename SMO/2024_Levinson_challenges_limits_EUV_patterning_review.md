# Challenges and Limits to Patterning Using Extreme Ultraviolet Lithography

## 메타데이터
- **저자**: Harry J. Levinson
- **연도**: 2024
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology (JMM), Vol. 24, Issue 1, 011005 (29 October 2024)
- **DOI/URL**: https://doi.org/10.1117/1.JMM.24.1.011005

## 핵심 요약
EUV 리소그래피를 이용한 패터닝의 도전과 한계를 종합적으로 검토하는 리뷰 논문이다. 레지스트 아키텍처, 분자 빌딩 블록 한계, 수차, 확률론적 효과 등 EUV 패터닝의 근본적 물리적 제약을 분석하고, 고NA EUV 시대를 위한 기술 요구사항을 정리한다.

## 주요 기여
1. **EUV 패터닝 한계 종합 리뷰**: 물리적 근본 제약부터 실용적 도전까지 체계적 정리
2. **레지스트 아키텍처 요구사항**: 10nm 이하 하프 피치에서 필요한 새로운 레지스트 설계
3. **분자 빌딩 블록 한계**: 금속 산화물 클러스터 크기가 패터닝 해상도에 미치는 한계
4. **수차 요구사항**: EUV에서 수차 수준과 패터닝 성능의 관계 정량화

## 알고리즘/수식
### EUV 패터닝 근본 한계
```
해상도 한계:
  CD_min = k1 × λ / NA
  k1_min ≈ 0.18 (하이퍼NA 하한)
  → 최소 하프 피치 = 0.18 × 13.5nm / 0.75 ≈ 3.2nm (하이퍼NA)

레지스트 분자 한계:
  금속 산화물 클러스터 중심 간격 ≈ 1.8nm
  ≈ 고NA EUV 목표 최소 ½피치(8nm)의 22%
  LER 요구사항 (IRDS 2028): ≤ 0.8nm

수차 요구사항:
  0.23nm 수차 = 17 milliwaves (EUV)
  → 광학 리소그래피 대비 높은 수차 수준 (동일 밀리웨이브 기준)
  → SMO로 수차 영향 부분 보상 필요

확률론적 한계:
  광자 수: N_photon ∝ Dose × λ / E_photon
  EUV λ=13.5nm → 광자 에너지 높음 → 광자 수 적음
  → 샷 노이즈 기반 LER, LCDU 한계
```

### SMO/OPC와 관련한 함의
```
수차 보상 SMO:
  수차 영향: ΔCD_aberr(W_k, pitch, orientation)
  SMO로 수차 민감도 감소 가능
  → but 근본적 한계 (파면 오차 자체는 SMO로 수정 불가)

확률론적 인식 OPC:
  P_fail ≥ P_fail_floor (물리적 하한 존재)
  → OPC 최적화로 P_fail_floor 이상은 개선 가능
  → but 도즈/레지스트 물리 한계로 하한 존재
```

## OPC 툴 SMO 구현 관련성
- EUV 패터닝 한계 인식: SKOPC SMO/OPC 성능 목표 설정의 현실적 기준
- 수차 보상 SMO 필요성: 17 milliwaves 수차 보상을 위한 SMO 기능 정당성
- 확률론적 OPC 한계: stochastic OPC의 물리적 하한 인식과 비용 함수 설계
- 레지스트 모델 연계: 분자 수준 레지스트 한계를 OPC 모델 정확도 기준으로 반영

## 태그
`EUV`, `review`, `challenges`, `limits`, `resist`, `stochastic`, `aberration`, `high_NA`, `LER`, `LCDU`, `Levinson`, `JMM`, `2024`
