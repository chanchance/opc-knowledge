# Thick-Mask Model Based on Multi-Channel U-Net for EUV Lithography

## 메타데이터
- **저자**: Chengzhen Yu, Xu Ma
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 1249525
- **DOI/URL**: https://doi.org/10.1117/12.2657246

## 핵심 요약
EUV 리소그래피에서 마스크 두께(thick-mask) 효과를 빠르게 시뮬레이션하기 위해 다중 채널 U-Net(MCU-Net) 기반 두꺼운 마스크 모델을 제안한다. 엄밀한 EM 시뮬레이션을 대체하여 M3D 효과를 포함한 빠른 마스크 필드 계산이 가능하다.

## 주요 기여
1. 다중 채널 U-Net(MCU-Net) 아키텍처를 EUV 두꺼운 마스크 모델에 적용
2. 엄밀한 FDTD/RCWA 시뮬레이션 데이터로 MCU-Net 학습
3. 전통적인 thin-mask 근사 대비 M3D 효과 정확도 대폭 향상
4. 풀칩 OPC에 적용 가능한 런타임으로 EUV 마스크 필드 시뮬레이션 가속
5. 다양한 마스크 재료 및 구조에 대한 일반화 능력 평가

## 모델 수식/아키텍처
- **MCU-Net 구조**:
  - 입력 채널: 마스크 레이아웃 (binary) + 입사각 정보 + 재료 광학 상수
  - 인코더: 다운샘플링 컨볼루션 블록 (마스크 패턴 특징 추출)
  - 디코더: 업샘플링 블록 + skip connection (마스크 필드 복원)
  - 출력: 복소 마스크 투과 필드 (진폭 + 위상) 또는 M3D 보정 계수
- 손실 함수: 엄밀 시뮬레이션 대비 필드 오차 (MSE in complex domain)
- 다중 채널 입력으로 편광(TE/TM) 의존성 동시 학습

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [x] ML/DL
- [x] 하이브리드 (CNN이 물리 기반 M3D 시뮬레이션 대체)

## OPC 툴 구현 관련성
- SKOPC EUV OPC 모듈의 M3D/EMF 계산을 MCU-Net으로 가속 가능
- EUV 0.33NA 및 0.55NA 마스크의 thick-mask 효과 처리에 적용
- 기존 `2024_Ju_PINN_Mask3D_Lithography.md`, `2025_Hybrid_ML_M3D_MaskModel.md`와 상보적
- 마스크 설계 규칙 검증(MRC) 및 OPC 검증(OPC verification) 흐름에 통합 가능

## 태그
`Model`, `M3D`, `ThickMask`, `UNet`, `EUV`, `CNN`, `DeepLearning`, `MaskModel`, `SPIE`, `DTCO`
