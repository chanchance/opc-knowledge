# Wavefront-Based Pixel Inversion Algorithm for Generation of Subresolution Assist Features

## 메타데이터
- **저자**: Jue-Chin Yu, Peichen Yu, Hsueh-Yung Chao
- **연도**: 2011
- **게재지**: Journal of Micro/Nanolithography, MEMS, and MOEMS (JM3), Vol. 10, Issue 4, 043014
- **DOI/URL**: https://doi.org/10.1117/1.3663249
- **인용수**: ~50

## 핵심 요약
역리소그래피 기술(ILT)을 이용한 SRAF 생성은 방대한 계산 자원을 요구하여 첨단 CMOS 노드에서의 배포를 제한한다. 본 논문은 파면 기반 픽셀 반전(wavefront-based pixel inversion) 알고리즘으로 높은 항공 이미지 품질을 가진 역 마스크를 빠르게 획득하고, 유연한 패턴 단순화 기법으로 효과적인 SRAF를 생성하는 방법을 제안한다. 생성된 SRAF는 기존 마스크 보정 흐름 전에 삽입되어 주 패턴과 SRAF를 동시에 최적화한다.

## 주요 기여
1. 파면 전파 기반 빠른 픽셀 반전 알고리즘 (ILT 대비 계산 효율)
2. 높은 항공 이미지 품질 역 마스크 신속 획득
3. 유연한 패턴 단순화로 효과적 SRAF 생성
4. 기존 마스크 보정 흐름과 통합 가능한 SRAF 전처리 방법

## Recipe/Process Flow 상세

### 파면 기반 픽셀 반전 알고리즘
```
기존 ILT 방식:
  M_opt = argmin ||I(M) - I_target||² + λ||M||
  - 반복적 경사 하강법
  - 많은 이터레이션 필요
  - 높은 계산 비용

파면 기반 픽셀 반전:
파면(wavefront) 개념 적용:
  1. 목표 이미지 I_target에서 역 파면 계산
     Ψ_target = IFFT(√I_target × exp(iφ))
  2. 마스크 초기화
     M_init = sign(Re(Ψ_target))  (이진화)
  3. 픽셀 반전 최적화
     For each pixel p:
       if flip(p) reduces ||I(M) - I_target||²:
         M(p) = 1 - M(p)
  4. 수렴 체크 → 역 마스크 M_opt 획득
```

### SRAF 생성 파이프라인
```
1. 파면 기반 픽셀 반전으로 역 마스크 생성
   - 주 패턴에서 최대 공정 윈도우를 주는 역 마스크 계산
   - 계산 효율적 알고리즘으로 빠른 수렴

2. 패턴 단순화 (Pattern Simplification)
   - 역 마스크의 복잡한 연속 패턴 → SRAF 후보로 단순화
   - 단순화 방법:
     a) 연결 성분 분석으로 고립된 영역 식별
     b) 너무 작거나 비정형 패턴 제거 (MRC 기반)
     c) 남은 패턴 → 직사각형 근사 (Manhattan SRAF)
   - 유연성: 단순화 임계값 조정으로 SRAF 수/복잡도 제어

3. SRAF 삽입 및 기존 OPC 흐름 통합
   - 단순화된 SRAF를 주 패턴에 추가
   - 기존 Model-Based OPC 실행 (주 패턴 + SRAF 포함)
   - 동시 최적화: OPC가 주 패턴과 SRAF 상호작용 고려
```

### 항공 이미지 품질 평가
```
NILS (Normalized Image Log-Slope):
  NILS = CD × d(log I)/dx|_threshold
  → 높을수록 패턴 충실도 및 공정 윈도우 양호

파면 기반 SRAF vs. 기존 방법:
  NILS 개선: 파면 기반 역 마스크 기반 SRAF가 우수
  런타임: ILT 대비 대폭 감소
  SRAF 품질: 비교 가능한 항공 이미지 품질
```

### 파라미터
```
픽셀 격자 크기: 마스크 해상도 결정 (일반적 1-2nm)
픽셀 반전 임계값: 이미지 품질 vs. 수렴 속도 균형
패턴 단순화 임계값: SRAF 수 및 복잡도 제어
MRC 검사: 마스크 규칙 준수 확인
```

## OPC 툴 구현 관련성
- **SKOPC SRAF 생성기**: `skopc/modeling/sraf_generator.py`에 파면 기반 픽셀 반전 알고리즘 통합 가능
- **ILT 대안**: OpenILT 기반 ILT(`skopc/modeling/openilt_adapter.py`)보다 빠른 SRAF 전처리 방법
- **패턴 단순화**: 연속 최적화 결과를 Manhattan SRAF로 변환하는 후처리 참조
- **동시 최적화**: SRAF 삽입 후 OPC 실행으로 주 패턴-SRAF 상호작용 자동 처리

## 참고문헌
- JM3 Vol. 10, Issue 4 (2011)
- 관련: Model-based insertion of assist features using pixel inversion (SPIE 6283, 2006)
- 관련: SRAF rule extraction and insertion based on ILT (SPIE 10961, 2019)
- 관련: Innovative pixel-inversion for MB-SRAF and OPC (SPIE 7274, 2009)

## 태그
`Recipe`, `SPIE`, `JM3`, `SRAF`, `PixelInversion`, `WavefrontBased`, `ILT`, `PatternSimplification`, `AerialImage`, `NILS`, `EfficientAlgorithm`
