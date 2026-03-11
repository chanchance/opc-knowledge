# EPE Variability Comparison Study of Multiple Patterning Options for Restricted 2D Structures in Advanced Logic Nodes

## 메타데이터
- **저자**: Arup Saha (ASML Technology Development Ctr.), Brett Schroeder (Coventor/Lam Research), Tsann-Bim Chiou (ASML Technology Development Ctr., Taiwan), Fung Suong Ou (Lam Research Corp.)
- **연도**: 2021
- **게재지**: Proc. SPIE 11615, Advanced Etch Technology and Process Integration for Nanopatterning X, 116150M
- **DOI/URL**: https://doi.org/10.1117/12.2584615

## 핵심 요약
SADP(Self-Aligned Double Patterning)와 SALELE 등 다양한 멀티패터닝 옵션이 30nm 피치 그레이팅(grating)과 15nm 팁-투-팁(tip-to-tip) EUV 패턴에 대해 EPE(Edge Placement Error) 변동성에 미치는 영향을 체계적으로 비교한 논문. Tachyon SMO로 생성된 OPC 컨투어와 SEMulator3D 몬테카를로 시뮬레이션을 결합한 공정-리소그래피 통합 검증 방법론을 제시하였다.

## 주요 기여
1. **통합 공정-리소 EPE 분석 방법론**: 리소그래피 변동(도즈, 포커스, 플레어, 마스크 변동)과 etch/deposition 단계를 함께 몬테카를로 시뮬레이션으로 처리
2. **SADP vs. SALELE EPE 정량 비교**: 각 멀티패터닝 옵션별로 EPE 분포의 평균/표준편차 도출
3. **Tachyon OPC 컨투어 활용**: SMO 생성 컨투어를 레지스트 윤곽 입력으로 사용하는 검증 플로우
4. **SEMulator3D 몬테카를로**: 레지스트 컨투어, 스페이서 두께, 오버레이를 통합 시뮬레이션으로 처리
5. **OPC 설계 공간과 패터닝 옵션 간 상호작용** 체계적 정량화

## 검증 방법론
- 30nm 피치 L/S(grating) 및 15nm 팁-투-팁(cut 패턴) EUV 레이아웃 대상
- Tachyon SMO로 도즈, 포커스, 플레어, 마스크 변동 고려한 OPC 컨투어 생성
- SEMulator3D에서 레지스트 컨투어 + 스페이서 두께 + 각 노광 오버레이를 통합 Monte Carlo 분석
- EPE CDF(cumulative distribution function) 비교로 각 멀티패터닝 옵션의 공정 마진 정량화

## OPC 툴 구현 관련성
- SKOPC PWO(Process Window Optimizer) 모듈에서 멀티패터닝 공정 변동 입력 파라미터 확장 시 참조
- 오버레이, 스페이서 두께, 레지스트 컨투어를 통합한 EPE 예산 계산 프레임워크 설계 지침
- 멀티패터닝 OPC 검증 플로우에서 Monte Carlo 기반 EPE 분포 보고 방식의 기준 논문
- `recipes/example_arfimm.yaml` 등에서 SADP/SAQP 공정 파라미터 추가 시 기준 데이터

## 태그
`Verification`, `SPIE`, `Multi-Patterning`, `SADP`, `EPE`, `EUV`, `Process Window`, `Monte Carlo`, `OPC`
