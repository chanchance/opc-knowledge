# Optical Diffraction-based Convolution for Semiconductor Mask Optimization (OptiCo)

## 메타데이터
- **저자**: (저자명 확인 필요 — NeurIPS 2025 ML4PS 워크샵 게재)
- **연도**: 2025
- **게재지/학회**: NeurIPS 2025 Workshop on Machine Learning and the Physical Sciences (ML4PS)
- **DOI/URL**: https://ml4physicalsciences.github.io/2025/files/NeurIPS_ML4PS_2025_344.pdf
- **인용수**: 미확인

## 핵심 요약
광학 회절 원리를 신경망 아키텍처에 명시적으로 통합한 최초의 컨볼루션 신경망 프레임워크 OptiCo를 제안한다. 광학 회절 기반 컨볼루션(Optical Diffraction-based Convolution) 연산을 통해 광학 리소그래피에서의 빛의 거동을 효과적으로 시뮬레이션한다. 광학 위상(Optical Phase, OP) 커널이 빛 전파로 인한 공간적 위상 변화를 인코딩하며, MetaNeXt 기반 백본과 OP 복소 컨볼루션을 통합한 OptiCo 블록을 구성한다. LithoBench 벤치마크에서 대부분의 평가 지표와 하위 태스크에서 우수한 성능을 달성한다.

## 주요 기여
- **최초의 회절 기반 CNN 프레임워크**: 광학 회절 물리를 CNN 핵심 연산에 직접 통합
- **광학 위상(OP) 커널**: 빛 전파의 공간적 위상 변화를 인코딩하는 새로운 커널 설계
- **OptiCo 블록**: MetaNeXt 백본과 OP 복소 컨볼루션을 통합한 기본 구성 단위
- **복소 컨볼루션**: 광학 시스템의 복소 진폭 표현을 신경망에서 처리
- **LithoBench 최고 성능**: 최신 컴퓨테이셔널 리소그래피 벤치마크에서 대부분의 지표에서 우수

## 검증 방법론
- **LithoBench 벤치마크**: 최신 컴퓨테이셔널 리소그래피 벤치마크로 성능 평가
- **합성 및 실세계 설계 포함**: LithoBench의 합성 패턴과 실세계 IC 설계 패턴 모두 평가
- **다중 하위 태스크 평가**: 리소그래피 시뮬레이션과 마스크 최적화 두 가지 하위 태스크에서 평가
- **기존 방법 비교**: GAN-OPC, DAMO, CFNO 등 기존 최고 성능 방법들과 비교
- **회절 통합 절제 연구**: OP 커널 제거 시 성능 저하 측정으로 물리 통합 효과 정량화

## 검증 지표
- **EPE 허용 범위**: LithoBench 벤치마크의 EPE 위반 수 기준
- **L2 오차**: 리소그래피 시뮬레이션 픽셀 오차
- **PVB (Process Variation Band)**: 마스크 최적화 결과의 공정 변동 견고성
- **Shots**: 마스크 복잡도 지표
- **사용 시뮬레이터**: LithoBench 벤치마크 리소그래피 시뮬레이터 (45nm)
- **검증 커버리지**: LithoBench 전체 데이터셋 (합성 + 실세계 패턴)

## OPC 툴 구현 관련성
SKOPC의 리소그래피 시뮬레이션 및 OPC 최적화 모듈에 다음과 같이 활용 가능:
1. **회절 기반 OPC 커널**: OptiCo의 OP 커널을 SKOPC의 OPC 신경망 모델에 통합
2. **물리적으로 정합한 시뮬레이션**: 회절 물리를 명시적으로 인코딩한 리소그래피 시뮬레이터 구현
3. **복소 진폭 처리**: 광학 이미징의 복소 진폭을 직접 처리하는 OPC 검증 엔진
4. **MetaNeXt 효율적 백본**: 최신 고효율 MetaNeXt 아키텍처를 OPC 신경망 백본으로 채택
5. **위상 이동 마스크(PSM) 최적화**: OP 커널의 위상 인코딩으로 PSM 최적화에 직접 적용

## 참고문헌 (핵심)
- Liu et al. (2022) - MetaNeXt: 효율적 네트워크 아키텍처
- LithoBench (Zheng et al., 2023) - NeurIPS 2023 컴퓨테이셔널 리소그래피 벤치마크
- Hopkins 이미징 모델 관련 광학 리소그래피 이론
- Yang & Ren (2023) - 물리 영감 AI 리소그래피 (ASPDAC 2023)
- 복소 컨볼루션 신경망 관련 참고문헌

## 태그
`Verification`, `OPC`, `Optical Diffraction`, `Convolution`, `CNN`, `Physics-Inspired`, `Complex Convolution`, `Phase Kernel`, `NeurIPS`, `ML4PS`, `2025`, `LithoBench`, `Mask Optimization`, `MetaNeXt`
