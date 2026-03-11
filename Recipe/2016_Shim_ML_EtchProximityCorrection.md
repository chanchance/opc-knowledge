# Machine Learning-Guided Etch Proximity Correction

## 메타데이터
- **저자**: Suhyeong Shim, Youngsoo Shin (et al.)
- **소속**: (IEEE TCAD 게재)
- **연도**: 2016
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD)
- **DOI/URL**: https://ieeexplore.ieee.org/document/7738596/

## 핵심 요약
리소그래피 후 식각(etch) 공정에서 발생하는 proximity 효과를 보정하는 Etch Proximity Correction(EPC)에 머신러닝을 도입한 연구. 기존 rule-based 및 model-based EPC 방식이 20nm 이하에서 부정확해지는 한계를 인공신경망(ANN)으로 극복하며, model-based EPC 대비 34% 더 정확한 etch bias 예측을 달성한다.

## 주요 기여
1. **ML 기반 EPC 프레임워크**: 각 관심 segment와 그 주변 환경을 기하학적·광학적 파라미터로 특성화 → ANN이 etch bias 예측
2. **정확도 향상**: model-based EPC 대비 34% 정확도 개선 (20nm 이하 기술 노드 대상)
3. **Feature 설계**: segment별 geometry 특성(폭, 피치, 인접 패턴 밀도)과 optical 특성을 입력 피처로 사용
4. **Rule/Model-based 한계 극복**: 기존 EPC는 물리 모델의 단순화로 인해 복잡한 2D 패턴에서 부정확 → NN이 복잡한 비선형 의존성 학습

## Recipe/Flow 상세
```
[ML-EPC Flow]
1. 입력 레이아웃 패턴에서 각 edge segment 추출
2. Segment별 Feature 추출:
   - 기하학적: 선폭, 피치, 인접 feature까지의 거리
   - 광학적: 해당 위치에서의 aerial image 특성
3. 훈련된 ANN으로 etch bias 예측
4. 예측된 bias를 mask에 역방향 적용 (EPC 보정값)
5. 보정된 mask로 OPC 실행
6. 최종 wafer CD 검증
```

### 핵심 파라미터
- **입력 피처**: geometric parameters + optical parameters per segment
- **출력**: etch bias prediction (nm 단위)
- **정확도 지표**: model-based EPC 대비 34% 개선
- **적용 노드**: 20nm 이하

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: etch bias 보정 단계에 ML 모델 통합 고려
- **Post-lithography correction**: SKOPC의 OPC 플로우에서 리소그래피 이후 etch 단계 보정 모듈 추가 참고
- **Feature engineering**: segment 기반 기하학적+광학적 피처 추출은 GNN-OPC의 node feature 설계와 직접 연관
- `skopc/modeling/gnn/`: GNN edge segment displacement 예측에 etch bias 피처 포함 확장 가능

## 태그
`Recipe`, `IEEE`, `Etch Proximity Correction`, `EPC`, `Machine Learning`, `Neural Network`, `Post-Lithography`, `Etch Bias`, `20nm`
