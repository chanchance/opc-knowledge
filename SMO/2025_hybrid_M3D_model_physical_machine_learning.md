# Hybrid Mask 3D Modeling Driven by Both Physical Solution and Machine Learning

## 메타데이터
- **저자**: (SPIE 13425 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134251B (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051827

## 핵심 요약
물리 기반 솔루션과 머신러닝을 결합한 하이브리드 마스크 3D(M3D) 모델을 제시한다. EUV 리소그래피에서 피치가 축소됨에 따라 기존 물리 기반 모델은 런타임 증가와 정확도 저하 문제가 있고, 머신러닝 모델은 높은 정확도와 빠른 계산을 달성하지만 과적합(overfitting) 위험이 있다. 하이브리드 접근으로 두 방법의 장점을 결합한다.

## 주요 기여
1. **하이브리드 M3D 모델**: 물리 모델 + ML의 장점 결합으로 정확도-속도-일반화 균형
2. **소형 피치 M3D 처리**: EUV 축소된 피치에서도 정확한 M3D 예측
3. **과적합 방지**: 물리 제약 기반 ML 학습으로 일반화 성능 향상
4. **OPC/ILT 통합**: 빠른 하이브리드 M3D 모델로 OPC/ILT 루프 가속화

## 알고리즘/수식
### 하이브리드 M3D 모델 구조
```
물리 기반 M3D 모델:
  RCWA(M) → T_M3D_physical(fx, fy)
  장점: 물리적으로 타당, 외삽 가능
  단점: 계산 비용 높음 (작은 피치에서 급증)

ML 기반 M3D 모델:
  NN(M) → T_M3D_ML(fx, fy)
  장점: 빠른 추론
  단점: 훈련 데이터 범위 밖 일반화 취약

하이브리드 모델:
  T_M3D_hybrid = α · T_M3D_physical + (1-α) · T_M3D_ML
  또는:
  T_M3D_hybrid = T_M3D_physical_fast + NN_correction(M)
  → 물리 모델이 전반적 구조 제공
  → ML이 잔차(residual) 보정
```

### 훈련 및 검증
```
훈련 전략:
  물리 제약 손실:
    L = L_data + λ·L_physics
    L_physics: 물리 법칙(Maxwell 방정식) 위반 페널티

성능 평가:
  정확도: CD 오차 vs RCWA 기준
  속도: 추론 시간 vs RCWA
  일반화: 미학습 패턴에서 정확도 유지
```

## OPC 툴 SMO 구현 관련성
- 하이브리드 M3D 통합: SKOPC에서 물리+ML 결합 M3D 모델 채택
- OPC/ILT 루프 가속: 하이브리드 M3D로 전체 칩 OPC 런타임 단축
- 일반화 성능: 새로운 마스크 패턴에도 안정적인 M3D 예측
- SMO 비용 함수: 빠른 M3D 모델로 SMO 반복 계산 가속화

## 태그
`M3D`, `hybrid_model`, `machine_learning`, `physics_informed`, `EUV`, `OPC`, `ILT`, `RCWA`, `DTCO`, `SPIE`, `2025`
