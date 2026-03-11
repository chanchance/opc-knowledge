# RuleLearner: OPC Rule Extraction From Inverse Lithography Technique Engine

## 메타데이터
- **저자**: Ziyang Yu, Su Zheng, Wenqian Zhao, Shuo Yin, Xiaoxiao Liang, Guojin Chen, Yuzhe Ma, Bei Yu, Martin D.F. Wong
- **연도**: 2025
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD), Vol. 44, No. 5, May 2025
- **DOI/URL**: https://ieeexplore.ieee.org/document/10753456/

## 핵심 요약
ILT(Inverse Lithography Technology) 엔진의 정교한 마스크 최적화 능력을 학습하여 OPC 룰과 SRAF(Sub-Resolution Assist Feature) 생성 룰을 자동으로 추출하는 RuleLearner 프레임워크를 제안한다. ILT는 표현력이 뛰어나지만 전체 설계 클립에 대해 마스크를 생성하기 비용이 크므로, 소수의 ILT 결과로부터 룰을 학습해 대규모 적용 가능성을 확보한다.

## 주요 기여
1. **ILT 기반 룰 자동 추출**: ILT 엔진 결과를 지식 소스로 활용하여 모델 기반 OPC 룰과 SRAF 룰을 자동화된 방식으로 학습
2. **정보 보강 ILT 엔진**: 룰 추출을 위한 information-augmented ILT 엔진 설계
3. **자연 기울기 최적화**: 추출된 룰 파라미터 분포를 맞춤형 natural gradient로 정제
4. **엣지 세그먼테이션 및 이동 안내**: 추출된 룰로 OPC 엣지 이동을 안내하여 리소그래피 성능 향상
5. **범용 적용성**: 다양한 복잡 설계 패턴에서 최고의 리소그래피 성능과 계산 효율성 달성

## 검증 방법론
- 다양한 설계 패턴 클립에서 EPE(Edge Placement Error) 측정
- 기존 규칙 기반 OPC 및 순수 모델 기반 OPC 대비 성능 비교
- 계산 효율성(런타임) 평가
- SRAF 배치 정확도와 도움 패턴 인쇄 억제 효과 검증

## OPC 툴 구현 관련성
- `skopc/modeling/` 내 Rule OPC 모듈에 ILT 기반 룰 학습 기능 통합 가능
- GNN-OPC와 RuleLearner를 결합하면 데이터 효율적인 OPC 최적화 파이프라인 구축 가능
- SRAF 자동 생성 기능 개발 시 ILT 지식 전이 방식 참고
- `skopc/modeling/gnn/` GNN 아키텍처의 학습 전략으로 활용 가능

## 태그
`Verification`, `IEEE`, `TCAD`, `OPC`, `ILT`, `SRAF`, `Rule_Extraction`, `Machine_Learning`, `2025`
