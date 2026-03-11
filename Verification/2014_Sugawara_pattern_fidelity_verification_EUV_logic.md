# Pattern Fidelity Verification for Logic Design in EUV Lithography

## 메타데이터
- **저자**: Minoru Sugawara, Eric Hendrickx, Vicky Philipsen, Chris Maloney, Germain Fenger
- **연도**: 2014
- **게재지**: Proc. SPIE 9048, Extreme Ultraviolet (EUV) Lithography V
- **DOI/URL**: https://doi.org/10.1117/12.2046096

## 핵심 요약
EUV 리소그래피에서 마스크 3D 효과를 인식한 OPC(DDM-OPC)를 적용한 후의 패턴 피델리티를 검증한 논문. NXE3300B EUV 노광기를 이용해 10nm 노드 로직 디바이스의 2D 이미지에 대한 DDM-OPC 효과를 실험적으로 확인하고, 패턴 배치 오류(PPE)를 정량화한다. 완벽한 OPC 후 예측 잔류 PPE는 x방향 0.21nm, y방향 0.76nm로, 이는 웨이퍼 디포커스와 마스크 평탄도의 보정 불가 성분에 기인한다.

## 주요 기여
1. Mentor Graphics DDM(Domain Decomposition Method) 기반 마스크 3D 인식 OPC 방법론 검증
2. EUV 리소그래피에서 로직 설계 패턴 피델리티의 실험적 측정 및 정량화
3. 패턴 배치 오류(PPE) 잔류 성분 분석: 웨이퍼 디포커스와 마스크 평탄도 기여분 분리
4. EUV 전용 마스크 그림자 효과(shadowing) 보정을 포함한 2D OPC 검증 프레임워크 제시

## 검증 방법론
- **실험 플랫폼**: ASML NXE3300B EUV 노광기
- **기술 노드**: 10nm 노드 로직 디바이스
- **OPC 방법**: DDM(Domain Decomposition Method) - 마스크 3D 효과 인식
- **PPE 측정**: x/y 방향 패턴 배치 오류 정량화
- **보정 불가 성분**: 잔류 PPE = x: 0.21nm, y: 0.76nm
- **기여 원인**: 웨이퍼 디포커스, 마스크 평탄도의 uncorrectable 성분

## OPC 툴 구현 관련성
- EUV OPC 모델에 마스크 3D/그림자 효과를 포함해야 함을 실험으로 입증
- DDM 기반 OPC 알고리즘의 2D 패턴(로직 레이아웃)에 대한 검증 절차
- PPE 예산(budget) 설정 시 마스크 평탄도와 디포커스 기여분을 분리 고려해야 함
- 10nm 노드 EUV 리소그래피 OPC 검증 flow의 기준 논문

## 태그
`Verification`, `EUV`, `PatternFidelity`, `Mask3D`, `DDM-OPC`, `PPE`, `LogicDesign`, `SPIE`, `2014`
