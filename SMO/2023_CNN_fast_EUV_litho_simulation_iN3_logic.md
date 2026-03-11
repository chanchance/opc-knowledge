# Evaluation of CNN for Fast EUV Lithography Simulation Using iN3 Logic Mask Patterns

## 메타데이터
- **저자**: (SPIE 12495 저자 정보)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124951J (2023)
- **DOI/URL**: https://doi.org/10.1117/12.2659063

## 핵심 요약
iN3(intel 3nm급) 로직 마스크 패턴에 대해 CNN(Convolutional Neural Network)을 빠른 EUV 리소그래피 시뮬레이션 대리 모델로 평가한다. 기존 물리 기반 시뮬레이션 대비 CNN의 정확도와 속도를 정량적으로 비교하여 OPC/SMO 가속화 가능성을 검토한다.

## 주요 기여
1. **CNN EUV 시뮬레이션 대리 모델**: iN3 로직 패턴에 특화된 CNN 기반 빠른 시뮬레이션
2. **속도-정확도 평가**: 물리 기반 vs CNN 시뮬레이션의 정량적 비교
3. **실제 로직 패턴 적용**: 반복 테스트 패턴이 아닌 실제 로직 마스크에서 CNN 성능 평가
4. **OPC/SMO 가속화 가능성**: CNN 대리 모델로 OPC/SMO 루프 계산 시간 단축

## 알고리즘/수식
### CNN 기반 EUV 리소그래피 시뮬레이션
```
CNN 아키텍처:
  입력: 마스크 패턴 이미지 M (패치 단위)
  출력: 웨이퍼 이미지/CD 예측값

훈련 데이터:
  물리 기반 시뮬레이션 결과 쌍 (M_i, CD_i)
  iN3 로직 레이어 다양한 패턴

손실 함수:
  L = ||CD_CNN(M) - CD_physics(M)||² + λ·Regularization

예측 속도:
  물리 시뮬레이션: O(N²) 또는 O(N log N) (FFT)
  CNN 추론: O(N) - 패치 처리로 선형 확장
```

### 성능 평가 메트릭
```
정확도:
  CD 오차 평균: μ(|CD_CNN - CD_ref|)
  CD 오차 3σ: 3σ(CD_CNN - CD_ref)

속도:
  가속 배율 = T_physics / T_CNN
  목표: 100x 이상 가속
```

## OPC 툴 SMO 구현 관련성
- ML 기반 리소그래피 시뮬레이션: SKOPC SMO/OPC 엔진에서 CNN 대리 모델 옵션
- 로직 패턴 적용: 반복 패턴 이외 로직 레이어 OPC/SMO에서 CNN 활용
- OPC 가속화: CNN으로 OPC 반복 계산(iterate) 속도 향상
- iN3급 노드 지원: 3nm 이하 노드 EUV OPC/SMO에서 ML 모델 채택 방향

## 태그
`CNN`, `EUV`, `deep_learning`, `fast_simulation`, `surrogate_model`, `iN3`, `logic_pattern`, `OPC_acceleration`, `DTCO`, `SPIE`
