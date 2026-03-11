# Aerial Imaging (AIMS) Based Computational Lithography Model Calibration and Mask Metrology for High-NA EUV

## 메타데이터
- **저자**: Nitesh Pandey, Stefan Hunsche, Adam Lyons, Christoph Hennerkes, Andreas Verch, Maximilian Albert, Grizelda Kersteen, Renzo Capelli, Werner Gillijns, Balakumar Baskaran, Joost Bekaert
- **연도**: 2023
- **게재지**: Proc. SPIE PC12751, Photomask Technology 2023
- **DOI/URL**: https://doi.org/10.1117/12.2688109

## 핵심 요약
ZEISS AIMS EUV 툴을 이용한 직접 aerial image 측정을 고-NA(0.55NA) EUV 리소그래피 컴퓨테이셔널 리소그래피 모델 캘리브레이션 및 마스크 메트롤로지에 적용한다. 기존 AIMS 기반 연구(2022년 동일 저자)를 고-NA EUV로 확장하며, 아나모픽(anamorphic) 이미징 특성이 캘리브레이션에 미치는 영향을 분석한다.

## 주요 기여
- 고-NA(0.55NA) EUV 아나모픽 시스템에서 aerial image 기반 OPC 모델 캘리브레이션 적용
- ZEISS AIMS EUV를 이용한 마스크 패턴 변동성의 정량적 메트롤로지 방법론
- EPE 버짓 관리를 위한 aerial image 기반 마스크 효과 정량화
- 고-NA EUV에서 강화된 aerial image 모델 캘리브레이션 중요성 분석
- 아나모픽 이미징 특성(x: 4×, y: 8× 배율차)이 캘리브레이션에 미치는 영향

## 모델 수식/아키텍처
- Aerial image 직접 측정값과 시뮬레이션 비교를 통한 모델 파라미터 최적화
- 아나모픽 광학계 TCC(Transmission Cross Coefficient) 수정 항 포함
- 마스크 3D 효과(M3D)와 aerial image 측정의 결합

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- 고-NA EUV OPC 모델 캘리브레이션 워크플로우에 직접 활용
- SKOPC의 EUV 모델링 확장 시 0.55NA 아나모픽 광학계 지원에 핵심 참조
- AIMS 메트롤로지 데이터를 OPC 캘리브레이션 루프에 통합하는 방법론

## 태그
`Model`, `SPIE`, `AIMS`, `EUV`, `High-NA`, `Anamorphic`, `Mask Metrology`, `Calibration`, `0.55NA`
