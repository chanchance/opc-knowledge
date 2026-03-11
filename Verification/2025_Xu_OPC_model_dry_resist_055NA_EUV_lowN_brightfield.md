# OPC Model Accuracy of Dry Resist Readiness for 0.55NA EUVL by Using Low-n Bright Field Mask

## 메타데이터
- **저자**: Dongbo Xu, Werner Gillijns, Shruti Jambaldinni, Soobin Hwang, Anuja De Silva, Germain Fenger
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250Y
- **DOI/URL**: https://doi.org/10.1117/12.3051855
- **소속**: imec, Siemens EDA

## 핵심 요약
0.55NA 고NA EUV 리소그래피 도입을 앞두고 음성 톤 금속산화물 레지스트(MOR, Metal Oxide Resist)와 저굴절률(low-n) 감쇠 위상천이마스크(bright field attenuated PSM)를 결합한 드라이 레지스트 공정의 OPC 모델 정확도를 조사한다. imec N2 노드(피치 28nm) 금속 설계에서 NXE:3400 스캐너를 사용하여 수천 개의 OPC 관련 피처를 ADI(After-Develop Inspection) 및 AEI(After-Etch Inspection) SEM으로 측정하고 OPC 모델 정확도를 정량화한다.

## 주요 기여
1. 0.55NA EUVL용 드라이 레지스트 + low-n 밝은 필드 마스크 조합의 OPC 모델 정확도 최초 정량화
2. imec N2 피치 28nm 금속 레이어에서의 포괄적 OPC 모델 검증
3. ADI + AEI 양방향 SEM 측정을 통한 OPC 모델 정확도 평가 방법론
4. 0.55NA EUV 제조 도입을 위한 드라이 레지스트 OPC 준비도(readiness) 평가
5. 음성 톤 MOR + low-n mask 조합의 OPC 고유 특성 분석

## 검증 방법론
- **노광기**: imec NXE:3400 EUV 스캐너 (0.33NA)
- **목표 공정**: 0.55NA EUVL 준비도 평가
- **마스크 유형**: Low-n 감쇠 위상천이마스크 (bright field)
- **레지스트**: 음성 톤 금속산화물 레지스트(MOR) 드라이 현상 공정
- **기술 노드**: imec N2, 피치 28nm 금속 설계
- **측정 방법**: HITACHI CD-SEM (ADI + AEI 양방향)
- **샘플 크기**: 수천 개의 OPC 관련 피처 측정
- **평가 지표**: OPC 모델 정확도 (EPE, CD 예측 오차)

## OPC 툴 구현 관련성
- 0.55NA 고NA EUV 도입 시 드라이 레지스트 OPC 모델의 특수 요구사항 파악
- Low-n mask의 OPC 모델링에 미치는 영향: 기존 binary/AttPSM 대비 차이점
- ADI/AEI 양방향 측정 데이터를 OPC 모델 캘리브레이션에 통합하는 방법
- 음성 톤 MOR 레지스트의 독특한 물리적 특성을 OPC 컴팩트 모델에 반영하는 방법

## 태그
`Verification`, `EUV`, `HighNA`, `DryResist`, `MOR`, `LowNMask`, `OPCModel`, `0.55NA`, `imec`, `N2Node`, `SPIE`, `DTCO`, `2025`
