# Efficient ILT via Multi-level Lithography Simulation

## 메타데이터
- **저자**: Shuyuan Sun, Fan Yang, Bei Yu, Li Shang, Xuan Zeng
- **연도**: 2023
- **게재지/학회**: 60th ACM/IEEE Design Automation Conference (DAC 2023)
- **DOI/URL**: https://dl.acm.org/doi/10.1145/3489517.3530460
- **기관**: CUHK, 복단대학교 (Fudan University)

## 핵심 요약
Multi-level ILT는 다중 해상도 리소그래피 시뮬레이션을 활용한 효율적인 역리소그래피 최적화 프레임워크다. 대형 스케일 팩터에서 소형 스케일 팩터로 점진적으로 해상도를 높이는 멀티레벨 접근법을 통해 ILT 수렴 속도와 최적화 품질을 동시에 향상시킨다. ICCAD 2013 경진대회 벤치마크에서 최신 SOTA 대비 최소 33.8% L2 손실 감소, 15.5% PVBand 감소를 달성한다.

## 주요 기여
- **멀티레벨 시뮬레이션 전략**: 저해상도 → 고해상도 점진적 ILT 최적화로 수렴 가속
- **계층적 초기화**: 저해상도에서 얻은 마스크를 고해상도 최적화의 초기값으로 활용
- **계산 효율성**: 초기 반복에서 저해상도 시뮬레이션으로 계산 비용 절감
- **ICCAD 2013 벤치마크 SOTA**: L2 loss 33.8%↓, PVBand 15.5%↓

## Recipe/Process Flow 상세

### Multi-level ILT 파이프라인

```
입력:
  설계 타겟 레이아웃 (Target Pattern)
        ↓
[Level 1: 저해상도 시뮬레이션]
  - 스케일 팩터 S1 (큰 값, 저해상도)
  - 빠른 Hopkins/SOCS 근사
  - 초기 마스크 최적화 (대략적 형태)
  - 수렴 기준 완화 → 빠른 반복
        ↓
[Level 2: 중간 해상도 시뮬레이션]
  - 스케일 팩터 S2 (S1 < S2)
  - Level 1 마스크를 초기값으로 사용 (업스케일링)
  - 더 세밀한 최적화
  - 중간 수렴 기준
        ↓
[Level K: 고해상도 시뮬레이션 (최종)]
  - 스케일 팩터 SK = 1 (원본 해상도)
  - Level K-1 마스크를 초기값으로 사용
  - 정밀 ILT 최적화
  - 엄격한 수렴 기준 (EPE < 허용치)
        ↓
최종 최적화된 마스크 출력
```

### 멀티레벨 시뮬레이션 수학적 프레임워크

```
전통 ILT 목적함수:
  min_{m} L(m) = ||z(m) - z_target||² + λ·R(m)

여기서:
  z(m): 마스크 m의 리소그래피 시뮬레이션 결과
  z_target: 목표 레지스트 윤곽
  R(m): 마스크 복잡도 정규화 항

멀티레벨 ILT 목적함수 (레벨 l):
  min_{m_l} L_l(m_l) = ||z_l(m_l) - z_target_l||² + λ·R(m_l)

여기서:
  z_l: 스케일 팩터 s_l에서의 저해상도 시뮬레이션
  z_target_l: 타겟을 스케일 s_l로 다운샘플링한 버전
  m_{l+1} 초기값 = Upsample(m_l^*)

멀티레벨 스케일 팩터 시퀀스:
  s_1 > s_2 > ... > s_K = 1
  (큰 s: 저해상도, 빠른 수렴 / 작은 s: 고해상도, 정밀 최적화)
```

### 저해상도 시뮬레이션 구현

```
각 레벨 l에서의 리소그래피 시뮬레이션:

[공중 이미지 계산 (스케일 s_l)]
  ┌─────────────────────────────────────────┐
  │ Hopkins 모델 (다운샘플드 커널)           │
  │   K_l(f) = K(f·s_l)  [주파수 영역]     │
  │                                         │
  │ 공중 이미지:                             │
  │   AI_l(x) = |F^{-1}{K_l·M_l(f)}|²     │
  │                                         │
  │ 여기서 M_l: 스케일된 마스크 푸리에 변환  │
  └─────────────────────────────────────────┘
          ↓
[레지스트 모델 적용]
  임계값 슬라이싱:
    z_l(x) = sigmoid((AI_l(x) - t_r) / σ)

[손실 계산 및 역전파]
  ∂L_l/∂m_l = (∂z_l/∂AI_l)·(∂AI_l/∂m_l)
```

### 레벨 간 마스크 전달 (업스케일링)

