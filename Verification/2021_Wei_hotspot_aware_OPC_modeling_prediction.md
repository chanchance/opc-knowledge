# Better Prediction on Patterning Failure Mode With Hotspot Aware OPC Modeling

## 메타데이터
- **저자**: Chih-I Wei, Stewart Wu, Yunfei Deng, Gurdaman Khaira, Ir Kusnadi, Germain Fenger, Seulki Kang, Yosuke Okamoto, Kotaro Maruyama, Yuichiro Yamazaki, Sayantan Das, Sandip Halder, Werner Gillijns, Gian Lorusso
- **연도**: 2021
- **게재지**: Proc. SPIE 11611, Metrology, Inspection, and Process Control for Semiconductor Manufacturing XXXV, 1161112
- **DOI/URL**: https://doi.org/10.1117/12.2583837
- **인용수**: 다수 (Siemens EDA + imec 협력, OPC 모델 핫스팟 인식 분야 기준 논문)

## 핵심 요약
LFoV(Large Field of View) e-빔 검사를 활용한 OPC 모델 캘리브레이션 방법으로, 리소그래피 실패 모드에도 민감하게 반응하는 모델을 구축한다. ADI(After Development Inspection) 패턴 핫스팟(트렌치 핀칭, 브리징 등 복잡한 2D 라우팅 패턴)의 예측 정확도 향상을 위해 핫스팟 위치의 추가 샘플링 계획과 웨이퍼 컨투어 입력 데이터를 도입한다. 핫스팟 인식 OPC 모델은 기존 주요 피처 OPC 모델 대비 더 높은 ADI 핫스팟 포착률을 달성한다.

## 주요 기여
1. LFoV e-빔 검사 기반 웨이퍼 핫스팟 컨투어를 OPC 모델 캘리브레이션에 통합 — 핫스팟 인식 모델 구축
2. 핫스팟 위치 추가 샘플링 계획으로 OPC 모델 커버리지 확장
3. 개선된 훈련 알고리즘으로 LFoV e-빔에서 미세 컨투어 추출
4. 핫스팟 인식 OPC 모델이 기존 모델 대비 ADI 핫스팟 포착률 향상 실증

## 검증 방법론
- **LFoV e-빔 컨투어 추출**: 넓은 시야의 e-빔 검사로 웨이퍼 핫스팟 패턴의 고해상도 컨투어 추출
- **핫스팟 인식 OPC 모델 캘리브레이션**:
  - 기존 CD-SEM 측정 데이터 + LFoV 핫스팟 컨투어 데이터를 혼합하여 모델 훈련
  - 핫스팟 위치의 가중치를 높여 실패 모드 재현 능력 강화
- **ADI 핫스팟 예측 검증**:
  - 대상 실패 모드: 트렌치 핀칭(Trench Pinching), 브리징(Bridging), 2D 라우팅 패턴 변형
  - 예측된 핫스팟 컨투어와 실제 웨이퍼 컨투어 비교
  - 포착률(Capture Rate): 핫스팟 인식 모델 vs. 기존 모델
- **평가 지표**:
  - ADI 핫스팟 포착률 향상 (Capture Rate improvement)
  - 핫스팟 컨투어 재현 오차 (Contour Reproduction Error)
  - 핫스팟/비핫스팟 패턴에서의 EPE 분포

## 검증 지표
- EPE 허용 범위: ADI 핫스팟 판정 기준 (실패 모드별 CD 한계값)
- 시뮬레이터: Siemens EDA Calibre 핫스팟 인식 OPC 모델 + LFoV e-빔 컨투어
- 커버리지: 복잡한 2D 라우팅 패턴 핫스팟 — 다양한 트렌치/비아 패턴

## OPC 툴 구현 관련성
- **OPC 모델 캘리브레이션에 핫스팟 인식 기능 추가**: `ModelingEngine`의 OPC 모델 캘리브레이션 파이프라인에 핫스팟 위치 추가 샘플링 및 가중치 학습을 통합하는 구현 근거
- LFoV e-빔 컨투어 데이터를 OPC 모델 훈련에 활용하는 데이터 파이프라인 설계 방법 제공
- 핫스팟 인식 OPC 모델과 일반 OPC 모델의 성능 트레이드오프 분석 — 캘리브레이션 전략 선택 기준
- imec + Siemens EDA + TSMC/삼성 등 파운드리 협력 기반의 실무 검증 방법론

## 참고문헌
- SPIE Metrology, Inspection, and Process Control for Semiconductor Manufacturing XXXV 2021, Vol. 11611
- Siemens EDA Calibre OPC 모델 관련 기술 문서
- imec EUV 공정 연구 데이터

## 태그
`Verification`, `SPIE`, `OPCModel`, `HotspotAware`, `Calibration`, `LFoV`, `EBeam`, `Contour`, `ADI`, `CaptureRate`, `PinchBridge`, `PostOPC`
