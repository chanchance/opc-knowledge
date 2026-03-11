# Application of CM0 Resist Model to OPC and Verification

## 메타데이터
- **저자**: Tyminski, J. K. et al.
- **연도**: 2006
- **게재지**: Proc. SPIE 6154, Optical Microlithography XIX
- **DOI/URL**: https://doi.org/10.1117/12.656566
- **인용수**: ~30

## 핵심 요약
Compact Model Zero(CM0)라 불리는 물리 기반 레지스트 모델을 OPC 및 OPC 검증에 적용한 결과를 제시한다. CM0는 노광·베이크·현상 단계를 2D 메쉬와 컨투어 이동 방정식으로 순차 풀어 레지스트 CD를 예측한다. CM1 대비 비선형 모델이지만 물리적 해석이 명확하며, 캘리브레이션 후 OPC 툴과 연동 가능함을 실증한다.

## 주요 기여
1. CM0 모델의 OPC 적용 가능성을 최초로 실증
2. 노광(exposure)→PEB→현상(development) 3단계 물리 방정식의 2D 메쉬 구현
3. CM0 vs CM1 정확도 비교: RMS 오차 1 nm 이하 달성
4. OPC 검증(verification) 루프에서 CM0 모델 통합 방법론 제시

## 모델 수식/아키텍처

**노광 단계 (Dill's ABC 모델 기반):**
```
∂M/∂t = -C·I(x,y)·M
```
여기서 M = 광활성 화합물 농도, I = 광강도, C = Dill C 파라미터

**PEB 확산:**
```
∂[H⁺]/∂t = D·∇²[H⁺]
```
여기서 D = 확산계수, [H⁺] = 탈보호 산 농도

**현상 속도 모델 (Mack 모델):**
```
R(M) = Rmax · (a+1)(1-M)^n / (a + (1-M)^n) + Rmin
```
여기서 a = (n+1)/(n-1)·(1-Mth)^n, Mth = 현상 임계 농도

**컨투어 이동 (level-set):**
```
∂φ/∂t + R(M)|∇φ| = 0
```

## 모델 유형
- [ ] 광학 모델
- [x] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- CM0는 Calibre OPC 툴의 물리 기반 레지스트 모델 옵션으로 통합 가능
- 2D 메쉬 기반이므로 계산 비용이 크나, 비선형 OPC 효과(resist profile, top-loss) 정밀 예측 가능
- skopc/modeling/compact_model/ 구현 시 CM0 수식 참조 가능
- CM1 대비 캘리브레이션 파라미터: Dill A/B/C, PEB 확산계수 D, Mack n/Mth/Rmax/Rmin

## 참고문헌
- Mack, C.A., "PROLITH: A Comprehensive Optical Lithography Model" (1985)
- Cobb, N., "Variable Threshold Resist Models" (1999)
- Mentor Graphics Calibre CM1 documentation

## 태그
`Model`, `SPIE`, `ResistModel`, `CM0`, `PhysicalModel`, `OPC`, `Calibration`, `2006`
