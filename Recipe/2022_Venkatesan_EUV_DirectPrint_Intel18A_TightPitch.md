# Direct Print EUV Patterning of Tight Pitch Metal Layers for Intel 18A Process Technology Node

## 메타데이터
- **저자**: R. Venkatesan, C. Guven, D. Bhawe, A. R. Greenwood, Z. Zhang, P. Gupta, P. Saksena, R. Rodriguez, N. Moumen, B. Bains, M. Aykol, C. Wallace, R. Bigwood, K. Fischer
- **연도**: 2022
- **게재지**: Proc. SPIE 12292, International Conference on Extreme Ultraviolet Lithography 2022, 1229202
- **DOI/URL**: https://doi.org/10.1117/12.2641744

## 핵심 요약
Intel 18A 공정 기술 노드의 약 30~36nm 피치 금속 레이어를 EUV 단일 노광(direct print)으로 패터닝하는 기술을 소개한다. 다중 패터닝 없이 EUV 단일 노광으로 타이트한 피치 메탈 레이어를 구현하기 위한 OPC, SMO, 레지스트 최적화 전략을 포함하는 Intel 내부 EUV 양산 플로우를 공개한다.

## 주요 기여
1. **Intel 18A EUV 단일 노광**: 30~36nm 피치 메탈 레이어를 다중 패터닝 없이 EUV 단일 노광으로 구현
2. **양산 수준 공정 검증**: HVM(High-Volume Manufacturing) 환경에서 EUV 직접 프린트 실증
3. **OPC 전략 공개**: Intel 18A 노드 메탈 레이어 EUV OPC 방법론 최초 공개
4. **공정 창 최적화**: 타이트 피치에서 DOF, EL 등 공정 창 지표 최적화
5. **Intel 내부 EUV 역량**: Intel의 자체 EUV 리소그래피 역량 및 컴퓨터 리소그래피 플로우 공개

## Recipe/Flow 상세
- **Intel 18A EUV 직접 프린트 플로우**:
  1. **타겟 설정**:
     - 피치: 30~36nm (금속 배선 레이어)
     - 단일 노광(no multi-patterning) 목표
     - Intel 18A RibbonFET 공정에서의 BEOL 첫 금속 레이어
  2. **레지스트 선택**:
     - EUV 고감도 레지스트 (CAR 또는 금속산화물 기반)
     - LWR 최소화 및 감도 균형 레지스트 선정
     - 음성 톤 현상(NTD) 또는 양성 톤 선택
  3. **광원 최적화(SMO)**:
     - 30~36nm 피치 최적 조명 조건 (dipole 또는 multipole)
     - 타이트 피치에서 NILS 최대화를 위한 광원 설계
  4. **마스크 설계 및 OPC**:
     - Dark-field 또는 bright-field 마스크 선택
     - 타이트 피치에서 OPC 보정 (SRAF 유무 포함)
     - EUV 특유의 shadowing, mask 3D 효과 모델링 및 보정
  5. **공정 창 최적화**:
     - Focus-Exposure 매트릭스 측정
     - DOF(Depth of Focus), EL(Exposure Latitude) 측정
     - 핫스팟 스크리닝 및 OPC 보정
  6. **양산 검증**:
     - 웨이퍼 CD 균일도, EPE 측정
     - 수율 테스트
- **Intel 18A 특성**:
  - RibbonFET(Gate-All-Around) 트랜지스터 구조
  - PowerVia 후면 전력 공급 기술과 결합
  - EUV 단일 노광으로 BEOL 스케일링 가속
- **업계 의의**: Intel의 EUV 양산 공정 복귀 및 경쟁력 회복의 핵심 기술

## OPC 툴 구현 관련성
- SKOPC EUV 단일 노광 메탈 OPC 레시피 설계 참고
- 30~36nm 피치 EUV OPC 파라미터 설정 기준
- Intel 18A 수준의 타이트 피치 OPC 정확도 요구사항 이해
- EUV 직접 프린트 vs. 다중 패터닝 선택 기준 및 OPC 전략 차이

## 태그
`EUV`, `DirectPrint`, `Intel18A`, `TightPitch`, `Metal`, `OPC`, `SinglePatterning`, `BEOL`, `RibbonFET`, `Manufacturing`, `SPIE`, `2022`
