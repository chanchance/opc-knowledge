# EUV Full-Chip Curvilinear Mask Options for Logic Via and Metal Patterning

## 메타데이터
- **저자**: (SPIE DTCO and Computational Patterning II, 2023)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950K
- **DOI/URL**: https://doi.org/10.1117/12.2647882

## 핵심 요약
3nm 노드 via 및 metal 레이어를 대상으로 full-chip 규모의 EUV curvilinear 마스크 생성 옵션을 비교 평가한다. 전체 ILT(Inverse Lithography Technology), 하이브리드 ILT + 밀집 curvilinear OPC, 그리고 머신러닝 기반 접근법 등 다양한 방식의 성능, 런타임, 마스크 제조 가능성을 종합적으로 분석한다.

## 주요 기여
1. **ILT vs. Curvilinear OPC 비교**: 전체 ILT와 curvilinear OPC의 via/metal 레이어 성능 비교
2. **하이브리드 접근법**: ILT + dense curvilinear OPC 조합으로 품질-런타임 균형 최적화
3. **ML 기반 가속**: 머신러닝으로 curvilinear 마스크 생성 가속화
4. **3nm 노드 적용**: 실제 3nm 노드 via/metal 레이아웃 예시로 검증
5. **제조 가능성 분석**: 각 방식의 MRC 준수율, 파일 크기, 마스크 쓰기 시간 비교

## Recipe/Flow 상세
- **EUV Curvilinear 마스크 생성 옵션 비교**:
  1. **Option A – 전체 ILT**:
     - Pixel 기반 마스크 최적화 → 완전 curvilinear 형상
     - 최고 품질 (공정 창, EPE)
     - 런타임 오래 걸림, 파일 크기 매우 큼
  2. **Option B – 하이브리드 ILT + Dense Curvilinear OPC**:
     - SRAF: ILT로 생성
     - 주요 패턴: curvilinear OPC로 보정
     - 품질-런타임 균형 달성
  3. **Option C – ML 가속 Curvilinear**:
     - 학습된 모델로 curvilinear 마스크 즉시 생성
     - 추론 단계에서 가장 빠름
     - 새 레이아웃에 대한 일반화 성능 중요
- **대상 레이어**: Via 레이어, Metal 레이어 (Logic, 3nm 노드)
- **EUV 특화 고려사항**:
  - Stochastic 효과: via 레이어에서 curvilinear 마스크로 실패율 감소
  - 마스크 3D: EUV 반사형 마스크의 곡선 형상 EM 효과
- **평가 지표**: EPE, 공정 창, 런타임, 파일 크기, MRC 위반율

## OPC 툴 구현 관련성
- SKOPC의 EUV via/metal 레이어 curvilinear OPC 전략 선택 기준
- ILT와 curvilinear OPC의 하이브리드 구현 방법
- 3nm 노드 via/metal OPC 레시피 파라미터 참고
- `euv_curvilinear_opc.py`: 레이어 타입별 curvilinear 생성 옵션 선택기

## 태그
`EUV`, `CurvilinearMask`, `OPC`, `ILT`, `Via`, `Metal`, `3nm`, `FullChip`, `SPIE`, `2023`
