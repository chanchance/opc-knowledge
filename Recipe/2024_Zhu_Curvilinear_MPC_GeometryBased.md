# Geometry-Based Curvilinear Mask Process Correction for Enhanced Pattern Fidelity, Contrast, and Manufacturability

## 메타데이터
- **저자**: (IEEE Xplore document 10812794, 2024년 게재)
- **연도**: 2024
- **게재지**: IEEE Transactions on Semiconductor Manufacturing (또는 관련 IEEE 저널)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10812794/

## 핵심 요약
Curvilinear 마스크 패턴이 복잡한 패턴 환경과 심각한 proximity 효과로 인해 fidelity와 contrast 저하를 겪는 문제를 해결하기 위해, 기하학 기반 2-layer CL-MPC(Curvilinear Mask Process Correction) 방법을 제안한다. 패턴 충실도와 이미지 대비 공동 최적화에 패턴 제조 가능성 향상을 통합한 방법론이다.

## 주요 기여
1. **Skeleton 기반 프래그먼테이션**: CL 패턴의 스켈레톤을 이용해 보정 제어점(fragment) 생성
2. **이중 PID 제어기**: 타깃 포인트의 energy slope 분류 기반으로 패턴 fidelity 향상
3. **이미지 대비 피드백 메커니즘**: energy slope의 역수 최소화를 통해 이미지 contrast 개선
4. **제조 가능성 향상**: edge corner 스무딩 및 패턴 각도 최적화로 마스크 제조 용이성 증대
5. **2-Layer 구조**: fidelity/contrast 최적화 layer + manufacturability 향상 layer 분리

## Recipe/Flow 상세
- **입력**: Curvilinear OPC/ILT 결과물 (베지어 곡선 또는 다각형 근사)
- **Step 1 – Skeleton 기반 프래그먼테이션**:
  - CL 패턴의 medial axis(skeleton) 추출
  - skeleton 기반 제어점 배치 → 균등하고 물리적으로 의미 있는 fragment 생성
- **Step 2 – 이중 PID 보정**:
  - energy slope 분류 (고경사/저경사)
  - PID Controller 1: 패턴 fidelity (CD 오차 최소화)
  - PID Controller 2: 이미지 contrast (NILS 최대화)
- **Step 3 – 제조 가능성 후처리**:
  - 예각 코너 스무딩
  - 최소 곡률 반경 MRC 만족
  - 패턴 각도 최적화
- **평가 지표**: EPE, NILS, 마스크 CD 균일도, curvature compliance rate

## OPC 툴 구현 관련성
- CL-MPC 구현의 skeleton 기반 접근법 참고
- 이중 PID 제어기 구조를 OPC 수렴 루프에 적용 가능
- Energy slope 기반 fragment 분류 로직
- `curvilinear_mpc.py`: skeleton 추출 → PID 보정 → manufacturability 후처리 파이프라인

## 태그
`CurvilinearMask`, `MPC`, `GeometryBased`, `PID`, `Manufacturability`, `OPC`, `IEEE`, `2024`
