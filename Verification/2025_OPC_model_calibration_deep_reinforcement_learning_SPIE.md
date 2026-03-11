# OPC Model Calibration Using Deep Reinforcement Learning

## 메타데이터
- **저자**: Weilun Chiu, Tony Hu, Terry Hsuan, Elvis Yang, T. H. Yang, K. C. Chen
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV (SPIE Advanced Lithography + Patterning 2025, 2025년 4월 22일)
- **DOI/URL**: https://spie.org/advanced-lithography/presentation/OPC-model-calibration-using-deep-reinforcement-learning/13425-58

## 핵심 요약
OPC 모델 캘리브레이션은 모델 항(term)의 최적 조합을 찾고 대응 파라미터의 회귀(regression)를 통해 모델 예측 오차를 최소화하는 과정이다. 이 논문은 심층 강화학습(DRL)을 이용하여 OPC 모델 파라미터를 예측하는 에이전트(Agent)를 학습시키는 방법론을 제안한다. 보상 함수는 OPC 모델 캘리브레이션의 음의 RMSE로 정의된다.

## 주요 기여
1. **DRL 기반 OPC 파라미터 예측**: 에이전트가 OPC 모델 파라미터를 직접 예측하는 직접 접근법과 VAE/PCA/커널 PCA로 파라미터 차원을 4D 벡터로 축소하는 차원 축소 접근법 두 가지 제안
2. **두 가지 최적화 접근법**: (1) DRL 모델이 모든 OPC 파라미터를 직접 예측, (2) VAE/PCA/Kernel PCA로 파라미터 공간을 4D로 압축 후 DRL 최적화
3. **VIA 레이어 실증**: VIA 레이어에서 실험을 수행하여 제안 DRL 모델이 기존 순차적 캘리브레이션과 동등한 성능 달성
4. **자동화된 캘리브레이션**: 사람의 개입 없이 OPC 모델 파라미터를 자동으로 최적화하는 완전 자동화 파이프라인

## 검증 방법론
- VIA 레이어에서 DRL 캘리브레이션 결과와 기존 순차적 캘리브레이션 방법 비교
- RMSE(Root Mean Square Error)를 캘리브레이션 품질 지표로 사용
- 직접 예측 vs 차원 축소(VAE/PCA/커널 PCA) 방식 간 성능 비교

## OPC 툴 구현 관련성
- `skopc/modeling/` 내 OPC 모델 캘리브레이션 모듈에 DRL 기반 파라미터 최적화 통합 가능
- GNN-OPC(`skopc/modeling/gnn/`)와 DRL 기반 캘리브레이션을 결합한 엔드-투-엔드 학습 파이프라인 구현에 참고
- `skopc/pwo/` NSGA-II PWO와 유사하게 강화학습을 최적화 엔진으로 활용하는 설계 패턴 참고
- 자동화된 OPC 모델 캘리브레이션 레시피 실행기 구현 시 DRL 에이전트 통합 방안으로 활용

## 태그
`Verification`, `SPIE`, `OPC_Model`, `Calibration`, `Deep_Reinforcement_Learning`, `DRL`, `VAE`, `Automation`, `2025`
