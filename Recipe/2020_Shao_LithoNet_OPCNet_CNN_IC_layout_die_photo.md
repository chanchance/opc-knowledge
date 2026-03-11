# From IC Layout to Die Photo: A CNN-Based Data-Driven Approach (LithoNet + OPCNet)

## 메타데이터
- **저자**: Hao-Chiang Shao, Chao-Yi Peng, Jun-Rei Wu, Chia-Wen Lin, Shao-Yun Fang, Pin-Yen Tsai, Yan-Hsiu Liu
- **연도**: 2020
- **게재지/학회**: arXiv:2002.04967
- **DOI/URL**: https://arxiv.org/abs/2002.04967
- **인용수**: 다수 인용

## 핵심 요약
LithoNet과 OPCNet으로 구성된 두 개의 상호 보완적 신경망으로 IC 제조 과정의 형상 변형을 예측하고 보정하는 데이터 기반 프레임워크다. LithoNet은 레이아웃 패턴-SEM 이미지 쌍에서 학습하여 제조 유도 형상 변형을 예측하며, 웨이퍼 파라미터를 잠재 벡터로 인코딩하여 파라메트릭 공정 변동을 모델링한다. OPCNet은 LithoNet과 협력하여 비용 집약적인 전통적 OPC를 대체하는 교정된 포토마스크를 생성한다.

## 주요 기여
- **LithoNet**: 웨이퍼 파라미터를 잠재 벡터로 표현하여 파라메트릭 변동을 모델링하는 리소그래피 시뮬레이터
- **OPCNet**: LithoNet과 협력하여 보정된 포토마스크를 생성하는 OPC 네트워크
- **통합 파이프라인**: 리소그래피 시뮬레이션과 OPC 보정을 단일 파이프라인으로 통합
- **SEM 기반 학습**: 실제 SEM 이미지와 레이아웃 설계 패턴 쌍으로 학습

## Recipe/Process Flow 상세

### LithoNet 아키텍처 및 학습

**입력**
- IC 레이아웃 이미지 (설계 패턴)
- 웨이퍼 파라미터 잠재 벡터 (파라메트릭 공정 변동 인코딩)

**LithoNet 구조**
- CycleGAN: 레이아웃-SEM 이미지 변환 (도메인 적응)
- U-Net: 변형 학습 (픽셀별 형상 변형 예측)
- 공정 조건 잠재 벡터: 초점, 도즈 등 공정 파라미터 인코딩

**출력**
- 예측된 웨이퍼 인쇄 형상 (SEM 이미지 유사)
- 제조 공정의 형상 변형 맵

### OPCNet 아키텍처 및 학습

**입력**
- 목표 IC 레이아웃 패턴
- LithoNet 피드백 (예측 인쇄 결과)

**OPCNet 구조**
- 레이아웃 → OPC 보정 마스크 직접 생성
- LithoNet을 손실 함수의 일부로 활용
- 인쇄 충실도 최대화를 위한 마스크 최적화

**출력**
- 보정된 포토마스크 (OPC 적용)
- 전통적 OPC보다 빠른 마스크 생성

### 통합 OPC 파이프라인

**단계 1: 데이터 수집**
- 다양한 레이아웃 패턴-SEM 이미지 쌍 수집
- 공정 파라미터(초점, 도즈) 기록

**단계 2: LithoNet 훈련**
- 레이아웃-SEM 쌍으로 CycleGAN 훈련
- U-Net으로 형상 변형 패턴 학습
- 공정 파라미터 잠재 벡터 임베딩

**단계 3: OPCNet 훈련**
- 훈련된 LithoNet 고정
- OPCNet이 LithoNet 피드백 기반 마스크 최적화 학습

**단계 4: 추론 (OPC 실행)**
1. 새 레이아웃 입력
2. OPCNet으로 초기 OPC 마스크 생성
3. LithoNet으로 예측 인쇄 결과 시뮬레이션
4. EPE 계산 및 마스크 품질 평가
5. 최종 OPC 마스크 출력

### 파라메트릭 공정 변동 모델링
- 초점 변동: 다양한 초점 조건에서의 인쇄 결과 예측
- 도즈 변동: 다양한 노광 도즈에서의 결과 예측
- 공정 창 분석: 여러 공정 조건에서 OPC 레시피 견고성 평가

## OPC 툴 구현 관련성
- **데이터 기반 OPC 모델**: SEM 측정 데이터로 학습한 LithoNet을 SKOPC OPC 레시피의 리소그래피 시뮬레이터로 통합
- **파라메트릭 공정 모델**: 공정 조건을 잠재 벡터로 인코딩하는 OPC 레시피의 공정 모델 설계
- **OPCNet 마스크 생성**: 딥러닝 기반 초기 마스크 생성으로 OPC 레시피 실행 가속화
- **SEM 캘리브레이션 루프**: SEM 이미지와 시뮬레이션 비교로 OPC 레시피 지속적 캘리브레이션
- **LithoHoD 연계**: 동일 저자의 LithoHoD 논문(2024)과 함께 OPC 핫스팟 감지 파이프라인 구성

## 참고문헌 (핵심)
- CycleGAN (Zhu et al., 2017)
- U-Net (Ronneberger et al., 2015)
- GAN-OPC (Yang et al., 2018)
- DAMO (Chen et al., 2020)

## 태그
`LithoNet`, `OPCNet`, `CNN`, `Data-driven`, `SEM`, `Shape Deformation`, `Die Photo`, `Process Variation`, `Latent Vector`, `Recipe`, `OPC`, `CycleGAN`, `U-Net`, `Parametric Model`
