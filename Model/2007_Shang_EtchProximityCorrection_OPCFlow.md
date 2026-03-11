# Etch Proximity Correction by Integrated Model-Based Retargeting and OPC Flow

## 메타데이터
- **저자**: Shang, S., Granik, Y., Niehoff, M. (Mentor Graphics)
- **연도**: 2007
- **게재지**: Proc. SPIE 6730, Photomask Technology 2007
- **DOI/URL**: https://doi.org/10.1117/12.746773
- **인용수**: ~70

## 핵심 요약
에칭 근접 효과(etch proximity effect)를 OPC 플로우에 통합하기 위해 에칭 모델과 광학/레지스트 모델을 분리하여 순차적으로 적용하는 새로운 모델 기반 리타겟팅(retargeting) 방법론을 제안한다. 에칭 및 광학/레지스트 공정 효과를 모델 캘리브레이션과 레이아웃 보정 단계에서 분리함으로써 에칭·레지스트 타겟 제어가 용이해지고 OPC 런타임이 크게 단축된다.

## 주요 기여
1. 에칭 OPC와 리소 OPC의 분리(decoupled) 플로우 제안: 런타임 대폭 절감
2. 에칭 근접 효과와 광학/레지스트 효과의 독립적 모델 캘리브레이션 방법론
3. 에칭 리타겟팅 → 리소 OPC 순차 적용으로 두 효과의 독립 제어 가능
4. 실제 크리티컬 레이어 적용 시 OPC 정확도 유지하면서 런타임 감소 실증
5. 에칭 바이어스의 패턴 밀도·피치 의존성 분리 모델링 방법

## 모델 수식/아키텍처

**분리된 OPC 플로우:**
```
Step 1: Etch Retargeting
  CD_litho_target = CD_wafer_target - Etch_Bias_Model(layout_context)

Step 2: Litho OPC
  mask_CD = Litho_OPC(CD_litho_target, optical_model, resist_model)
```

**에칭 바이어스 모델:**
```
Etch_Bias(x) = Σ_k c_k · K_k(local_density(x), pitch(x), orientation(x))
```
K_k = 기하학적 커널 (밀도, 피치, 방향 의존 특성 함수)

**기존 통합 OPC (비교 기준):**
```
mask_CD = OPC(CD_wafer_target, optical+resist+etch combined model)
```
→ 에칭과 리소 효과 결합 → 캘리브레이션/디버깅 어려움

**런타임 비교:**
```
Runtime_integrated: O(N_iter × N_gauges × (litho + etch))
Runtime_separated: O(N_etch_iter × N_gauges × etch)
                  + O(N_litho_iter × N_gauges × litho)
→ 분리 방식: ~3-5× 런타임 절감 (에칭 반복 횟수 감소)
```

**모델 정확도 메트릭:**
```
RMS_etch = sqrt(mean((CD_etch_sim - CD_etch_meas)²))
RMS_litho = sqrt(mean((CD_litho_sim - CD_litho_meas)²))
RMS_total = sqrt(RMS_etch² + RMS_litho²)
```

## 모델 유형
- [ ] 광학 모델
- [ ] 레지스트 모델
- [ ] ML/DL
- [x] 하이브리드 (에칭 컴팩트 모델 + 리소 OPC 모델)

## OPC 툴 구현 관련성
- skopc OPC 플로우: 에칭 리타겟팅 단계를 리소 OPC 앞에 전처리로 추가
- 에칭 모델 캘리브레이션: 리소 후 CD + 에칭 후 CD 동시 측정 필요
- 분리 플로우의 장점: 에칭 공정 변경 시 에칭 모델만 재캘리브레이션
- Calibre OPC의 기본 에칭 보정 플로우 구조와 일치
- 28nm 이하 크리티컬 레이어(게이트, 메탈1)에서 필수 적용

## 참고문헌
- Lafferty, N. et al., "Etch kernels for etch bias prediction" (2018)
- Sato, T. et al., "Deep-learning based etch model" (2022)
- Mentor Graphics Calibre etch bias documentation

## 태그
`Model`, `SPIE`, `EtchModel`, `EtchProximity`, `Retargeting`, `OPCFlow`, `Calibration`, `2007`
