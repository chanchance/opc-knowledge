# Accurate Prediction of EUV Lithographic Images and 3D Mask Effects Using Generative Networks

## 메타데이터
- **저자**: Awad, Brendel, Evanschitzky et al.
- **연도**: 2021
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology (JMM), Vol. 20, Issue 04, 043201
- **DOI/URL**: https://doi.org/10.1117/1.JMM.20.4.043201

## 핵심 요약
생성적 신경망(generative networks)을 사용하여 EUV 리소그래피 이미지와 마스크 3D(M3D) 효과를 정확하게 예측하는 방법을 제시한다. 전자기장(EMF) 시뮬레이션의 계산 병목 문제를 극복하기 위해 딥러닝 대리 모델(surrogate model)을 개발하며, 공정 변동성을 포함한 EUV 이미징을 효율적으로 예측한다.

## 주요 기여
1. **생성 네트워크 기반 EUV 이미징**: EMF 시뮬레이션을 대체하는 빠른 딥러닝 대리 모델
2. **M3D 효과 통합**: 마스크 3D 전자기 효과를 생성 네트워크로 모델링
3. **공정 변동성 포함 예측**: EUV 특유의 확률론적/공정 변동 효과 반영
4. **계산 효율화**: RCWA 기반 EMF 대비 수십~수백배 빠른 예측 속도

## 알고리즘/수식
### 생성 네트워크 아키텍처
```
입력: 마스크 레이아웃 M, 공정 파라미터 θ
출력: EUV 리소그래피 이미지 Î(x, y)

생성 네트워크:
  G: (M, θ) → Î
  훈련: L = L_pixel + λ_perceptual·L_perceptual + λ_adv·L_adv

M3D 효과 모델링:
  M3D_NN(M) ≈ M3D_RCWA(M)
  → RCWA 계산 없이 마스크 토포그래피 효과 예측

공정 변동 포함:
  Î = G(M, θ + δθ), δθ ~ N(0, σ²_process)
```

### EUV 이미징 예측 정확도
```
평가 메트릭:
  CD 오차: ||CD_NN - CD_RCWA||
  목표: CD 오차 < 1nm

계산 속도:
  RCWA EMF: 수 시간/필드
  생성 네트워크: 밀리초/필드 (1000x 이상 가속)
```

## OPC 툴 SMO 구현 관련성
- EUV SMO 가속화: 생성 네트워크로 SMO 비용 함수 계산 속도 향상
- M3D 빠른 모델: SMO/OPC 루프에서 M3D 효과를 실시간으로 고려 가능
- 딥러닝 대리 모델: SKOPC SMO 모듈에서 ML 기반 이미징 모델 채택 방향
- 공정 변동 내성 SMO: 공정 파라미터 변동을 포함한 강건한 최적화

## 태그
`SMO`, `EUV`, `generative_networks`, `deep_learning`, `M3D`, `surrogate_model`, `EMF`, `lithographic_simulation`, `process_variation`, `JMM`
