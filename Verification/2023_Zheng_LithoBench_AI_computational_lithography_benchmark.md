# LithoBench: Benchmarking AI Computational Lithography for Semiconductor Manufacturing

## 메타데이터
- **저자**: Su Zheng, Haoyu Yang, Haoxing Ren, Bei Yu (CUHK, NVIDIA)
- **연도**: 2023
- **게재지/학회**: NeurIPS 2023 Datasets and Benchmarks Track
- **DOI/URL**: https://proceedings.neurips.cc/paper_files/paper/2023/hash/604b9fa9e1c16284e6517d923cf9ff20-Abstract-Datasets_and_Benchmarks.html
- **GitHub**: https://github.com/shelljane/lithobench
- **인용수**: 미확인

## 핵심 요약
LithoBench는 AI 기반 컴퓨테이셔널 리소그래피 연구를 위한 최초의 대규모 표준 벤치마크 데이터셋 및 평가 프레임워크다. 실제 회로 설계에서 크롭하거나 유명 ILT 테스트케이스의 레이아웃 토폴로지에 따라 합성한 12만 개 이상의 타일로 구성된다. 리소그래피 시뮬레이션과 마스크 최적화(ILT) 두 가지 핵심 태스크를 위한 표준 학습 데이터와 평가 메트릭(L2, PVB, EPE, shots)을 제공하며, 45nm 기술 노드를 기준으로 최신 DNN 모델들을 비교 평가한다. 기존 ML 기반 ILT 연구들이 통일된 벤치마크 없이 진행되던 문제를 해결한다.

## 주요 기여
- **최초의 통합 벤치마크**: 리소그래피 시뮬레이션과 마스크 최적화를 동시에 다루는 통합 벤치마크 제공
- **12만 개 이상 타일**: 실제 IC 설계 + 합성 레이아웃 기반 대규모 데이터셋
- **표준 평가 메트릭**: L2, PVB, EPE, shots 측정을 위한 표준 인터페이스 제공
- **DNN 프레임워크**: DNN 설계 및 평가를 위한 표준 프레임워크
- **재현 가능한 비교**: 최신 모델들(GAN-OPC, DAMO, Neural-ILT 등)을 동일 조건에서 벤치마크

## 검증 방법론
- **리소그래피 시뮬레이션 태스크**: 마스크 입력 → 웨이퍼 컨투어 출력 예측 정확도 평가
- **마스크 최적화(ILT) 태스크**: 목표 레이아웃 → 최적 마스크 생성 품질 평가
- **L2 손실 측정**: 예측/생성된 이미지와 참조 이미지 간 픽셀 단위 L2 오차
- **PVB 측정**: 공정 변동 밴드 면적으로 마스크 견고성 평가
- **EPE 측정**: 엣지 배치 오차 위반 수 계수
- **Shots 측정**: 마스크 복잡도(제조 비용) 지표

## 검증 지표
- **EPE 허용 범위**: EPE 위반 수 기준 (벤치마크 내 각 방법별 비교)
- **PVB (Process Variation Band)**: 낮을수록 공정 견고성 우수
- **L2 오차**: 픽셀 단위 시뮬레이션/최적화 정확도
- **Shots**: 마스크 복잡도 및 제조 비용 지표
- **사용 시뮬레이터**: 학술 리소그래피 모델 (45nm 노드)
- **검증 커버리지**: 12만 개 이상 타일 (실제 IC 설계 + 합성 레이아웃)

## OPC 툴 구현 관련성
SKOPC의 OPC 검증 및 모델 평가에 다음과 같이 활용 가능:
1. **표준 벤치마크 통합**: SKOPC의 OPC 알고리즘 성능을 LithoBench 기준으로 객관적 평가
2. **평가 메트릭 채택**: L2, PVB, EPE, Shots의 4가지 표준 메트릭을 SKOPC 검증 모듈에 도입
3. **학습 데이터 활용**: LithoBench 데이터셋을 SKOPC의 ML 기반 OPC 모델 학습에 활용
4. **비교 기준선 확립**: 공개된 최신 ML-OPC 방법들과 SKOPC 성능을 직접 비교
5. **오픈소스 생태계**: GitHub 공개 코드로 리소그래피 시뮬레이션 모듈 통합 및 확장

## 참고문헌 (핵심)
- Yang et al. (2020) - GAN-OPC: GAN 기반 OPC (비교 기준선)
- Chen et al. (2021) - DAMO: 딥 애자일 마스크 최적화 (비교 기준선)
- Gu et al. (2022) - Neural-ILT: 신경망 기반 ILT (비교 기준선)
- Sun et al. (2023) - GPU-ILT: GPU 가속 수치 ILT (참조 솔루션)
- ICCAD 2012/2019 기존 벤치마크 데이터셋

## 태그
`Verification`, `OPC`, `Benchmark`, `Dataset`, `NeurIPS`, `2023`, `ILT`, `Lithography Simulation`, `L2`, `PVB`, `EPE`, `Shots`, `45nm`, `Open Source`
