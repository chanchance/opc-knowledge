# MEEF-Based Correction to Achieve OPC Convergence of Low-k1 Lithography with Strong OAI

## 메타데이터
- **저자**: Soo-Han Choi, A-Young Je, Ji-Suk Hong, Moon-Hyun Yoo, Jeong-Taek Kong
- **연도**: 2006
- **게재지**: Proc. SPIE 6154, Optical Microlithography XIX, 61540P
- **DOI/URL**: https://doi.org/10.1117/12.656894
- **인용수**: ~30

## 핵심 요약
고 NA 액침 리소그래피에서 강한 OAI(Off-Axis Illumination: 다이폴, 크로스폴)를 사용할 때, 패턴 방향과 형상에 따라 MEEF(Mask Error Enhancement Factor)와 NILS(Normalized Intensity Log-Slope)가 크게 변동하여 OPC 수렴이 발산(divergence)하는 문제를 해결한다. 방향 의존 MEEF를 OPC 댐핑(damping) 파라미터에 반영하여 수렴 안정성을 확보하는 MEEF 기반 보정 방법론을 제시한다.

## 주요 기여
1. 강한 OAI 환경에서 OPC 발산 원인인 방향 의존 MEEF 분석
2. MEEF 분포를 OPC 댐핑 팩터에 반영하는 적응형 수렴 제어
3. 기존 고정 댐핑 값 방식의 OPC 대비 수렴성 대폭 개선
4. 삼성전자 고 NA 액침 공정에서 실증

## Recipe/Process Flow 상세

### 강한 OAI에서의 OPC 수렴 문제
```
표준 OPC 이터레이션 (Newton-Raphson 근사):
  세그먼트 이동 = EPE / MEEF
  MEEF = ΔCD_wafer / ΔCD_mask

고정 댐핑 OPC의 가정:
  MEEF ≈ 상수 (방향/형상 무관)
  → 댐핑 팩터 α = 일정 값 사용

강한 OAI(다이폴, 크로스폴)의 현실:
  수평(H) 패턴: MEEF_H 값
  수직(V) 패턴: MEEF_V 값
  2D 패턴(코너, 끝단): MEEF가 급격히 변화

  MEEF_H ≠ MEEF_V (경우에 따라 2-5배 차이)
  → 고정 댐핑 → H 또는 V 중 하나에서 과보정/미보정
  → 이터레이션이 수렴하지 않고 발산

발산 증상:
  EPE가 이터레이션마다 감소하지 않고 진동
  OPC 결과가 불안정, 재현성 낮음
  수렴 판정 기준 달성 불가
```

### MEEF 기반 적응형 댐핑 알고리즘
```
MEEF 분포 계산:
  1. 리소그래피 시뮬레이션으로 각 세그먼트의 MEEF 계산
     MEEF_seg = d(CD_wafer)/d(CD_mask)|_seg
     방법: 마스크 바이어스 ±δ 적용 후 CD 변화 측정

  2. 세그먼트별 MEEF 매핑:
     dense 패턴 세그먼트 → 낮은 MEEF
     isolated 패턴 세그먼트 → 높은 MEEF
     2D 코너 세그먼트 → MEEF 급변
     OAI 방향 의존 세그먼트 → H vs. V MEEF 차이

적응형 OPC 댐핑:
  표준: 세그먼트 이동 = α × EPE_seg
  MEEF 기반: 세그먼트 이동 = (α / MEEF_seg) × EPE_seg
  또는: 세그먼트 이동 = α × EPE_seg / MEEF_nominal × MEEF_seg

수렴 보장:
  MEEF 큰 세그먼트(민감): 이동 제한 → 진동 방지
  MEEF 작은 세그먼트(둔감): 이동 허용 → 빠른 수렴
  → 전체적으로 안정적 수렴 달성
```

### MEEF 분포와 OAI의 관계
```
다이폴 조명 (Dipole):
  H-pole (수평 쌍극): 수직(V) 패턴에 최적화
    → V 패턴: 낮은 MEEF, 높은 NILS
    → H 패턴: 높은 MEEF, 낮은 NILS (보조 효과)
    → H 패턴 OPC 어려움

  V-pole (수직 쌍극): H 패턴에 최적화
    → 반대 패턴 의존성

크로스폴 조명 (Cross-Pole, 쿼드러폴):
  H/V 패턴 모두 지원
  그러나 2D 패턴(L-자형, T자형)에서 MEEF 불균일
  → 여전히 방향 의존 MEEF 존재

결론:
  강한 OAI 필수적이지만 방향 의존 MEEF 문제 수반
  → MEEF 기반 적응형 댐핑이 핵심 해결책
```

### 성능 결과 (삼성전자 고 NA 액침 공정)
```
기존 고정 댐핑 OPC:
  수렴 이터레이션 수: 발산 또는 매우 많음
  수렴 후 RMS EPE: 높음 또는 불안정

MEEF 기반 적응형 댐핑 OPC:
  수렴 이터레이션 수: 안정적으로 감소
  수렴 후 RMS EPE: 충분히 낮음
  H/V 패턴 균등한 EPE 달성
  2D 패턴(코너, 끝단)에서도 안정적 수렴
```

## OPC 툴 구현 관련성
- **SKOPC 수렴 안정화**: `skopc/modeling/model_opc.py` OPC 이터레이션에 MEEF 의존 댐핑 팩터 추가
- **세그먼트별 MEEF**: 각 세그먼트에 대한 MEEF 계산 후 이동 크기 조절
- **PID 제어와 통합**: Painter(2004) PID 제어기와 결합하여 더 강건한 수렴 제어
- **OAI 레시피**: 강한 다이폴/크로스폴 조명 사용 시 MEEF 기반 댐핑 자동 활성화

## 참고문헌
- Proc. SPIE 6154, Optical Microlithography XIX (2006)
- 저자 소속: Samsung Electronics
- 관련: Classical control theory applied to OPC convergence (SPIE 5377, 2004)
- 관련: Fast Forward OPC 4-iteration convergence (SPIE 2007)
- 관련: Model-based OPC using MEEF matrix II (SPIE 9052, 2014)

## 태그
`Recipe`, `SPIE`, `OPC-Convergence`, `MEEF`, `OAI`, `Dipole`, `AdaptiveDamping`, `NewtonRaphson`, `LowK1`, `Samsung`, `ImmersionLithography`, `2006`
