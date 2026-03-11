# A Novel Flow of Full-Chip OPC Model Calibration and Verification by Utilizing SEM Image Contours

## 메타데이터
- **저자**: Yuan Gan, Changlian Yan, Mengqing Yu, Penghui Zhu, Jing Qiao, Lile Lu, Shengrui Zhang, Ming Ding, Chunying Han, Weijie Shi, Xiaojun Luo, Junhai Jiang, Zongchang Yu
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540K
- **DOI/URL**: https://doi.org/10.1117/12.3010034

## 핵심 요약
SEM 이미지 컨투어(contour)를 활용하여 풀칩 OPC 모델 교정 및 검증 품질을 향상시키는 혁신적인 흐름을 제안한다. 2D 컨투어 기반 대규모 교정 데이터로 기존 CD 측정 대비 더 적은 계측 시간으로 2D 패턴 예측 모델 정확도를 개선한다.

## 주요 기여
1. SEM 이미지 컨투어를 OPC 모델 교정 데이터로 직접 활용하는 혁신적 흐름 제안
2. 기존 CD 기반 교정 대비 2D 패턴 예측 정확도 향상
3. 대규모 2D 컨투어 데이터를 활용한 교정 게이지 패턴 커버리지 확대
4. 계측 시간 단축: CD 측정 없이 컨투어에서 직접 교정 데이터 추출
5. 교정 모델의 2D 형상 예측 능력과 풀칩 OPC 성능 평가

## 모델 수식/아키텍처
- **컨투어 기반 교정**: SEM contour → 다수의 CD 게이지 자동 추출
- 컨투어 추출 알고리즘: SEM 이미지 임계값 처리 + 에지 검출
- 교정 목적함수: RMSE(contour_simulated, contour_measured) 최소화
- 기존 CD 교정과 비교: 동일 레이아웃에서 더 많은 2D 교정 포인트 확보
- OPC 검증(verification) 단계에서도 컨투어 기반 EPE 평가 적용

## 모델 유형
- [x] 광학
- [x] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC 모델 교정 파이프라인의 데이터 수집 단계 개선에 직접 활용
- SEM 컨투어 자동 추출 → 교정 게이지 자동 생성 파이프라인 구현 참조
- 기존 CD-SEM 기반 교정의 병목(throughput) 문제 해결 방향 제시
- 2D 패턴(contact, 2D-bar 등) 모델 정확도 향상에 특히 유용

## 태그
`Model`, `Calibration`, `SEMContour`, `OPC`, `FullChip`, `2D`, `Metrology`, `SPIE`, `DTCO`
