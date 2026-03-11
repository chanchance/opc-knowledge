# Accurate Prediction of EUV Lithographic Images and 3D Mask Effects Using Generative Networks

## 메타데이터
- **저자**: Abdalaziz Awad, Philipp Brendel, Peter Evanschitzky, Dereje S. Woldeamanual, Andreas Rosskopf, Andreas Erdmann
- **연도**: 2021
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology (JMM), Vol. 20, Issue 4, 043201
- **DOI/URL**: https://doi.org/10.1117/1.JMM.20.4.043201
- **인용수**: ~30

## 핵심 요약
생성적 신경망(GAN 계열)을 활용하여 EUV 리소그래피 이미지를 빠르고 정확하게 예측하며, EMF(Electromagnetic Field) 시뮬레이션이 필요한 마스크 3D 효과(M3D effects)를 포함한 EUV 공정 변동을 딥러닝으로 모델링한다. 기존 리고러스 EMF 시뮬레이션 대비 수백 배 빠르면서 정확한 EUV 이미지 예측을 달성함으로써, OPC 및 SMO 최적화 루프에서 EUV M3D 시뮬레이션의 실용적 통합을 가능하게 한다.

## 주요 기여
1. GAN 기반 EUV 리소그래피 이미지 예측 (M3D 효과 포함)
2. EMF 시뮬레이션 대비 수백 배 빠른 EUV 이미지 예측
3. EUV 공정 변동(포커스, 도즈, 마스크 오차) 통합 모델링
4. OPC/SMO 루프에 EUV M3D 시뮬 실용적 통합 경로 제시

## Recipe/Process Flow 상세

### EUV M3D 효과와 시뮬레이션 과제
```
EUV 리소그래피 (λ=13.5nm, NA=0.33~0.55):
  반사형 마스크 (크롬 흡수체 + Mo/Si 다층막)
  경사 조명: 6° 오프-액시스 반사
  M3D 효과 (마스크 3차원 효과):
    마스크 흡수체 3D 형상이 근접장 회절에 영향
    H-V 비대칭 (수평-수직 라인 최적 포커스 차이)
    비텔레센트리시티: 패턴 위치에 따른 이미지 이동
    최적 포커스 시프트: 마스크 두께/흡수체 형상 의존

리고러스 EMF 시뮬레이션:
  RCWA (Rigorous Coupled Wave Analysis)
  FDTD (Finite-Difference Time-Domain)
  정확도: 높음
  속도: 매우 느림 (클립당 수십 분~수 시간)
  OPC/SMO 루프: 수천~수만 번 시뮬 필요 → 실용 불가
```

### 생성적 신경망 기반 EUV 예측 모델
```
모델 구조: 조건부 GAN (cGAN) 또는 U-Net 변형

입력:
  타겟 레이아웃/마스크 이미지
  공정 조건: 포커스 F, 도즈 D
  마스크 변수: 흡수체 높이, CD 바이어스

출력:
  EUV 항공 이미지 I(x, y; F, D) [M3D 효과 포함]
  또는 레지스트 이미지 (컨투어)

훈련 데이터:
  리고러스 EMF 시뮬레이션 결과 (수천~수만 클립)
  다양한 패턴 유형, CD/pitch, 포커스/도즈 조건

GAN 훈련:
  생성기 G: 레이아웃+조건 → EUV 이미지
  판별기 D: 진짜 EMF 이미지 vs. G 생성 이미지
  물리 손실: 훈련된 모델의 물리적 일관성 강제
```

### M3D 효과 모델링 전략
```
M3D 효과의 공간 분리:
  1. 방향성 비대칭 (H vs. V):
     H-라인: 더 강한 M3D 영향 (경사 조명과 평행)
     V-라인: 다른 M3D 패턴
  2. 공간 주파수 의존성:
     고주파 (작은 pitch) → M3D 효과 심화
  3. CD 의존성:
     CD 변화 → 흡수체 두께/폭 비율 변화 → M3D 변화

신경망 전략:
  별도 분기(branch): H-라인 M3D, V-라인 M3D
  주파수 인식 컨볼루션: 다중 스케일 특징 추출
  조건부 입력: 마스크 설계 파라미터를 조건으로

EUV 공정 변동 통합:
  포커스 스캐닝 (Focus Exposure Matrix):
    다수 (F, D) 조건에서 이미지 예측 → 공정 윈도우 계산
  Dose to size 보정: 도즈 변동 → CD 변화 예측
```

### 성능 결과
```
EMF 시뮬레이션 대비:
  정확도: 이미지 예측 오차 < 1% (픽셀 강도 기준)
  속도: 수백 배 빠름 (ms vs. 수분/클립)

M3D 효과 재현:
  H-V 비대칭 포커스 시프트: 정확히 예측
  비텔레센트리시티에 의한 이미지 이동: 예측 가능

OPC/SMO 통합 가능성:
  GAN 예측을 OPC 목적함수에 통합:
    f(M) = GAN(M, F, D) → 미분 가능 (역전파 가능)
  SMO: GAN 예측으로 EUV SMO 비용 100× 감소
```

## OPC 툴 구현 관련성
- **SKOPC EUV 시뮬 가속**: `skopc/modeling/litho_engine.py`에 GAN 기반 EUV M3D 예측 통합
- **TorchLitho 연동**: TorchLitho EUV 모듈에 GAN 예측 레이어 추가
- **SMO 통합**: SMO 목적함수에 GAN EUV 이미지를 EMF 대리 모델로 활용
- **공정 윈도우**: GAN 기반 포커스-도즈 스캐닝으로 EUV 공정 윈도우 빠른 계산

## 참고문헌
- JMM, Vol. 20, Issue 4, 043201 (November 2021)
- 저자 소속: Fraunhofer IISB (Andreas Erdmann 그룹)
- 관련: 3D mask effects in high NA EUV (SPIE 10957, 2019)
- 관련: Fast EUV simulation using CNN (JMM 2021)
- 관련: EUV OPC modeling requirements (SPIE 9048, 2014)

## 태그
`Recipe`, `JMM`, `SPIE`, `EUV`, `Mask3D`, `M3D`, `GenerativeNetwork`, `GAN`, `NeuralNetwork`, `LithographySimulation`, `ProcessWindow`, `Fraunhofer`, `2021`
