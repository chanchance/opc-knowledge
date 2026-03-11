# Using Machine Learning Etch Models in OPC and ILT Correction

## 메타데이터
- **저자**: Kevin Hooker, Lena Zavyalova, Shuo Huang, Li-Jin Chen
- **연도**: 2021
- **게재지**: Proc. SPIE 11614, Design-Process-Technology Co-optimization XV, 116140B
- **DOI/URL**: https://doi.org/10.1117/12.2587225

## 핵심 요약
DUV 및 EUV 리소그래피의 새로운 노드에서 etch 효과를 OPC 및 ILT 마스크 합성에 정확하게 통합하는 것이 점점 중요해지고 있다. 기존 룰 기반 etch 근사의 정확도 한계를 극복하기 위해, 머신러닝 기반 etch 모델을 OPC와 ILT 보정에 직접 적용하는 방법을 제시한다. 신경망 등 ML 기법이 etch 모델의 정확도와 효율성을 동시에 향상시킨다는 것을 실증한다.

## 주요 기여
1. **ML Etch 모델의 OPC/ILT 통합**: 학습 기반 etch 모델을 마스크 합성 플로우에 직접 내장
2. **룰 기반 etch 한계 극복**: 규칙 기반 etch 근사 대비 ML 모델의 정확도 우위 입증
3. **DUV/EUV 범용 적용**: DUV와 EUV 양쪽 공정에서 ML etch 모델 효과 검증
4. **OPC-ILT 공동 적용**: OPC와 ILT 양 workflow에 동일 ML etch 모델 활용
5. **Manufacturing yield 관련성**: 체계적 etch 오차 보정으로 웨이퍼 yield 향상 기여

## Recipe/Flow 상세
- **ML Etch 모델 기반 OPC 플로우**:
  1. **ML Etch 모델 학습**:
     - 학습 데이터: (resist 윤곽, etch 후 CD/윤곽) 쌍
     - 모델 구조: CNN 또는 fully-connected NN
     - 특징: 국소 패턴 밀도, CD, 방향, 주변 구조
  2. **OPC 통합**:
     - 기존 optical/resist 모델로 resist 윤곽 예측
     - ML etch 모델로 resist → 최종 etch 윤곽 변환
     - 최종 etch 윤곽 기준 EPE 최소화 OPC 수렴
  3. **ILT 통합**:
     - ILT 목적함수에 ML etch 모델 출력 포함
     - End-to-end: 마스크 → resist → etch → EPE 최소화
  4. **검증**: ML etch 모델 예측 vs. 실제 etch SEM 측정 비교
- **ML 모델 유형**:
  - 신경망(NN): 비선형 etch 근접 효과 캡처
  - 컨볼루션 신경망(CNN): 공간적 패턴 의존성 학습
- **적용 레이어**: Critical 레이어 (게이트, 금속, 컨택트)
- **평가 지표**: Etch CD 오차, OPC 수렴 반복 횟수, 웨이퍼 CD 균일도

## OPC 툴 구현 관련성
- SKOPC 모델링 모듈에 ML etch 모델 레이어 추가 방법
- `ml_etch_model.py`: CNN 기반 resist → etch 윤곽 예측 모듈
- OPC 수렴 루프에 etch 보정 단계 통합 구조
- ILT 목적함수의 etch-aware 확장 구현 참고

## 태그
`MachineLearning`, `EtchModel`, `OPC`, `ILT`, `CNN`, `EtchProximity`, `DUV`, `EUV`, `SPIE`, `2021`
