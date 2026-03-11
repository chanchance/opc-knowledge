# Study of Mask Error Enhancement Factor Improvement with Low-n Absorber Extreme Ultraviolet Lithography Mask

## 메타데이터
- **저자**: (JMM 저자 정보)
- **연도**: 2024
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology (JMM), Vol. 23, Issue 4, 044401
- **DOI/URL**: https://doi.org/10.1117/1.JMM.23.4.044401

## 핵심 요약
저굴절률(low-n) 흡수층 EUV 마스크가 마스크 오차 증폭 계수(MEEF, Mask Error Enhancement Factor)를 개선하는 원리와 효과를 분석한다. 저-k1 이미징에서 EUV 마스크의 CD 변동이 웨이퍼에서 증폭되는 MEEF 문제를, 흡수층의 굴절률(n)과 소광 계수(k)를 최적화하여 NILS 향상과 함께 MEEF를 감소시킨다.

## 주요 기여
1. **Low-n MEEF 개선 메커니즘 분석**: 흡수층 광학 상수(n, k)가 MEEF에 미치는 영향 정량화
2. **NILS-MEEF 연관성**: NILS 향상이 MEEF 감소로 이어지는 원리 분석
3. **흡수층 최적화**: MEEF 최소화를 위한 최적 (n, k) 범위 도출
4. **실험적 검증**: 0.33NA EUV에서 low-n 마스크 MEEF 실측 비교

## 알고리즘/수식
### MEEF 정의 및 low-n 개선 원리
```
MEEF 정의:
  MEEF = ΔCD_wafer / (ΔCD_mask / M)
  여기서 M: 마스크 배율 (EUV: 4x)
  MEEF > 1: 마스크 CD 오차가 웨이퍼에서 증폭

MEEF와 NILS의 관계:
  MEEF ≈ 1 / NILS (근사)
  NILS ↑ → MEEF ↓

Low-n 흡수층 MEEF 개선:
  n < n_TaBN → 위상 이동 감소 → NILS ↑
  MEEF(low-n) < MEEF(TaBN)

흡수층 (n, k) 최적화:
  min_{n, k} MEEF(n, k)
  = max_{n, k} NILS(n, k)
  subject to: 흡수율 ≥ 흡수율_min, MRC 충족
```

### 실험 설계
```
비교 마스크:
  - TaBN 기준 마스크 (n ≈ 0.94, k ≈ 0.04)
  - Low-n 마스크 (n < 0.85 영역)

측정 피치: 28nm ~ 40nm LS 패턴 (0.33NA EUV)
측정 메트릭: MEEF, NILS, EL, DOF
```

## OPC 툴 SMO 구현 관련성
- MEEF 인식 SMO: SMO 비용 함수에 MEEF 항 추가 (MEEF 최소화 목표)
- Low-n 마스크 OPC 모델: 흡수층 (n, k)에 따른 MEEF 차이 반영 OPC 모델
- 마스크 CD 변동 허용치: MEEF 기반 마스크 CD 예산 할당
- SKOPC EUV OPC 모듈: low-n 마스크 타입별 MEEF 파라미터 데이터베이스

## 태그
`MEEF`, `EUV`, `low_n`, `mask_absorber`, `NILS`, `OPC`, `SMO`, `CD_uniformity`, `0p33NA`, `JMM`, `2024`
