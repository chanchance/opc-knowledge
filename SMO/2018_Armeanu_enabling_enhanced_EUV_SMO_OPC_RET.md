# Enabling Enhanced EUV Lithographic Performance Using Advanced SMO, OPC, and RET

## 메타데이터
- **저자**: Ana Armeanu, Vicky Philipsen, Fan Jiang, Germain Fenger, Neal Lafferty, Werner Gillijns, Eric Hendrickx, John Sturtevant
- **연도**: 2018 (출판일: 2019-01-02)
- **게재지**: Proc. SPIE 10809, International Conference on Extreme Ultraviolet Lithography 2018
- **DOI/URL**: https://doi.org/10.1117/12.2502809

## 핵심 요약
현재 산업 표준인 TaBN(탄탈룸 질화물) 기반 EUV 마스크 흡수층(60nm)이 웨이퍼 수준에서 강한 3D 전자기장(EMF) 효과(그림자 효과, 피치 의존 최적 초점 이동 등)를 유발함을 분석하고, 대안적 마스크 흡수층(high-k absorber, attPSM) 도입과 고급 SMO/OPC/RET 기법을 결합하여 EUV 리소그래피 성능을 향상시키는 방법을 제시한다.

## 주요 기여
1. **대안적 마스크 흡수층 평가**: High-k EUV 흡수층 및 감쇠 위상 이동 마스크(attPSM) 삽입 옵션 제시
2. **3D EMF 효과 완화**: 얇은 흡수층 또는 높은 EUV 소멸 계수 재료로 마스크 3D 효과 저감
3. **Proteus SMO 적용**: M3D 효과 및 레지스트 특성을 포함한 공동 최적화 방법론 검증
4. **파운드리 N5 노드 적용**: 실제 로직 디자인에 대한 EUV 성능 향상 시연

## 알고리즘/수식
- **Proteus SMO**: 마스크 3D(M3D) 효과를 포함한 소스-마스크 공동 최적화 수행
  - NXE M3D+ 모델: 반사형 3D 마스크 효과를 정확히 예측하는 빠른 모델
  - 새로운 동공 대칭성 및 마스크 디포커스 최적화 활성화
- **비용 함수**: 웨이퍼 이미지 예측과 실제 웨이퍼 프린팅 간 오차 최소화
  - CD 균일성, EPE, 노출 위도(EL), 공정 창(PW) 최적화
- **M3D 보상 전략**:
  - SMO 소스 재최적화로 best-focus 이동 보상
  - OPC bias 조정으로 CD 오차 보정
  - RET(해상도 향상 기술): SRAF 삽입 최적화

## OPC 툴 SMO 구현 관련성
- EUV SMO에서 M3D 효과를 반드시 고려해야 함을 시사
- 고급 비용 함수 설계: 노출 위도, 공정 창, MEF를 동시 고려
- Proteus SMO 방법론은 상용 툴 구현의 참조 아키텍처
- N5 노드 이하에서 attPSM + SMO 결합의 필요성 확인

## 태그
`SMO`, `EUV`, `OPC`, `RET`, `M3D`, `mask_absorber`, `attPSM`, `SPIE`, `N5_node`
