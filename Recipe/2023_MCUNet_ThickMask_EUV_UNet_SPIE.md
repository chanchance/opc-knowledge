# Thick-Mask Model Based on Multi-Channel U-Net for EUV Lithography

## 메타데이터
- **저자**: Chengzhen Yu, Xu Ma
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 1249525
- **DOI/URL**: https://doi.org/10.1117/12.2657246
- **인용수**: ~15

## 핵심 요약
EUV 리소그래피의 마스크 3D 효과(M3D)를 모델링하기 위한 다중 채널 U-Net(MCU-Net) 기반 빠른 두꺼운 마스크 모델을 제안한다. EUV 두꺼운 마스크의 근접장 회절 분포(DNF: Diffraction Near Field)를 네 개의 복소값 회절 행렬(실부/허부 포함 총 8개 실수 행렬)로 특성화하고, MCU-Net으로 이를 동시에 합성한다. 커비리니어 두꺼운 마스크 DNF 데이터셋을 기반으로 지도 학습으로 훈련하여 ILT로 생성된 커비리니어 마스크의 M3D 효과를 빠르게 모델링한다.

## 주요 기여
1. EUV 두꺼운 마스크 DNF를 8채널(4개 복소 행렬)로 표현하는 MCU-Net
2. ILT 커비리니어 마스크의 M3D 효과 빠른 모델링
3. 커비리니어 두꺼운 마스크 DNF 훈련 데이터셋 구축
4. 기존 RCWA 대비 수백 배 빠른 두꺼운 마스크 모델

## Recipe/Process Flow 상세

### EUV 두꺼운 마스크 회절 근접장
```
EUV 마스크 구조:
  기판: Si + Mo/Si 다층막 (반사층, 40쌍)
  흡수체: TaN 또는 TaBN (두께 ~56~75nm)
  반사: 6° 오프-액시스 입사광

두꺼운 마스크 효과:
  흡수체 두께 ~파장(13.5nm) → 근접장 회절 3D 구조
  얇은 마스크 근사: 흡수체 즉각 투과/반사 가정 → 부정확
  리고러스 EMF 필요: RCWA, FDTD → 3D 전자기장 계산

DNF (Diffraction Near Field):
  마스크 바로 위 근접장 전기장 분포
  복소값: E(x, y, z=0) → 진폭 + 위상
  4개 행렬: E_xx, E_xy, E_yx, E_yy (편광 혼합)
  각 행렬: 복소값 → 실부 + 허부 = 2 채널
  총 8채널: MCU-Net 출력 채널 수

커비리니어 마스크 DNF:
  ILT로 생성된 자유 형상 마스크
  직교 격자 아닌 곡선 경계 → DNF 계산 더 복잡
  기존 주기적 패턴 가정 RCWA 적용 어려움
```

### MCU-Net 아키텍처
```
다중 채널 U-Net (MCU-Net):
  입력: 마스크 이진 이미지 (1채널)
  출력: 8채널 DNF (4 복소 행렬의 실부/허부)

U-Net 구조:
  인코더: 다운샘플링 경로
    Conv + BN + ReLU × 5 레벨
    채널: 1 → 64 → 128 → 256 → 512 → 1024
  디코더: 업샘플링 경로
    TransposeConv + Skip Connection + Conv
    채널: 1024 → 512 → 256 → 128 → 64 → 8
  Skip Connection: 세부 형상 정보 보존

다중 출력 채널 설계:
  채널 1-2: E_xx 실부/허부
  채널 3-4: E_xy 실부/허부
  채널 5-6: E_yx 실부/허부
  채널 7-8: E_yy 실부/허부
  → 단일 순방향 패스로 모든 편광 성분 동시 예측

손실 함수:
  L = Σ_j ||DNF_pred_j - DNF_RCWA_j||²  (j: 8채널)
  → 모든 채널 동등 가중치 학습
```

### 훈련 데이터셋
```
커비리니어 두꺼운 마스크 데이터:
  ILT 최적화로 생성된 다양한 커비리니어 마스크 패턴
  각 패턴 → RCWA 시뮬레이션 → DNF 레이블

데이터 다양성:
  1D 패턴: 라인/스페이스 (다양한 CD, pitch)
  2D 패턴: 컨택 홀, 비아, L자형, T자형
  커비리니어: ILT 최적화 결과 자유 형상

훈련/검증 분할:
  훈련: 다양한 패턴 타입
  검증: 새로운 패턴 유형 (일반화 테스트)
  특히: OPC 포함 패턴, 커비리니어 비아
```

### 성능 결과
```
DNF 예측 정확도:
  MCU-Net vs. RCWA 기준:
    진폭 오차: < 2%
    위상 오차: 작은 수준
  커비리니어 마스크: 직교 패턴과 유사한 정확도

속도:
  RCWA: 클립당 수 분
  MCU-Net 추론: ms 단위
  속도 향상: 수백 배 이상

OPC 통합:
  MCU-Net DNF → 빠른 항공 이미지 계산
  EUV ILT/OPC 루프에서 M3D 보정 실용화
```

## OPC 툴 구현 관련성
- **SKOPC EUV M3D 모델**: `skopc/modeling/litho_engine.py`에 MCU-Net 두꺼운 마스크 모델 통합
- **커비리니어 M3D**: ILT 커비리니어 마스크 최적화 중 M3D 효과 실시간 평가
- **OPC 루프 가속**: 8채널 MCU-Net으로 ms 단위 M3D DNF → OPC 루프 통합 가능
- **편광 혼합 모델링**: EUV 편광 의존 이미징 효과 완전 모델링

## 참고문헌
- Proc. SPIE 12495, DTCO and Computational Patterning II (April 2023)
- 저자 소속: Beijing Institute of Technology (Xu Ma 그룹)
- 관련: Fast EUV simulation CNN (JMM 2021, Tanabe)
- 관련: Pre-training CNN EUV M3D (SPIE 12954, 2024, Tanabe)
- 관련: Accurate EUV 3D mask GAN (JMM 2021, Awad et al.)

## 태그
`Recipe`, `SPIE`, `EUV`, `Mask3D`, `M3D`, `UNet`, `MultiChannel`, `DNF`, `ThickMask`, `Curvilinear`, `NeuralNetwork`, `ILT`, `BIT`, `2023`
