# In-situ and Non-contact Etch Depth Prediction in Plasma Etching via Machine Learning (ANN & BNN) and Digital Image Colorimetry

## 메타데이터
- **저자**: Minji Kang, Seongho Kim, Eunseo Go, Donghyeon Paek, Geon Lim, Muyoung Kim, Soyeun Kim, Sung Kyu Jang, Min Sup Choi, Woo Seok Kang, Jaehyun Kim, Jaekwang Kim, Hyeong-U Kim
- **연도**: 2025
- **게재지/학회**: arXiv:2505.03826
- **DOI/URL**: https://arxiv.org/abs/2505.03826
- **인용수**: N/A (2025년 출판)

## 핵심 요약
플라즈마 에칭에서 절연 재료(SiO₂, Si₃N₄)의 에칭 깊이를 비접촉 인시튜 방식으로 실시간 예측하는 머신러닝 프레임워크다. ANN(인공 신경망)으로 기준 예측을 수행하고 BNN(베이지안 신경망)으로 불확실성을 정량화한다. 디지털 이미지 색도계(RGB) 데이터만으로도 강력한 성능을 제공하여 공정 파라미터 없이도 예측 가능하다.

## 주요 기여
- **이중 모델링 접근법**: 기준 예측용 ANN + 불확실성 정량화용 BNN
- **낮은 오류율**: 선형 기준 모델 대비 MSE 크게 감소
- **RGB 색도계 통합**: 명시적 공정 파라미터 없이도 강력한 성능 제공
- **불확실성 추정**: BNN이 인식론적 및 우연적 불확실성 모두 포착

## Recipe/Process Flow 상세

### 플라즈마 에칭 공정 모니터링 파이프라인

**시나리오 1: 공정 파라미터 기반 예측**
1. 플라즈마 에칭 공정 파라미터 수집
   - 에칭 가스 유량
   - 애싱 가스 유량
   - RF 전력
   - 압력
   - 온도
2. ANN/BNN으로 평균 에칭 깊이 예측
3. 불확실성 정량화 (BNN)

**시나리오 2: RGB 색도계 기반 예측**
1. 웨이퍼 표면 디지털 이미지 캡처 (비접촉)
2. RGB 채널 색도계 특성 추출
3. 명시적 공정 파라미터 없이 에칭 깊이 예측
4. 실시간 인시튜 모니터링 가능

### ANN 아키텍처
- 입력: 공정 파라미터 또는 RGB 색도계 값
- 히든 레이어: 다중 완전 연결 레이어
- 출력: 에칭 깊이 예측값
- 손실: MSE 최소화

### BNN 불확실성 정량화
- 베이지안 추론으로 가중치 분포 학습
- 예측 불확실성 = 인식론적 불확실성 + 우연적 불확실성
- 검증된 커버리지 분석으로 불확실성 신뢰성 확인

### 대상 재료
- SiO₂ (산화 실리콘)
- Si₃N₄ (질화 실리콘)
- 반도체 FEOL/BEOL 공정에서 핵심 절연체

## OPC 툴 구현 관련성
- **에칭 후 OPC 보정**: 플라즈마 에칭 깊이/바이어스 예측으로 OPC 레시피에서 에칭 후 패턴 변형 사전 보상
- **공정 모델 통합**: ANN 기반 에칭 모델을 OPC 레시피의 after-etch 공정 시뮬레이션 컴포넌트로 통합
- **인시튜 피드백 루프**: 에칭 공정 중 실시간 깊이 예측으로 OPC 레시피 파라미터 동적 조정
- **에칭 바이어스 캘리브레이션**: SiO₂/Si₃N₄ 층의 에칭 바이어스를 OPC 레시피 캘리브레이션 데이터로 활용
- **불확실성 기반 레시피 마진**: BNN 불확실성을 OPC 레시피의 공정 마진 설정에 활용

## 참고문헌 (핵심)
- 반도체 결함 감소 및 가상 계측 관련 응용 연구
- CNN 및 오토인코더 기반 제조 공정 제어 연구

## 태그
`Plasma Etching`, `Etch Depth`, `ANN`, `BNN`, `Bayesian`, `RGB Colorimetry`, `In-situ`, `Non-contact`, `SiO2`, `Si3N4`, `Recipe`, `OPC`, `Etch Bias`, `Process Control`, `FEOL`, `BEOL`
