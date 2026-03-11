# Compact 2D OPC Modeling of a Metal Oxide EUV Resist for a 7nm Node BEOL Layer

## 메타데이터
- **저자**: Adam Lyons, David Rio, Sook Lee, Thomas Wallow, Maxence Delorme, Anita Fumar-Pici, Michael Kocsis, Peter de Schepper, Michael Greer, Jason K. Stowers, Werner Gillijns, Danilo De Simone, Joost Bekaert
- **연도**: 2017
- **게재지**: Proc. SPIE 10143, Extreme Ultraviolet (EUV) Lithography VIII, 101431E
- **DOI/URL**: https://doi.org/10.1117/12.2260441

## 핵심 요약
Inpria의 직접 패터닝 가능한 금속산화물 하드마스크(MOR, Metal Oxide Resist)를 EUV 포토레지스트로 활용하여 N7 BEOL 블록 마스크 응용에 적용한 Tachyon 2D OPC 풀칩 모델을 구축한 논문. MOR 기반 EUV 레지스트에 대한 컴팩트 2D OPC 모델링 최초 사례 중 하나로, 7nm BEOL 레이어에서의 OPC 모델 정확도와 EUV 리소그래피 적용 가능성을 입증하였다.

## 주요 기여
1. **MOR EUV 레지스트 최초 컴팩트 2D OPC 모델**: Inpria MOR을 EUV 레지스트로 사용하는 N7 BEOL 레이어에 대한 Tachyon 기반 컴팩트 2D OPC 풀칩 모델 구축
2. **블록 마스크 응용 OPC 모델**: N7 BEOL 블록 마스크의 특수한 패턴 요구사항에 맞춘 OPC 모델 설계
3. **MOR 레지스트 특성의 OPC 모델 통합**: 직접 패터닝 금속산화물 하드마스크의 독특한 광화학적 특성을 OPC 컴팩트 모델에 반영
4. **7nm 노드 BEOL EUV 적용성 입증**: 7nm 기술 노드 BEOL 레이어에서 EUV + MOR 조합의 OPC 모델 실용성 검증
5. **imec-Inpria 산학연 협력 실증**: imec, Inpria, ASML, Synopsys 등 다기관 협력으로 EUV MOR OPC 생태계 구축

## 검증 방법론
- N7 BEOL 블록 마스크 레이아웃에서 Tachyon 2D OPC 모델 캘리브레이션
- MOR 레지스트 EUV 노광 웨이퍼의 CD-SEM 측정 데이터와 OPC 모델 예측 비교
- 풀칩 OPC 플로우에서 MOR 2D 모델 적용 시 EPE 분포 분석
- 기존 유기 CAR(Chemically Amplified Resist) 모델 대비 MOR 모델의 차이점 및 개선 사항 분석

## OPC 툴 구현 관련성
- SKOPC의 MOR/건식 레지스트 OPC 모델 지원 기능의 역사적 기반 논문
- `2024_Xu_OPC_model_dry_resist_lowk1_EUV_N5.md`, `2024_Chen_EUV_OPC_dry_photoresist_32nm_BEOL.md`의 MOR OPC 모델 계보의 선구 연구
- `2023_Lyons_mask_error_OPC_model_error_EUV.md`(동일 1저자)와 함께 Lyons 연구팀의 EUV OPC 모델 시리즈 구성
- SKOPC 레지스트 모델에 MOR 파라미터 세트를 별도 프리셋으로 추가할 때 기준 OPC 모델 정확도 벤치마크

## 태그
`Verification`, `SPIE`, `EUV`, `OPC Model`, `Metal Oxide Resist`, `MOR`, `7nm`, `BEOL`, `Tachyon`, `2D Model`, `Inpria`
