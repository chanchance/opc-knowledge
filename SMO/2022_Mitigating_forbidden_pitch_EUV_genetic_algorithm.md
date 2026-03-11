# Mitigating the Forbidden Pitch of Extreme Ultraviolet Lithography Using Mask Optimization Based on Genetic Algorithm

## 메타데이터
- **저자**: (JMNM 2022, 상세 저자 정보)
- **연도**: 2022
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 21, Issue 4, 043204
- **DOI/URL**: https://doi.org/10.1117/1.JMM.21.4.043204

## 핵심 요약
EUV 리소그래피의 금지 피치(forbidden pitch) 문제를 유전 알고리즘(GA) 기반 마스크 최적화로 완화하는 방법을 제안한다. 엄격한 시뮬레이션과 소스-마스크 최적화(SMO) 관점에서 금지 피치 효과를 분석하고 그 완화 전략을 제시한다.

## 주요 기여
1. **금지 피치 분석**: EUV 리소그래피에서 금지 피치의 엄격한 시뮬레이션 기반 분석
2. **GA 마스크 최적화**: 유전 알고리즘으로 금지 피치 조건에서 마스크 패턴 최적화
3. **SMO 관점 통합**: 소스-마스크 공동 최적화 프레임워크에서 금지 피치 완화 전략
4. **실용적 해결책**: 금지 피치 조건의 이미징 성능 향상을 위한 실용적 마스크 설계

## 알고리즘/수식
### 금지 피치 정의
```
금지 피치(Forbidden Pitch):
  특정 피치에서 이미지 대비가 국소 최솟값을 보이는 피치
  원인: 조명 소스 형상과 마스크 회절 패턴의 상호작용

EUV 금지 피치 조건:
  f_pitch = 1/pitch
  금지 피치: |f_0 ± f_pitch| ≈ NA/λ (동공 가장자리 근처)
  → 회절 차수가 동공 경계에서 에너지 손실
```

### GA 기반 마스크 최적화
```
유전 알고리즘 프레임워크:
- 염색체(chromosome): 마스크 패턴 인코딩
- 적합도 함수(fitness): NILS 또는 PW 최대화
- 교차(crossover): 마스크 세그먼트 교환
- 돌연변이(mutation): 마스크 픽셀 무작위 변경
- 선택(selection): 상위 적합도 개체 생존

비용 함수:
max NILS(pitch_forbidden) subject to:
  CD_error ≤ CD_budget
  MEEF ≤ MEEF_max
  MRC 만족 (Mask Rule Check)
```

### SMO와의 통합
- 소스 형상을 금지 피치에 최적화 + 마스크 GA 최적화 동시 수행
- 교번 최적화: 소스 최적화 → 마스크 GA → 소스 재최적화

## OPC 툴 SMO 구현 관련성
- EUV SMO에서 금지 피치 조건 자동 감지 및 처리 필요
- GA 기반 마스크 최적화: 기울기 없는(gradient-free) 최적화의 EUV 적용 사례
- 소스 최적화와 GA 마스크 최적화의 결합 아키텍처 참조
- SKOPC에서 금지 피치 패턴을 SMO 비용 함수에서 가중치 강화 처리

## 태그
`SMO`, `EUV`, `forbidden_pitch`, `genetic_algorithm`, `mask_optimization`, `NILS`, `process_window`, `JMNM`, `SPIE`
