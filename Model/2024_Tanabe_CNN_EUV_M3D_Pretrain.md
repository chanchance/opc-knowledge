# Pre-training CNN for Fast EUV Lithography Simulation Including M3D Effects

## 메타데이터
- **저자**: Hiroyoshi Tanabe, Akira Jinguji, Atsushi Takahashi
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III
- **DOI/URL**: https://doi.org/10.1117/12.3009880

## 핵심 요약
EUV 리소그래피 시뮬레이션 가속을 위해 마스크 3D(M3D) 효과를 포함한 CNN 사전학습(pre-training) 기법을 제안한다. 엄밀한 전자기 시뮬레이션 데이터로 CNN을 사전학습하여 M3D 효과가 반영된 빠른 시뮬레이션을 가능하게 한다.

## 주요 기여
1. M3D 효과 포함 EUV 시뮬레이션을 위한 CNN 사전학습 전략 제시
2. 엄밀한 EM 시뮬레이션 데이터를 활용한 CNN 학습 데이터셋 구성 방법
3. 사전학습 후 미세조정(fine-tuning)으로 실제 공정 조건 적응
4. M3D 효과 미포함 대비 시뮬레이션 정확도 향상 정량화
5. EUV 0.33NA 및 0.55NA 조건에서의 성능 평가

## 모델 수식/아키텍처
- **CNN 구조**: 마스크 레이아웃 패치 → 컨볼루션 레이어 → 웨이퍼 이미지 출력
- 사전학습: 엄밀한 FDTD/RCWA 기반 M3D 시뮬레이션 데이터로 학습
- M3D 효과 인코딩: 마스크 두께, 재료 광학 상수, 입사각 의존성을 학습
- 미세조정: 실제 웨이퍼 SEM 데이터 또는 상업 시뮬레이터 결과로 적응

## 모델 유형
- [x] 광학 (M3D 포함)
- [ ] 레지스트
- [x] ML/DL
- [x] 하이브리드 (물리 기반 M3D + CNN)

## OPC 툴 구현 관련성
- EUV OPC 흐름에서 M3D 효과를 낮은 계산 비용으로 포함하는 핵심 기술
- SKOPC의 M3D 보정 모듈(EMF 커널 대체)에 CNN 접근법 적용 가능
- 사전학습 전략은 제한된 학습 데이터 환경에서도 적용 가능
- Tanabe 2021/2024 시리즈의 EUV CNN 시뮬레이션 연구 후속작

## 태그
`Model`, `EUV`, `CNN`, `M3D`, `PreTraining`, `MaskModel`, `FastSimulation`, `SPIE`, `DTCO`
