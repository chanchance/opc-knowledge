# Model-based OPC Extension in OpenILT

## 메타데이터
- **저자**: (CUHK CSE, Bei Yu 연구그룹)
- **연도**: 2024
- **게재지**: IEEE Conference Publication, ISEDA 2024 (International Symposium of EDA)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10617951/ | https://www.cse.cuhk.edu.hk/~byu/papers/C209-ISEDA2024-ModelOPC.pdf

## 핵심 요약
오픈소스 컴퓨테이셔널 리소그래피 라이브러리 OpenILT에 Model-Based OPC(MB-OPC) 기능을 확장 구현한다. 레이아웃 크기 제한 극복, GPU 가속, 모듈식 OPC 알고리즘 플랫폼을 제공하며 기존 대비 5배 이상의 속도 향상을 달성한다.

## 주요 기여
- OpenILT 오픈소스 플랫폼에 MB-OPC 기능 통합 (기존 ILT 전용에서 OPC로 확장)
- 레이아웃 크기 제한 극복: 대형 레이아웃을 2×2µm² 패치로 분할 후 병렬 시뮬레이션
- GPU 대용량 병렬 처리를 통해 MB-OPC 속도 5배 이상 향상
- 모듈식/유연한 OPC 알고리즘 개발 플랫폼 제공
- full-chip 스케일 OPC를 오픈소스로 접근 가능하게 함

## 모델 수식/아키텍처
- 레이아웃 분할: large-scale layout → 2×2µm² sub-region 패치
- 각 패치별 GPU 리소그래피 시뮬레이션 수행
- 패치 시뮬레이션 결과를 병합하여 전체 프린트 이미지 재구성
- MB-OPC 반복: 시뮬레이션 → EPE 계산 → 마스크 이동 → 재시뮬레이션
- GPU 메모리 제약 내 최대 병렬도 활용

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC Modeling 모듈의 model-based OPC 엔진 설계에 직접 참고
- OpenILT 기반 오픈소스 OPC 구현 레퍼런스 (openilt_adapter.py와 연계 가능)
- GPU 가속 OPC 시뮬레이션 아키텍처의 실용적 구현 사례
- 패치 분할 및 병합 전략은 full-chip OPC 메모리 관리에 적용 가능

## 태그
`Model`, `IEEE`, `OpenILT`, `Model-based OPC`, `GPU`, `Open Source`, `Full-Chip`, `ISEDA`
