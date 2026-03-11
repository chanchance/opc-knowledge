# TokMan: Tokenize Manhattan Mask Optimization for Inverse Lithography

## 메타데이터
- **저자**: Yiwen Wu 외 (저자명 확인 필요 — NeurIPS 2025 포스터)
- **연도**: 2025
- **게재지/학회**: NeurIPS 2025 (Advances in Neural Information Processing Systems)
- **DOI/URL**: https://openreview.net/forum?id=hsf4gi5iEN
- **인용수**: 미확인 (2025년 최신 논문)

## 핵심 요약
마스크 최적화를 이산적(discrete)이고 구조 인식(structure-aware) 시퀀스 모델링 태스크로 정식화한 최초의 프레임워크다. 기존 학습 기반 ILT 방법들이 연속적 픽셀 그리드에서 곡선 마스크를 생성하여 맨해튼 제약(Manhattan constraints)을 위반하는 문제를 해결한다. 디퓨전 트랜스포머(Diffusion Transformer)로 레이아웃을 폴리곤 단위 의존성을 가진 이산 기하 프리미티브로 토크나이징하고, 광학 근접 효과로 인해 왜곡된 맨해튼 정렬 점 시퀀스를 디노이징한다. 미분 가능 시뮬레이션을 통한 자기 지도 리소그래피 피드백과 ILT 후처리 정제로 학습하여, 최고 수준의 충실도, 런타임 효율성, 엄격한 제조 준수를 달성한다.

## 주요 기여
- **마스크 최적화의 시퀀스 모델링 재정식화**: 최초로 ILT를 이산 구조 인식 시퀀스 모델링으로 정식화
- **디퓨전 트랜스포머 기반 토크나이저**: 레이아웃을 이산 기하 프리미티브로 토크나이징
- **맨해튼 정렬 보장**: 생성된 마스크의 맨해튼 기하 준수 엄격 보장
- **자기 지도 리소그래피 피드백**: 미분 가능 시뮬레이션으로 레이블 없이 학습
- **ILT 후처리 정제**: 디퓨전 모델 출력을 ILT로 추가 정제하는 혼합 파이프라인

## 검증 방법론
- **대규모 IC 레이아웃 데이터셋**: 실제 IC 레이아웃 대규모 데이터셋으로 성능 평가
- **맨해튼 준수 검증**: 생성된 마스크의 맨해튼 기하 위반 수 측정
- **충실도 측정**: 웨이퍼 시뮬레이션 이미지와 목표 패턴 간 충실도 평가
- **런타임 효율**: 기존 ILT 및 ML-ILT 방법들과 처리 속도 비교
- **ILT 정제 효과**: 디퓨전 모델 단독 vs. ILT 정제 추가 시 성능 변화 측정

## 검증 지표
- **EPE 허용 범위**: EPE 위반 수 기준 마스크 최적화 품질
- **맨해튼 위반 수**: 제조 규칙 위반 (맨해튼 기하 이탈) 카운트
- **L2/MSE 오차**: 웨이퍼 시뮬레이션 충실도
- **PVB (Process Variation Band)**: 공정 변동 견고성
- **사용 시뮬레이터**: 미분 가능 리소그래피 시뮬레이터 (자기 지도 학습용)
- **검증 커버리지**: 대규모 IC 레이아웃 데이터셋

## OPC 툴 구현 관련성
SKOPC의 ILT 및 OPC 마스크 생성 모듈에 다음과 같이 활용 가능:
1. **이산 마스크 표현**: TokMan의 폴리곤 토크나이징으로 SKOPC의 마스크 데이터 구조 개선
2. **맨해튼 마스크 보장**: 디퓨전 모델로 생성된 마스크의 맨해튼 기하 자동 보장
3. **ILT-생성형 AI 하이브리드**: 생성형 AI와 수치 ILT를 결합한 하이브리드 OPC 파이프라인
4. **자기 지도 OPC 학습**: 레이블 데이터 없이 미분 가능 시뮬레이션 피드백으로 OPC 모델 학습
5. **디퓨전 기반 마스크 생성**: 디퓨전 트랜스포머를 OPC 마스크 초기화 및 생성에 활용

## 참고문헌 (핵심)
- DDPM (Ho et al., 2020) - 디노이징 확산 확률 모델 원형
- DiT (Peebles & Xie, 2023) - 디퓨전 트랜스포머
- LithoBench (Zheng et al., 2023) - 컴퓨테이셔널 리소그래피 벤치마크
- ILILT (Yang & Ren, 2024) - 암묵적 학습 ILT
- GPU-ILT (Yang & Ren, 2024) - GPU 가속 ILT

## 태그
`Verification`, `OPC`, `ILT`, `Diffusion Model`, `Transformer`, `Tokenization`, `Manhattan`, `Sequence Modeling`, `NeurIPS`, `2025`, `Self-supervised`, `Mask Optimization`, `Discrete Representation`
