# Inverse Lithography OPC Correction with Multiple Patterning and Etch Awareness

## 메타데이터
- **저자**: Heon Choi, Ayman Hamouda
- **연도**: 2018
- **게재지**: Proc. SPIE 10587, Optical Microlithography XXXI, 105870O
- **DOI/URL**: https://doi.org/10.1117/12.2297368

## 핵심 요약
멀티패터닝(LELELE: Litho-Etch×3) 공정에 etch 보정 인식(etch awareness)을 통합한 ILT(Inverse Lithography Technology) OPC 방법론을 제안한 논문. DUV 파장에서 서브-파장 치수로 진입하면서 ILT를 단일 노광 마스크 최적화를 넘어 멀티패터닝 OPC에 적용하는 최초의 실용적 시도 중 하나로, 3노광 메탈 레이어에서 ILT 마스크 최적화의 효과를 검증하였다.

## 주요 기여
1. **멀티패터닝 ILT(MP-ILT) 구현**: 3노광 LELELE 공정에 ILT 마스크 최적화를 적용하는 MP-OPC 프레임워크
2. **Etch Awareness 통합**: ILT 최적화 루프 내에 etch 편차(etch bias) 모델을 통합하여 post-etch 웨이퍼 패턴을 최적화 목표로 설정
3. **ILT vs. 기존 OPC 비교**: 동일 멀티패터닝 조건에서 ILT와 기존 모델기반 OPC의 EPE, 공정 윈도우, 마스크 복잡도 비교
4. **LELELE 메탈 레이어 실증**: 실제 메탈 레이어 레이아웃에서 3노광 ILT OPC 효과 검증
5. **MP-ILT 런타임 분석**: 3노광 ILT의 계산 비용과 공정 마진 개선 간의 트레이드오프 정량화

## 검증 방법론
- 3노광 LELELE 메탈 레이어 레이아웃 대상 ILT와 기존 OPC 결과 비교
- EPE 분포, 공정 윈도우(도즈-포커스 마진) 비교
- Etch 보정 포함/미포함 ILT의 post-etch 웨이퍼 패턴 예측 정확도 비교
- 마스크 복잡도(mask complexity) 지표 비교 (ILT 커비리니어 vs. 기존 맨해튼 OPC)

## OPC 툴 구현 관련성
- SKOPC의 ILT 모듈과 멀티패터닝 공정 연동 설계 시 핵심 참조
- `2021_Hooker_ML_etch_model_OPC_ILT.md`(기수집)의 선행 연구로, ILT+etch 통합 계보 형성
- `2016_Hamouda_combining_mask_OPC_verification_yield.md`(신규)와 같은 저자(Hamouda)의 OPC 검증 방법론 발전 추적
- SKOPC Recipe Runner에서 LELELE 공정 플로우 지원 시 ILT 단계 파라미터 설계 기준

## 태그
`Verification`, `SPIE`, `ILT`, `Multi-Patterning`, `LELELE`, `Etch Awareness`, `OPC`, `DUV`, `Curvilinear`
