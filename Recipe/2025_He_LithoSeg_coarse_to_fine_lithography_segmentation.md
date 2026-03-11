# LithoSeg: A Coarse-to-Fine Framework for High-Precision Lithography Segmentation

## 메타데이터
- **저자**: Xinyu He, Botong Zhao, Bingbing Li, Shujing Lyu, Jiwei Shen, Yue Lu
- **연도**: 2025
- **게재지/학회**: arXiv:2511.12005
- **DOI/URL**: https://arxiv.org/abs/2511.12005
- **라이선스**: CC BY-NC-ND 4.0
- **인용수**: N/A (2025년 출판)

## 핵심 요약
LithoSeg는 반도체 제조에서 리소그래피 SEM 이미지의 정밀 분할 및 측정을 위한 coarse-to-fine 프레임워크다. 코스 단계에서는 Human-in-the-Loop Bootstrapping과 SAM(Segment Anything Model)을 통해 최소한의 인간 감독으로 강건성을 달성하고, 파인 단계에서는 2D 분할을 1D 회귀 문제로 재공식화하여 경량 MLP로 정밀 보정을 수행한다. 기존 방법 대비 분할 정확도와 계측 정밀도를 동시에 향상시킨다.

## 주요 기여
- **Coarse-to-Fine 2단계 계층적 접근**: 거친 분할과 세밀한 정밀화를 단계적으로 처리
- **Human-in-the-Loop Bootstrapping**: SAM 활용으로 최소 인간 감독 하에 강건한 코스 분할
- **1D 회귀로 2D 분할 재공식화**: 홈 법선 프로파일 샘플링으로 분할을 회귀 문제로 변환
- **경량 MLP 정밀 보정**: 포인트별 정밀화에 경량 다층 퍼셉트론 활용

## Recipe/Process Flow 상세

### LithoSeg 2단계 파이프라인

**코스 단계 (Coarse Stage): Human-in-the-Loop Bootstrapping**

1. **SAM 기반 초기 분할**
   - Segment Anything Model(SAM)으로 SEM 이미지의 리소그래피 구조 거칠게 분할
   - 제한된 어노테이션으로 강건한 초기 마스크 생성

2. **Human-in-the-Loop 검토**
   - 낮은 신뢰도 예측에 인간 검토 개입
   - 부트스트랩 방식으로 점진적 어노테이션 확장
   - 반지도 학습으로 어노테이션 부담 감소

3. **코스 마스크 생성**
   - 전체 리소그래피 패턴 영역 경계 식별
   - 후속 파인 단계의 관심 영역(ROI) 정의

**파인 단계 (Fine Stage): 1D 회귀 기반 경계 정밀화**

1. **홈 법선 프로파일 샘플링**
   - 코스 마스크 경계에 수직(법선) 방향으로 1D 프로파일 샘플링
   - 경계선을 따라 등간격으로 샘플링 포인트 배치

2. **1D 회귀 문제 변환**
   - 2D 픽셀 분류 대신 1D 경계 위치 회귀
   - 각 법선 프로파일에서 정확한 경계 위치 예측

3. **경량 MLP 포인트별 정밀화**
   - 경량 다층 퍼셉트론(MLP)으로 각 샘플링 포인트 보정
   - 빠른 추론으로 실시간 SEM 이미지 처리 가능

4. **정밀화된 윤곽 생성**
   - 보정된 경계 포인트들을 연결하여 최종 고정밀 윤곽 생성
   - CD(Critical Dimension) 측정 정확도 향상

### 계측 정밀도 향상
- SEM 이미지에서 추출된 윤곽의 CD 측정 정확도 향상
- OPC 모델 캘리브레이션을 위한 고품질 계측 데이터 생성
- 다양한 리소그래피 패턴(라인/스페이스, 비아, 콘택트)에 적용 가능

## OPC 툴 구현 관련성
- **OPC 캘리브레이션 데이터 품질**: LithoSeg의 고정밀 SEM 윤곽으로 OPC 모델 캘리브레이션 데이터 품질 향상
- **CD 측정 자동화**: OPC 레시피 검증을 위한 자동 CD-SEM 측정 분석 파이프라인
- **반지도 학습 캘리브레이션**: 소수의 레이블된 SEM 이미지로 OPC 캘리브레이션 모델 학습
- **1D 프로파일 분석**: 경계 법선 프로파일 분석을 OPC EPE 계산에 활용
- **SegSEM과 상호보완**: SegSEM(SAM2 기반)과 LithoSeg(coarse-to-fine)를 앙상블하여 더 강건한 OPC 캘리브레이션 파이프라인 구성

## 참고문헌 (핵심)
- SAM (Segment Anything Model) - Kirillov et al.
- SEM 이미지 분할 관련 선행 연구
- 리소그래피 계측 관련 연구

## 태그
`LithoSeg`, `Coarse-to-Fine`, `SAM`, `SEM Segmentation`, `1D Regression`, `CD Measurement`, `Metrology`, `OPC Calibration`, `Recipe`, `OPC`, `Human-in-the-Loop`, `MLP`, `Lithography`
