# Lithographic Exposure Latitude Aware Source and Mask Optimization

## 메타데이터
- **저자**: Lulu Zou, Lihui Liu, Yiyu Sun, Pengzhi Wei, Miao Yuan, Zhaoxuan Li, Yaning Li, Yanqiu Li
- **연도**: 2021 (출판일: 2021-12-13)
- **게재지**: Proc. SPIE 12073, 10th International Symposium on Advanced Optical Manufacturing and Testing Technologies, 1207302
- **DOI/URL**: https://doi.org/10.1117/12.2604844

## 핵심 요약
노출 위도(Exposure Latitude, EL)를 SMO 비용 함수에 직접 통합하는 ELASMO(Exposure Latitude Aware SMO) 방법을 제안한다. 기존 SMO 대비 EL을 5%에서 11%로 향상시키면서 이미징 충실도를 유지한다. EUV 리소그래피에서 EL 향상은 공정 안정성에 직결된다.

## 주요 기여
1. **ELASMO 방법론**: EL 인식 SMO 비용 함수의 혁신적 패널티 항 도입
2. **EL 2배 이상 향상**: 기존 SMO 5% → ELASMO 11% (동일 이미징 충실도 조건)
3. **공중 이미지 대비도 향상**: EL 향상과 함께 이미지 대비 개선
4. **EUV 적용성**: EUV 리소그래피의 좁은 공정 창 문제 직접 해결

## 알고리즘/수식
### ELASMO 비용 함수
```
Cost_ELASMO = Cost_SMO + λ · Penalty_EL

여기서:
- Cost_SMO: 표준 SMO 비용 함수 (CD 오차, EPE 등)
- λ: EL 패널티 가중치
- Penalty_EL = max(0, EL_target - EL_current)^2
```

### EL 정의
```
EL = (ΔDose / Dose_nominal) × 100%
  = 허용 CD 범위에서의 도즈 변동 허용 범위
```

### 최적화 알고리즘
- 경사 기반(gradient-based) 최적화 프레임워크
- 소스와 마스크를 번갈아 최적화하는 교번 최소화(alternating minimization)
- EL 향상을 위한 새로운 패널티 함수 통합

## OPC 툴 SMO 구현 관련성
- SMO 비용 함수 확장: CD/EPE 외에 EL 항목 추가 필요
- EUV 공정 창 최적화 시 EL 인식 SMO가 표준 접근법이 되어야 함
- SKOPC의 SMO 모듈에서 공정 창(PW) 최적화 시 EL 패널티 항 참조 가능
- defocus 허용성과 EL의 트레이드오프 관리 방법론 제공

## 태그
`SMO`, `EUV`, `exposure_latitude`, `ELASMO`, `process_window`, `cost_function`, `gradient_optimization`, `SPIE`
