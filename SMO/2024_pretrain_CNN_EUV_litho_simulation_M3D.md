# Pre-Training CNN for Fast EUV Lithography Simulation Including M3D Effects

## 메타데이터
- **저자**: (SPIE 12954 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540I (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3009880

## 핵심 요약
마스크 패턴 입력으로부터 M3D 파라미터를 매우 빠르게 예측하는 사전 훈련(pre-training) CNN 모델을 개발한다. EUV 리소그래피 시뮬레이션에서 M3D 효과 포함 빠른 이미징 예측을 달성하여 OPC/SMO 가속화에 기여한다.

## 주요 기여
1. **M3D 포함 사전 훈련 CNN**: 마스크 패턴에서 M3D 파라미터 직접 예측
2. **빠른 EUV 시뮬레이션**: M3D 효과를 포함하면서도 RCWA 대비 획기적 속도 향상
3. **사전 훈련 전략**: 대규모 시뮬레이션 데이터로 사전 훈련 후 특정 공정에 파인튜닝
4. **OPC/SMO 가속화**: 빠른 M3D CNN으로 OPC 반복 계산 속도 향상

## 알고리즘/수식
### 사전 훈련 CNN 아키텍처
```
사전 훈련(Pre-training):
  대규모 다양한 마스크 패턴으로 훈련
  입력: 마스크 레이아웃 패치
  출력: M3D 파라미터 {BFS, ΔCD_M3D, CD_bias}

파인튜닝(Fine-tuning):
  특정 마스크 스택/공정 파라미터에 맞게 적응
  소량의 RCWA 시뮬레이션 데이터로 빠른 적응

M3D 파라미터 예측:
  CNN(M_patch) → {BFS(pitch), ΔCD(pitch, orient), CD_asymm}
  → 직접 Hopkins 적분 보정에 사용
```

### 속도-정확도 성능
```
예측 속도:
  RCWA: O(N_harmonics² × N_layers) per 피치
  CNN 추론: 밀리초 단위 (패치당)
  가속 배율: 100x ~ 1000x (패턴 복잡도에 따라)

정확도:
  M3D 파라미터 오차: < 5% (RCWA 대비)
  CD 오차: < 0.5nm
```

## OPC 툴 SMO 구현 관련성
- 사전 훈련 M3D CNN: SKOPC OPC/SMO 엔진에서 M3D 빠른 계산 옵션
- 파인튜닝 전략: 새로운 마스크 스택에 소량 데이터로 빠른 모델 적응
- EUV OPC 가속: M3D CNN으로 전체 칩 OPC 런타임 단축
- SMO 비용 함수 가속: M3D를 포함한 SMO 반복 계산 현실화

## 태그
`CNN`, `pre_training`, `M3D`, `EUV`, `fast_simulation`, `OPC_acceleration`, `fine_tuning`, `RCWA`, `DTCO`, `SPIE`, `2024`
