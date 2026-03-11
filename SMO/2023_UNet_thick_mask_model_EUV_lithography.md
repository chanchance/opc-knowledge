# Thick-Mask Model Based on Multi-Channel U-Net for EUV Lithography

## 메타데이터
- **저자**: (SPIE 12495 저자 정보)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 1249525 (2023)
- **DOI/URL**: https://doi.org/10.1117/12.2657246

## 핵심 요약
EUV 리소그래피에서 두꺼운 마스크(thick mask) 효과, 즉 M3D 효과를 모델링하기 위한 다채널 U-Net 기반 딥러닝 모델을 제시한다. ILT로 생성된 곡선형 마스크 패턴의 두꺼운 마스크 회절 스펙트럼 계산을 U-Net으로 대체하여 계산 효율을 향상시킨다.

## 주요 기여
1. **Multi-channel U-Net M3D 모델**: 마스크 두께 효과를 U-Net으로 효율적으로 모델링
2. **곡선형 마스크 지원**: ILT 곡선형 패턴의 M3D 계산 가속화
3. **회절 스펙트럼 예측**: RCWA 기반 M3D 계산을 U-Net으로 대체
4. **EUV OPC/ILT 가속화**: M3D 계산 병목 해소로 OPC/ILT 루프 속도 향상

## 알고리즘/수식
### Multi-channel U-Net 아키텍처
```
U-Net 구조:
  인코더: 마스크 패턴 M → 잠재 특징 추출
  디코더: 잠재 특징 → M3D 보정된 회절 스펙트럼

다채널 입력:
  채널 1: 마스크 투과율 (binary/attenuated)
  채널 2: 마스크 위상 (0/π)
  채널 3: 흡수층 두께 맵
  → 다채널 정보로 M3D 효과 통합 예측

출력:
  T_M3D(fx, fy): M3D 보정된 마스크 회절 스펙트럼
  → 직접 Hopkins 적분에 사용 가능

훈련:
  입력-출력 쌍: (마스크 패턴, RCWA 계산 스펙트럼)
  손실: L2(T_UNet - T_RCWA)
```

### M3D 가속화 성능
```
RCWA 계산 시간: O(N_harmonics²) × N_pitch
U-Net 추론 시간: O(N_pixels) - 빠른 CNN 추론

가속 배율: 수십~수백 배 (패턴 복잡도에 따라)
정확도: CD 오차 < 1nm 목표
```

## OPC 툴 SMO 구현 관련성
- M3D 빠른 계산: SKOPC OPC/SMO 루프에서 U-Net 기반 M3D 모델 옵션
- 곡선형 마스크 M3D: ILT/ML ILT 마스크에서 M3D 계산 통합
- SMO 비용 함수: M3D 보정된 이미지로 더 정확한 SMO 결과 달성
- 다채널 입력: 흡수층 재료/두께 변화에 대응한 범용 M3D 모델

## 태그
`U_Net`, `M3D`, `thick_mask`, `EUV`, `deep_learning`, `RCWA`, `curvilinear`, `ILT`, `diffraction_spectrum`, `OPC_acceleration`, `DTCO`, `SPIE`
