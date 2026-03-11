# Better Prediction on Patterning Failure Mode with Hotspot Aware OPC Modeling

## 메타데이터
- **저자**: Chih-I Wei, Stewart Wu, Yunfei Deng, Gurdaman Khaira, Ir Kusnadi, Germain Fenger, Seulki Kang, Yosuke Okamoto, Kotaro Maruyama, Yuichiro Yamazaki, Sayantan Das, Sandip Halder, Werner Gillijns, Gian Lorusso
- **연도**: 2021
- **게재지**: Proc. SPIE 11611, Metrology, Inspection, and Process Control for Semiconductor Manufacturing XXXV, 2583837
- **DOI/URL**: https://doi.org/10.1117/12.2583837

## 핵심 요약
리소그래피 실패 모드(핫스팟)에 민감한 OPC 모델 교정 방법을 제안한다. OPC 모델 커버리지와 정확도를 향상시켜 현상 후 검사(ADI) 패턴 핫스팟(트렌치 핀칭, 브리징 등)을 정밀 예측한다. 복잡한 2D 라우팅 패턴에서 특히 효과적이다.

## 주요 기여
1. 리소그래피 실패 모드에 민감한 핫스팟 인식(hotspot-aware) OPC 모델 교정
2. 트렌치 핀칭(pinching) 및 브리징(bridging) 등 ADI 핫스팟 예측 정확도 향상
3. 복잡한 2D 라우팅 패턴의 OPC 모델 커버리지 확대
4. 핫스팟 패턴을 교정 게이지에 우선 포함하는 샘플 플랜 전략
5. imec, TSMC, Synopsys 등 다기관 공동 연구 결과

## 모델 수식/아키텍처
- **핫스팟 인식 교정**:
  - 핫스팟 패턴 분류: 핀칭, 브리징, 넥킹, 섬(island) 형성
  - 핫스팟 가중치: 교정 목적함수에서 핫스팟 게이지에 높은 가중치 부여
  - RMSE_hs = w_hs · RMSE_hotspot + (1-w_hs) · RMSE_normal
- 교정 게이지 선택: 핫스팟 발생 취약 2D 패턴 우선 포함
- 검증: ADI SEM 이미지와 시뮬레이션 컨투어 비교

## 모델 유형
- [x] 광학
- [x] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC OPC 모델 교정 파이프라인의 핫스팟 인식 교정 기능 구현 참조
- OPC 검증(verification) 흐름에서 핫스팟 예측 정확도 향상 전략
- 2D 패턴 모델 정확도를 핫스팟 중심으로 개선하는 실용적 방법
- `2016_Hamouda_EtchAware_HotspotOPC.md`와 함께 핫스팟 방지 OPC 연구 계열

## 태그
`Model`, `OPC`, `Hotspot`, `Calibration`, `ADI`, `Pinching`, `Bridging`, `2D`, `imec`, `SPIE`
