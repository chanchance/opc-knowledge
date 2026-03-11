# Pre-training CNN for Fast EUV Lithography Simulation Including M3D Effects

## 메타데이터
- **저자**: Hiroyoshi Tanabe, Akira Jinguji, Atsushi Takahashi
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540I
- **DOI/URL**: https://doi.org/10.1117/12.3009880
- **인용수**: ~10

## 핵심 요약
EUV 리소그래피 시뮬레이션에서 마스크 3D 효과(M3D)를 포함한 빠른 시뮬레이션을 위해 사전 훈련(pre-training) CNN 방법론을 제안한다. M3D 효과에 의해 왜곡된 회절 진폭 계산에 리고러스 전자기장(EM) 시뮬레이션이 필요하지만, 이는 OPC 응용에서 매우 시간이 많이 소요된다. 사전 훈련으로 CNN의 M3D 효과 일반화 능력을 향상시키며, 다양한 마스크 패턴에서 빠른 M3D 시뮬레이션을 실현한다.

## 주요 기여
1. M3D 효과 포함 EUV 시뮬레이션을 위한 CNN 사전 훈련 방법론
2. 사전 훈련으로 소량 파인 튜닝 데이터로 새 패턴에 적응
3. 다양한 마스크 타입(OPC 포함, 커비리니어)에서 M3D CNN 일반화
4. 기존 Tanabe et al. (JMM 2021) CNN 방법의 사전 훈련 확장

## Recipe/Process Flow 상세

### 사전 훈련의 필요성
```
기존 CNN EUV M3D 시뮬:
  Tanabe et al. JMM 2021: CNN으로 T2T CD 예측
  한계:
    훈련 패턴 유형 외 패턴: 일반화 부족
    새 노드/흡수체 유형 변경 시: 처음부터 재훈련 필요
    OPC 포함, 커비리니어 패턴: 별도 훈련 어려움

사전 훈련 필요성:
  다양한 패턴 유형 커버: 1D, 2D, OPC 포함, 커비리니어
  전이 학습: 사전 훈련 → 소량 데이터로 새 패턴 적응
  데이터 효율: EM 시뮬 데이터 생성 비용 절감
```

### CNN 사전 훈련 방법론
```
사전 훈련 태스크:
  대규모 다양한 마스크 패턴 → EM 시뮬 데이터 생성
  사전 훈련: CNN이 M3D 효과의 일반 패턴 학습
    - 흡수체 형상 → 회절 진폭 왜곡 관계
    - 주파수 의존 M3D 패턴
    - H-V 비대칭 특성

사전 훈련 데이터:
  합성 1D 패턴: 다양한 CD, pitch, 방향 (H, V)
  합성 2D 패턴: 코너, 교차, 끝단 형상
  데이터 증강: 이동, 회전, 스케일 변형
  EM 시뮬 레이블: RCWA 계산 회절 진폭/T2T CD

미세 조정 (Fine-tuning):
  소량 목표 패턴 데이터 (iN3 실제 패턴 등)
  → 사전 훈련 가중치에서 출발하여 빠른 수렴
  → 새 노드/패턴 유형에 효율적 적응
```

### 아키텍처 세부사항
```
CNN 구조 (ResNet 기반):
  인코더: 다중 컨볼루션 블록 + 잔차 연결
  수용 영역: M3D 효과 공간 범위 포함 (수백 nm 수준)
  다중 스케일: 다양한 pitch/CD 처리

입력:
  마스크 패턴 이미지 (이진 또는 그레이)
  패턴 정보: CD, pitch (채널로 추가)
  흡수체 파라미터: 두께, 굴절률 (물질 조건)

출력:
  왜곡 회절 진폭: ΔA(f_x, f_y) for key diffraction orders
  또는 T2T CD 직접 예측

사전 훈련 vs. 미세 조정 가중치:
  초기층 (저수준 특징): 사전 훈련 가중치 고정
  후기층 (패턴별 특화): 미세 조정 학습
```

### iN3 패턴 평가
```
imec 3nm 노드 (iN3) 패턴:
  로직 메탈 레이어: OPC 포함 복잡 패턴
  비아 레이어: 커비리니어 비아 패턴
  실제 제조 의도 패턴 → 강력한 검증

사전 훈련 효과:
  처음부터 훈련: iN3 패턴 부족 → 과적합/일반화 부족
  사전 훈련 + 미세 조정: 적은 iN3 데이터로 높은 정확도
  T2T CD 오차: 사전 훈련 적용 시 유의미하게 감소

커비리니어 비아 처리:
  기존 직교 패턴 CNN: 커브 형상 M3D 예측 부정확
  사전 훈련 포함 커비리니어: 커브 형상 M3D 패턴 학습
  → EUV 비아 OPC에서 M3D 보정 정확도 향상
```

## OPC 툴 구현 관련성
- **SKOPC EUV M3D 사전 훈련**: 다양한 패턴으로 CNN 사전 훈련 후 신규 노드 적응
- **신규 노드 적응**: 소량 EM 시뮬 데이터로 신규 EUV 노드 M3D CNN 빠른 구축
- **커비리니어 OPC**: 커비리니어 마스크 M3D 효과 예측 지원
- **OPC 루프 통합**: 사전 훈련 CNN으로 EUV OPC 이터레이션 M3D 보정 ms 처리

## 참고문헌
- Proc. SPIE 12954, DTCO and Computational Patterning III (April 2024)
- 저자 소속: Tokyo Tech (Atsushi Takahashi 그룹)
- 관련: Fast EUV simulation CNN (JMM 2021, Tanabe et al.)
- 관련: EUV CNN evaluation iN3 (SPIE 12495, 2023, Tanabe et al.)
- 관련: Accurate EUV 3D mask GAN (JMM 2021, Awad et al.)

## 태그
`Recipe`, `SPIE`, `EUV`, `CNN`, `M3D`, `PreTraining`, `TransferLearning`, `LithographySimulation`, `ThickMask`, `Curvilinear`, `iN3`, `TokyoTech`, `2024`
