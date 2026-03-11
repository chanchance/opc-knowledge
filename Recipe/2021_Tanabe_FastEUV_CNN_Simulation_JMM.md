# Fast EUV Lithography Simulation Using Convolutional Neural Network

## 메타데이터
- **저자**: Hiroyoshi Tanabe, Shimpei Sato, Atsushi Takahashi
- **연도**: 2021
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology (JMM), Vol. 20, Issue 4, 041202
- **DOI/URL**: https://www.spiedigitallibrary.org/journals/journal-of-micro-nanopatterning-materials-and-metrology/volume-20/issue-4/041202/
- **인용수**: ~25

## 핵심 요약
CNN(Convolutional Neural Network)으로 EUV 리소그래피 시뮬레이션을 빠르게 수행하는 방법을 제안한다. 특히 리고러스 전자기장(EMF) 시뮬레이션이 필요한 마스크 3D 효과(M3D)의 두꺼운 마스크 모델(thick mask model)에서 T2T CD(Thick-to-Thin CD)를 CNN으로 예측한다. CNN이 왜곡된 회절 진폭을 마스크 패턴 입력에서 직접 예측하여 계산 시간을 크게 단축하면서도 M3D 효과에 민감한 T2T CD를 정확히 예측한다.

## 주요 기여
1. CNN으로 EUV M3D 두꺼운 마스크 모델의 T2T CD 빠른 예측
2. 왜곡 회절 진폭의 직접 CNN 예측 → EMF 시뮬 대체
3. 계산 시간 크게 단축 (리고러스 EMF vs. CNN 추론)
4. iN3 로직 패턴으로 평가하여 실제 노드 적용 가능성 검증

## Recipe/Process Flow 상세

### EUV 마스크 3D 효과와 두꺼운 마스크 모델
```
얇은 마스크 모델 (Thin Mask Approximation):
  마스크 두께 << 파장 → 즉각 투과/반사 가정
  EUV: λ=13.5nm, 흡수체 두께=56~75nm
  → 두께가 파장과 비슷 → 얇은 마스크 가정 부정확

두꺼운 마스크 모델 (Thick Mask / EMF):
  리고러스 전자기장 시뮬: RCWA, FDTD
  3D 마스크 형상 완전 모델링
  T2T CD (Thick-to-Thin CD):
    두꺼운 마스크 시뮬 CD - 얇은 마스크 시뮬 CD
    = M3D 효과에 의한 CD 오차
  특성: 피처 크기, pitch, 방향(H/V)에 크게 의존

리고러스 EMF 시뮬의 문제:
  속도: 매우 느림 (클립당 수 분~수 시간)
  OPC 루프 통합: 비실용적
  → CNN 대리 모델 필요
```

### CNN 기반 EUV 시뮬레이션 모델
```
입력:
  마스크 패턴 이미지 (이진 픽셀)
  공정 조건: 포커스, 도즈 (선택적)
  패턴 특성: CD, pitch 정보

출력 A (회절 진폭 예측):
  왜곡 회절 진폭: ΔA(f) = A_thick(f) - A_thin(f)
  모든 주요 회절 차수에 대한 진폭 예차 예측
  → EMF 시뮬 없이 두꺼운 마스크 효과 계산

출력 B (T2T CD 직접 예측):
  T2T CD = CNN(마스크 패턴) 직접 예측
  → 더 단순한 접근, 빠른 추론

CNN 아키텍처:
  ResNet/VGG 계열 컨볼루션 네트워크
  수용 영역(receptive field): 마스크 3D 효과 범위 포함
  다중 스케일: 다양한 pitch/CD 처리
```

### 훈련 및 검증
```
훈련 데이터:
  리고러스 RCWA 시뮬레이션 결과
  다양한 1D/2D 패턴: 다양한 CD, pitch, 방향
  M3D 민감 패턴 집중 포함

iN3 로직 패턴 평가:
  imec 3nm 노드 로직 메탈/비아 패턴
  OPC 포함 패턴, 커비리니어 비아 패턴 포함
  → 실제 노드 패턴에서 CNN 일반화 검증

평가 지표:
  T2T CD 예측 오차: vs. RCWA 기준
  회절 진폭 오차
  계산 시간 비교: CNN vs. RCWA
```

### 성능 결과
```
T2T CD 예측:
  CNN: RCWA 대비 정확한 T2T CD 예측
  M3D 민감 패턴 (작은 pitch, 복잡 2D): 높은 정확도

계산 속도:
  RCWA: 클립당 수 분
  CNN 추론: ms 단위
  속도 향상: 수천 배 이상

iN3 평가:
  OPC 포함 패턴: 정상 예측 성공
  커비리니어 비아: 커브 형상 M3D 효과도 예측
  → 실제 선진 노드 적용 가능성 확인
```

## OPC 툴 구현 관련성
- **SKOPC EUV M3D 보정**: `skopc/modeling/litho_engine.py`에 CNN T2T CD 예측 통합
- **OPC 루프 M3D 보정**: 각 OPC 이터레이션에서 CNN으로 M3D 보정 CD 빠른 계산
- **패턴 의존 보정**: CNN 예측 T2T CD로 패턴별 M3D 보정 OPC 바이어스 계산
- **커비리니어 지원**: 커비리니어 마스크의 M3D 효과 CNN 예측

## 참고문헌
- JMM, Vol. 20, Issue 4, 041202 (2021)
- 저자 소속: Tokyo Tech (Atsushi Takahashi 그룹)
- 관련: Accurate prediction of EUV 3D mask effects GAN (JMM 2021, Awad et al.)
- 관련: 3D mask effects in high NA EUV (SPIE 10957, 2019, Erdmann)
- 관련: Pre-training CNN for EUV M3D (SPIE 12954, 2024)

## 태그
`Recipe`, `JMM`, `SPIE`, `EUV`, `Mask3D`, `CNN`, `M3D`, `T2TCD`, `LithographySimulation`, `ThickMask`, `RCWA`, `TokyoTech`, `iN3`, `2021`
