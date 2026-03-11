# Geometry-Based Curvilinear Mask Process Correction for Enhanced Pattern Fidelity, Contrast, and Manufacturability

## 메타데이터
- **저자**: (저자명 미확인 - IEEE Xplore 수록)
- **연도**: 2024–2025
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10812794/

## 핵심 요약
EUV 리소그래피에 사용되는 곡선형 마스크 패턴의 마스크 공정 보정(MPC: Mask Process Correction)을 위한 2계층 기하학 기반 방법을 제안한다. 패턴 충실도(pattern fidelity), 이미지 대비(image contrast) 공동 최적화 및 패턴 제조 가능성 향상을 통합한 CL-MPC(Curvilinear Mask Process Correction) 방법론이다.

## 주요 기여
1. **2계층 기하학 기반 CL-MPC**: 1계층에서 패턴 충실도 및 이미지 대비 공동 최적화, 2계층에서 제조 가능성 향상을 처리하는 구조화된 접근법
2. **곡선형 마스크 전용 MPC**: 기존 맨해튼 MPC를 곡선형 패턴으로 확장하여 EUV 마스크에 적용
3. **이미지 대비 최적화 통합**: 충실도뿐만 아니라 광학 이미지 대비를 동시에 최적화하여 DOF(Depth of Focus) 및 NILS 향상
4. **제조 가능성 제약 통합**: 마스크 제조 공정 제약(MRC)을 보정 알고리즘에 직접 반영

## 검증 방법론
- 보정 전후 패턴 충실도 측정 (타겟 대비 마스크 패턴 EPE)
- 광학 이미지 대비 및 NILS 변화 정량 분석
- MRC 준수 여부로 제조 가능성 검증
- EUV 웨이퍼 시뮬레이션을 통한 최종 인쇄 패턴 충실도 확인

## OPC 툴 구현 관련성
- `skopc/modeling/` 내 마스크 공정 보정(MPC) 기능 구현 시 곡선형 패턴 지원을 위한 핵심 참고
- OPC 후 MPC 단계에서 패턴 충실도와 제조 가능성을 동시에 최적화하는 아키텍처 설계에 활용
- 레이아웃 에디터의 MRC 체크 기능을 MPC 루프에 통합하는 방안으로 참고
- `skopc/pwo/` PWO 모듈에서 마스크 공정 오차를 프로세스 윈도우 최적화에 반영할 때 활용

## 태그
`Verification`, `IEEE`, `TCAD`, `Curvilinear`, `MPC`, `EUV`, `Pattern_Fidelity`, `Manufacturability`, `2024`
