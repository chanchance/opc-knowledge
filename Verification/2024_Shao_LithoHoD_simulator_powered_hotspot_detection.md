# LithoHoD: A Litho Simulator-Powered Framework for IC Layout Hotspot Detection

## 메타데이터
- **저자**: Hao-Chiang Shao, Guan-Yu Chen, Yu-Hsien Lin, Chia-Wen Lin, Shao-Yun Fang, Pin-Yian Tsai, Yan-Hsiu Liu
- **연도**: 2024
- **게재지/학회**: arXiv:2409.10021 (September 2024)
- **DOI/URL**: https://arxiv.org/html/2409.10021v1
- **인용수**: N/A (2024년 출판)
- **소속**: National Chung Hsing University, National Tsing Hua University, National Taiwan University of Science and Technology, United Microelectronics Corporation (UMC)

## 핵심 요약
LithoHoD는 리소그래피 시뮬레이터(LithoNet)와 객체 검출기(RetinaNet)를 통합하는 시뮬레이터 기반 IC 레이아웃 핫스팟 감지 프레임워크다. 기존 학습 기반 감지기가 알려진 결함 패턴만 인식하는 한계를 극복하여, 제조 유도 형상 변형 맵과 패턴 인식 능력을 결합함으로써 새로운 패턴에 대한 일반화 성능을 향상시킨다.

## 주요 기여
- **시뮬레이터 기반 아키텍처**: LithoNet 리소그래피 시뮬레이터와 RetinaNet 객체 검출 백본을 통합
- **CMF(Cross-Model Feature Fusion)**: 형상 변형 피처와 감지 피처를 통합하는 교차 주의 블록 설계
- **향상된 일반화**: 레이아웃, 제조 결과, 핫스팟 ground truth 간의 관계 학습으로 새로운 패턴 감지 향상
- **실세계 검증**: UMC 20K 데이터셋에서 디지털~아날로그 6개 회로 설계 서브셋에서 강건성 입증

## 검증 방법론

### 2단계 훈련 프로세스

**사전 훈련 (Pre-training)**
1. 쌍으로 구성된 레이아웃 및 SEM(주사전자현미경) 이미지로 LithoNet 훈련
2. LithoNet이 제조 공정에 의한 회로 형상 변형을 나타내는 픽셀별 변위 벡터 생성 학습
3. 리소그래피 물리학 기반 지식을 신경망에 내재화

**주 훈련 (Main Training)**
1. 사전 훈련된 LithoNet이 변형 맵 예측
2. CMF 모듈을 통해 변형 피처와 RetinaNet 레이아웃 피처 융합
3. 세 가지 피라미드 레벨(P3-P5)에서 동시 처리
4. 결합 손실 함수로 최적화:
   - α-balanced focal loss (분류)
   - Huber loss (경계 박스 회귀)
   - Distance-IoU loss (λ=0.02 가중치)

### 핵심 컴포넌트 아키텍처

**LithoNet (리소그래피 시뮬레이터)**
- 입력: IC 레이아웃 이미지
- 출력: 픽셀별 변위 벡터 (제조 형상 변형 표현)
- 역할: 리소그래피 공정 지식을 특징 공간으로 인코딩

**수정된 RetinaNet 백본**
- ResNet과 FPN 사이에 채널별 주의 모듈 추가
- 단순화된 FPN (P3-P5, 기존 P1-P7 대비)
- 다중 해상도 피처 추출 지원

**CMF (Cross-Model Feature Fusion) 모듈**
- 2개 자기 주의 블록: 개별 피처 텐서 향상
- 교차 주의 블록: 변형 가이던스를 감지 네트워크로 전달
- 세 가지 피라미드 레벨에서 동시 동작
- 학습 가능한 피처 가중치 파라미터 ξ (초기값 1)

### 실험 결과

**ICCAD16 데이터셋**
- 평균 재현율: 0.963 (ResNet-34 변형)
- BBL-HoD, R-HSD, FCN-HoD 방법 일관되게 능가

**UMC20K 실세계 데이터셋**
- 평균 재현율: 0.889 (ResNet-18 변형)
- 오경보 수 최신 방법 대비 효과적 감소
- 6개 회로 설계 서브셋(디지털~아날로그)에서 강건성 입증

**핵심 발견**: 이진 다각형 특성으로 인해 자연 이미지 대비 IC 레이아웃 감지 태스크에서 얕은 ResNet 백본(ResNet-18)이 더 우수

## 검증 지표
- **재현율**: ICCAD16 0.963, UMC20K 0.889
- **사용 시뮬레이터**: LithoNet (리소그래피 형상 변형 시뮬레이터)
- **검증 커버리지**: ICCAD16 벤치마크 + UMC 20K 실세계 데이터셋 (디지털~아날로그 6종)
- **비교 기준선**: BBL-HoD, R-HSD, FCN-HoD

## OPC 툴 구현 관련성
- **OPC 후 핫스팟 검증**: OPC 레시피 실행 완료 후 핫스팟 자동 감지 및 리포팅 모듈 구현에 LithoHoD 아키텍처 참조
- **리소그래피 시뮬레이터 통합**: OPC 흐름의 검증 단계에서 LithoNet과 같은 경량 시뮬레이터 활용
- **파운드리 데이터 활용**: UMC 실세계 데이터를 기반으로 파운드리별 OPC 레시피 검증 데이터셋 구축
- **SEM 이미지 기반 보정**: SEM 측정 이미지와 시뮬레이션 비교를 통한 OPC 레시피 캘리브레이션 루프
- **다중 레이어 핫스팟 감지**: 디지털/아날로그 혼합 설계에서의 레이어별 OPC 레시피 적용 검증

## 참고문헌 (핵심)
- LithoNet (prior simulator framework)
- Lin et al. (2019): RetinaNet focal loss
- Feature Pyramid Networks (FPN) for object detection
- ICCAD16 hotspot detection benchmark dataset

## 태그
`LithoHoD`, `Hotspot Detection`, `Lithography Simulator`, `RetinaNet`, `CMF`, `Feature Fusion`, `OPC Verification`, `Verification`, `OPC`, `UMC`, `SEM`, `IC Layout`, `DfM`