```
Level l → Level l+1 마스크 전달:

m_{l+1}^{init} = Upsample(m_l^*, s_{l+1}/s_l)

업스케일링 방법:
  1. 이중선형 보간 (Bilinear interpolation)
  2. 바이큐빅 보간 (Bicubic interpolation) - 권장
  3. 이진화 후 거리 변환 기반 리샘플링

마스크 이진화 보정:
  m_{l+1}^{init} = clip(m_{l+1}^{init}, [0, 1])
  → 연속 마스크값으로 최적화 시작
  → 최종 레벨에서만 이진화 (binarization penalty 적용)
```

### 최적화 알고리즘 상세

```
각 레벨 l에서의 최적화:

알고리즘: Adam / L-BFGS 선택 가능
  - Level 1~K-1: Adam (빠른 수렴, 탐색)
  - Level K: L-BFGS (정밀 수렴, 활용)

하이퍼파라미터:
  - 학습률: α_l (레벨별 감소: α_1 > α_2 > ... > α_K)
  - 정규화 가중치: λ (마스크 복잡도 패널티)
  - 최대 반복수: N_l (레벨별 설정, 고해상도일수록 증가)

수렴 기준:
  - Level l: ||m_l^{(k+1)} - m_l^{(k)}|| < ε_l
  - 최종 레벨: EPE < τ (사전 정의된 EPE 허용치)
```

### 성능 결과 (ICCAD 2013 벤치마크)

```
비교 기준: 전통 ILT (단일 해상도) 및 기타 SOTA 방법

결과 요약:
┌────────────────────────────────────────────────┐
│ 방법            │ L2 Loss │ PVBand │ 런타임     │
├────────────────────────────────────────────────┤
│ Traditional ILT │ 기준값  │ 기준값 │ 기준값     │
│ SOTA Methods    │ -       │ -      │ -          │
│ Multi-level ILT │ -33.8%  │ -15.5% │ 비교 가능  │
└────────────────────────────────────────────────┘

주요 개선:
  - L2 Loss: 최소 33.8% 감소 (마스크-타겟 픽셀 차이)
  - PVBand: 최소 15.5% 감소 (공정 윈도우 면적 개선)
  - 수렴 안정성: 저해상도 초기화로 local minimum 탈출 용이
```

### 레이아웃 분류 및 레벨 수 결정

```
패턴 복잡도에 따른 레벨 수 결정:

단순 패턴 (1D 라인/스페이스):
  2-level ILT (s_1=4, s_2=1)
  → 빠른 처리 우선

중간 복잡도 (2D 피처, L-shape):
  3-level ILT (s_1=8, s_2=2, s_3=1)
  → 균형적 접근

복잡 패턴 (tight 2D, 고밀도):
  4-level ILT (s_1=16, s_2=4, s_3=2, s_4=1)
  → 최고 품질 우선
```

## OPC 툴 구현 관련성
Multi-level ILT는 SKOPC의 ILT 모듈 성능 향상에 직접 적용 가능:
- **LithoEngine 멀티스케일**: `litho_engine.py`에 다중 해상도 Hopkins 커널 구현으로 SKOPC ILT 가속
- **OpenILT 통합**: OpenILT 프레임워크의 수치 ILT에 멀티레벨 전략을 플러그인으로 추가
- **GNN-OPC 초기화**: GNN-OPC 결과를 멀티레벨 ILT의 고해상도 레벨 초기값으로 활용 (하이브리드)
- **PVBand 최적화**: SKOPC PWO 모듈의 PVBand 계산 시 멀티레벨 접근으로 공정 윈도우 품질 개선
- **DAC 2023 레퍼런스**: SKOPC 논문 작성 시 멀티레벨 시뮬레이션 기반 ILT 비교 기준점

## 참고문헌 (핵심)
- ICCAD 2013 Contest Benchmark - 평가 표준 벤치마크
- Geng et al., "DAMO" (ICCAD 2020) - 비교 대상
- Chen et al., "DevelSet" (ICCAD 2021) - 비교 대상
- Yang et al., "GAN-OPC" (TCAD 2020)
- Chen et al., "Neural-ILT" (ICCAD 2020)
- Zheng et al., "L2O-ILT" (TCAD 2024) - 관련 최적화 언롤링

## 태그
`Multi-level ILT`, `DAC 2023`, `Lithography Simulation`, `Multi-Resolution`, `Inverse Lithography`, `PVBand`, `L2 Loss`, `CUHK`, `Fudan`, `ICCAD 2013 Benchmark`, `Efficient ILT`, `Coarse-to-Fine`, `2023`
