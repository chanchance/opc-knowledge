# Variable-Threshold Resist Models for Lithography Simulation

## 메타데이터
- **저자**: Neal B. Cobb, Avideh Zakhor
- **연도**: 1999
- **게재지/학회**: SPIE Optical Microlithography XII, Vol. 3679
- **DOI/URL**: https://doi.org/10.1117/12.354329
- **인용수**: 200+

## 핵심 요약
OPC 모델 보정에서 가장 널리 사용되는 Variable Threshold Resist Model (VTRM)을 정식화한 선구적 논문. 고정 임계값(constant threshold) 대신 이미지 강도 피크값과 기울기(slope)의 함수로 임계값을 변화시켜 레지스트 비선형 거동을 재현한다. 단순한 수식 구조와 빠른 계산 속도로 인해 현재까지 산업계 full-chip OPC 보정에 표준적으로 사용된다. 이후 VT-5, VTRE 등으로 발전하는 모델 계보의 시작점이다.

## 주요 기여
- Variable Threshold Resist Model (VTRM) 공식 제안 및 검증
- EPE를 이미지 피크 강도 및 이미지 기울기의 함수로 모델링
- 365nm 노광에서 광범위한 패턴에 대한 실험적 검증
- 파라미터 수가 적고 보정이 용이한 compact 모델 구조 확립

## 모델 아키텍처/수식
VTRM의 핵심 수식:

```
T(x) = a · Ipeak(x) + b · slope(x) + c
```

여기서:
- T(x): 위치 x에서의 가변 임계값
- Ipeak(x): 피처 엣지 근방의 이미지 강도 최댓값
- slope(x): 엣지 위치에서의 이미지 강도 기울기 (normalized image log slope, NILS)
- a, b, c: 보정 파라미터 (CD-SEM 측정값으로 fitting)

CD 예측:
```
CD = CD_aerial(T) = {x : I(x) = T(x)}
```

EPE = (CD_measured - CD_simulated) / 2

보정 절차:
1. 다양한 패턴(CD, pitch 조합)에 대해 CD-SEM 측정
2. 광학 모델로 aerial image 계산
3. (a, b, c) 파라미터를 최소제곱법으로 fitting
4. RMS EPE 최소화

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [ ] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 `skopc/modeling/` 내 레지스트 모델 구현의 핵심 레퍼런스. VTRM은 `ResistModel` 클래스의 기본 구현체로 사용 가능하며, 파라미터 (a, b, c) 보정 루틴을 least-squares 최적화로 구현. `rule_opc.py`에서 간단한 1D 패턴 보정 시 이 모델이 효과적. TorchResist 라이브러리의 sigmoid 기반 모델과 비교 검토 필요.

## 참고문헌 (핵심)
- Cobb, N. and Zakhor, A., "Fast sparse aerial image calculations for OPC," SPIE 2621 (1995)
- Brunner, T.A., "Approximate models for resist processing effects," SPIE 2726 (1996)
- Mack, C., "Analytical expression for the standing wave intensity in photoresist," Appl. Opt. 25(12), 1986
- Granik, Y. et al., "VTRE: Universal process modeling with for OPC," SPIE (2003)

## 태그
`Model`, `OPC`, `ResistModel`, `VTR`, `VTRM`, `Calibration`, `Threshold`, `EPE`, `CompactModel`, `CriticalDimension`
