# Universal Process Modeling with VTRE for OPC

## 메타데이터
- **저자**: Cobb, N. et al. (Mentor Graphics)
- **연도**: 2002
- **게재지**: Proc. SPIE 4691, Optical Microlithography XV
- **DOI/URL**: https://doi.org/10.1117/12.474587
- **인용수**: ~120

## 핵심 요약
VTR(Variable Threshold Resist) 모델을 확장한 VTRE(VTR-Enhanced)의 OPC 적용 방법론을 제시한다. Cobb & Zakhor(1999)가 제안한 원래 VTR 모델에 추가 이미지 특징 함수를 도입하여 2D 패턴 및 다양한 NA/sigma 조건에서의 예측 정확도를 향상시킨다. 365nm 조명에서의 실증 결과와 함께 전용 OPC 생산 흐름(production flow)에서의 적용 사례를 제시한다.

## 주요 기여
1. VTR → VTRE 확장: 추가 공중상 특징 함수로 2D 정확도 향상
2. VT-5 모델: 5개 파라미터 기반 단순화된 캘리브레이션 버전
3. 다양한 NA/sigma 조건에 대한 모델 이식성(portability) 입증
4. 실제 OPC 생산 흐름에서의 VTRE 적용 사례 (365nm)
5. EPE를 공중상 특성의 함수로 모델링하는 범용 프레임워크

## 모델 수식/아키텍처

**VTR 기본 모델 (Cobb 1999):**
```
EPE(edge) = f(I_peak, S_edge)
```
I_peak = 피크 광강도, S_edge = 엣지에서의 강도 기울기(slope)

**VTRE 확장 모델:**
```
EPE = c₀ + c₁·I_peak + c₂·S_edge + c₃·(1/S_edge) + c₄·I_min + c₅·ΔI
```
여기서:
- c₀~c₅ = 캘리브레이션 계수
- I_min = 스페이스 내 최소 강도
- ΔI = I_peak - I_min (contrast)

**VT-5 모델 (5파라미터):**
```
T_eff(x) = T_nom + α·(I_peak(x) - I_ref) + β·(S(x) - S_ref)
            + γ·ΔI(x) + δ·Curv(x) + ε·Load(x)
```
T_eff = 유효 현상 임계값 (위치 의존)
Load(x) = 장거리 로딩 항 (Gaussian 가중 적분)

**캘리브레이션 절차:**
```
1. 다양한 pitch/CD/orientation 패턴 노광
2. CD-SEM으로 실측 CD 수집
3. 시뮬레이션 CD 계산 (SOCS 기반 공중상)
4. 최소자승법으로 c₀~c₅ 피팅:
   min_c ||CD_meas - CD_sim(c)||²
```

## 모델 유형
- [x] 광학 모델 (공중상 특징 기반)
- [x] 레지스트 모델 (유효 임계값 모델)
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- VTRE/VT-5는 skopc의 Variable Threshold Resist 모델 구현 직접 참조
- 계산 효율 높음: SOCS 커널 컨볼루션 + 선형 파라미터 피팅
- EPE 예측 파이프라인: 마스크 → 공중상(SOCS) → VTRE 보정 → CD 예측
- 로딩 항은 수백nm 범위 Gaussian 커널로 구현
- CM1과 함께 현대 컴팩트 레지스트 모델의 양대 축

## 참고문헌
- Cobb, N., Zakhor, A., "Variable Threshold Resist Models for Lithography Simulation" (1999)
- Mack, C.A., "Lumped Parameter Model" (2004)
- Mentor Graphics VTR/VTRE documentation

## 태그
`Model`, `SPIE`, `VTR`, `VTRE`, `CompactModel`, `ResistModel`, `OPC`, `Calibration`, `EPE`, `2002`
