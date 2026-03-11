# OPC Model Accuracy Study Using High Volume Contour Based Gauges and Deep Learning on Memory Device

## 메타데이터
- **저자**: Kim et al. (삼성전자 / SK하이닉스)
- **연도**: 2019
- **게재지**: Proc. SPIE 10959, Metrology, Inspection, and Process Control for Microlithography XXXIII, 1095913
- **DOI/URL**: https://doi.org/10.1117/12.2515274

## 핵심 요약
메모리 소자 OPC 모델 정확도를 고용량 윤곽(contour) 기반 gauge와 딥러닝을 결합하여 크게 향상시키는 방법을 제안한다. 빠른 eBeam 계측 도구와 소프트웨어로 10K 이상의 윤곽 기반 EP(Edge Placement) gauge를 생성하고, 딥 뉴럴 네트워크(DNN)와 물리 지도 모델(physical guidance model)을 결합한 정규화 기법으로 기존 방법 대비 모델 정확도를 47% 이상 향상시킨다.

## 주요 기여
1. **고용량 윤곽 기반 Gauge**: eBeam 계측으로 10K+ 윤곽 기반 EP gauge를 TAT 증가 없이 생성
2. **DNN + 물리 모델 정규화**: 딥 뉴럴 네트워크에 물리 지도 모델로 정규화하여 과적합 방지
3. **47%+ 모델 정확도 향상**: 검증 gauge에서 기존 방법 대비 47% 이상 정확도 향상
4. **메모리 소자 특화**: 메모리 디바이스 OPC 모델 캘리브레이션에 최적화된 접근법
5. **계측-모델링 통합**: 고용량 eBeam 계측과 ML 모델 캘리브레이션의 효율적 통합 플로우

## Recipe/Flow 상세
- **고용량 Contour Gauge + DNN OPC 모델 플로우**:
  1. **고용량 Contour Gauge 생성**:
     - 빠른 eBeam SEM 도구로 다수 패턴의 윤곽 이미지 수집
     - 자동 윤곽 추출 소프트웨어로 10K+ EP gauge 생성
     - 다양한 패턴 환경(피치, 크기, 방향)의 대표성 있는 gauge 세트
  2. **Gauge 전처리**:
     - 윤곽 노이즈 필터링 및 품질 검사
     - EP gauge 위치 및 방향 정규화
     - 물리적으로 이상한 gauge 자동 제거
  3. **DNN 모델 학습**:
     - 입력: 광학 이미지 특징 (공중 이미지 픽셀 값)
     - 출력: CD / EP 예측
     - 물리 지도 모델(physical guidance): DNN 정규화 항으로 사용
     - 과적합 방지: 물리 모델 일관성 제약으로 일반화 향상
  4. **모델 검증**:
     - 홀드아웃 1.4K+ 검증 gauge에서 모델 정확도 측정
     - 기존 방법(적은 gauge + 물리 모델만) 대비 47%+ 향상 확인
     - 다양한 패턴 환경에서 일반화 성능 검증
  5. **OPC 적용**:
     - 향상된 DNN OPC 모델로 메모리 레이어 OPC 수행
     - ORC(Optical Rule Check)로 OPC 결과 검증
- **고용량 Gauge의 중요성**:
  - 적은 gauge로는 DNN 과적합 → 고용량 필요
  - 물리 모델 없이 DNN만으로는 물리적 일관성 미보장
  - 물리 + DNN 결합으로 정확도와 일반화 모두 달성
- **메모리 소자 특성**: 규칙적 어레이 패턴 + 다양한 크기 컨택/비아가 혼재

## OPC 툴 구현 관련성
- SKOPC OPC 모델 캘리브레이션에서 DNN + 물리 모델 하이브리드 구현
- `contour_gauge_dnn_model.py`: 윤곽 gauge 처리, DNN 학습, 물리 정규화
- eBeam 계측 데이터 자동 처리 및 대용량 gauge 관리 파이프라인
- 메모리 OPC 모델 정확도 47%+ 향상 전략 참고

## 태그
`OPC`, `ModelAccuracy`, `DeepLearning`, `ContourGauge`, `Memory`, `DRAM`, `eBeam`, `Metrology`, `NeuralNetwork`, `SPIE`, `2019`
