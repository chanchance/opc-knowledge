# Transforming Computational Lithography with Accelerated Computing and AI — Faster, More Accurate, and Energy-efficient

## 메타데이터
- **저자**: Saumyadip Mukhopadhyay, Kiho Yang, Kasyap Thottasserymana Vasudevan, Mounica Jyothi Divvela, Selim Dogru, Dilip Krishnamurthy, Fergo Treska, Werner Gillijns, Ryan Ryoung han Kim, Kumara Sastry, Vivek Singh
- **연도**: 2026 (arXiv 제출: 2026.01.27)
- **게재지/학회**: arXiv (eess.SP - Signal Processing)
- **DOI/URL**: https://arxiv.org/abs/2602.15036
- **인용수**: 미확인 (최신 논문)

## 핵심 요약
NVIDIA cuLitho를 활용하여 컴퓨테이셔널 리소그래피 소프트웨어 스택을 가속 컴퓨팅(AC)과 AI로 재설계한 산업 연구다. 회절 광학, 계산 기하학, 다변수 최적화, 데이터 처리 등 핵심 프리미티브를 재설계하여 57배의 엔드-투-엔드 가속을 달성한다. AI를 고충실도 대리 모델(surrogate)로 활용하여 계산 집약적 연산을 대체하고, through-focus 보정을 통해 공정 견고성을 향상시킨다. IMEC의 실리콘 실험으로 실세계 효과를 검증하였으며, 공정 윈도우 35% 개선과 EPE 19% 감소를 달성한다.

## 주요 기여
- **57배 엔드-투-엔드 가속**: cuLitho 기반 가속 컴퓨팅으로 기존 CPU 기반 OPC 대비 57배 속도 향상
- **AI 고충실도 대리 모델**: AI를 계산 집약적 연산의 고충실도 대리 모델로 활용
- **Through-focus 보정 통합**: 공정 변동에 대한 견고성 향상을 위한 through-focus 보정
- **소프트웨어 스택 재설계**: 회절 광학, 계산 기하학, 다변수 최적화, 데이터 처리 핵심 프리미티브 전면 재설계
- **IMEC 실리콘 검증**: 산업 환경에서의 실제 실리콘 실험을 통한 검증

## 검증 방법론
- **실리콘 실험 검증**: IMEC에서 실제 반도체 제조 공정으로 알고리즘 결과 검증
- **엔드-투-엔드 성능 측정**: OPC 전체 파이프라인의 런타임 및 정확도 측정
- **공정 윈도우 분석**: 포커스-도즈 공정 윈도우 크기 비교 (기존 대비 35% 향상)
- **EPE 측정**: 웨이퍼 레벨 EPE를 목표값과 비교 (19% 감소)
- **에너지 효율 측정**: 전력 소비 및 탄소 발자국 감소량 정량화

## 검증 지표
- **EPE 허용 범위**: 기존 대비 19% EPE 감소 달성
- **공정 윈도우**: 기존 대비 35% 향상
- **속도**: 엔드-투-엔드 57배 가속 (AC 단독: 약 14배, AI 추가: 추가 ~1.7배)
- **사용 시뮬레이터**: NVIDIA cuLitho (GPU 가속 OPC 엔진)
- **검증 커버리지**: 전체 칩 규모 (1.6억 폴리곤, 22mm² 면적)

## OPC 툴 구현 관련성
SKOPC의 모델 OPC 및 전체 칩 검증 모듈 가속화에 직접 활용 가능:
1. **GPU OPC 가속**: cuLitho의 CUDA 기반 OPC 가속 기법을 SKOPC의 OPC 엔진에 적용
2. **AI 대리 모델 통합**: 계산 집약적 리소그래피 시뮬레이션을 AI 대리 모델로 대체하여 검증 속도 향상
3. **Through-focus 보정**: OPC 최적화 시 through-focus 정보를 포함한 공정 견고성 개선
4. **전체 칩 검증 확장성**: 수억 폴리곤 규모의 전체 칩 OPC 검증을 위한 확장 가능한 아키텍처
5. **에너지 효율**: GPU 가속으로 대용량 OPC 검증의 에너지 소비 감소

## 참고문헌 (핵심)
- NVIDIA cuLitho 기술 문서 및 관련 논문
- Sun et al. (2023) - GPU-ILT: GPU 가속 ILT 기준선
- Chen et al. (2024) - TorchLitho: 오픈소스 미분 가능 리소그래피 프레임워크
- IMEC EUV 리소그래피 관련 연구
- 컴퓨테이셔널 리소그래피 가속 관련 산업 논문

## 태그
`Verification`, `OPC`, `GPU Acceleration`, `cuLitho`, `NVIDIA`, `AI Surrogate`, `Full Chip`, `Process Window`, `EPE`, `Through-focus`, `Energy Efficiency`, `IMEC`, `2026`, `Industrial`
