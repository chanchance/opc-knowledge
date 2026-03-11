# Machine Learning Techniques for OPC Improvement at the Sub-5nm Node

## 메타데이터
- **저자**: (SPIE 11323 발표, 2020)
- **연도**: 2020
- **게재지**: Proc. SPIE 11323, Optical Microlithography XXXIII
- **DOI/URL**: https://doi.org/10.1117/12.2551841

## 핵심 요약
5nm 이하 노드에서 OPC 성능 개선을 위한 기계학습 기법들을 연구한다. ML 기반 보정 예측이 런타임 30% 이상 단축, 기존 리소그래피 모델 대비 시뮬레이션 정확도 15% 향상을 달성함을 보인다.

## 주요 기여
1. Sub-5nm 노드 OPC에서 ML 기법 적용의 런타임 및 정확도 이중 개선 시연
2. ML 기반 보정 예측으로 런타임 30% 이상 단축
3. 기존 리소그래피 컴팩트 모델 대비 시뮬레이션 정확도 15% 향상
4. 극미세 노드에서 OPC 정확도 요구 사항과 ML 솔루션의 적합성 분석
5. 다양한 ML 아키텍처의 OPC 응용 성능 비교

## 모델 수식/아키텍처
- ML 보정 예측기: 레이아웃 특징 → OPC 보정량 직접 예측
- 입력 특징: 마스크 패턴 로컬 밀도, CD, 피치, 형상 복잡도
- 출력: 엣지 이동량(edge placement correction) 또는 CD 보정값
- 모델 앙상블: 다수 ML 모델 조합으로 예측 안정성 향상
- 런타임 최적화: 빠른 ML 추론으로 전통적 RCWA/시뮬레이션 대체

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [x] ML/DL
- [x] 하이브리드

## OPC 툴 구현 관련성
- SKOPC의 ML 기반 OPC 보정 예측 모듈 구현에 직접 참조
- Sub-5nm(EUV) 노드에서 OPC 런타임 단축과 정확도 향상 동시 달성 방안
- ML 모델을 기존 리소그래피 시뮬레이터의 대안 또는 보조 모듈로 활용
- Samsung_ML_OPC(2020) 등 동시대 ML OPC 연구와 비교 가능

## 태그
`Model`, `ML`, `OPC`, `Sub5nm`, `Runtime`, `Accuracy`, `LithographyModel`, `SPIE`
