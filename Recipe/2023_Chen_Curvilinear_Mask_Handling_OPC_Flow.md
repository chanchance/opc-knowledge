# Curvilinear Mask Handling in OPC Flow

## 메타데이터
- **저자**: Yung-Yu Chen, Kai-Hsiang Chang, Wen-Li Cheng, Yu-Po Tang
- **연도**: 2023
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 23, Issue 1, 011203
- **DOI/URL**: https://doi.org/10.1117/1.JMM.23.1.011203

## 핵심 요약
기존 Manhattan OPC 워크플로우를 일반화하여 curvilinear 마스크를 생성하고 조작하는 새로운 접근법을 제시한다. Edge 기반 OPC를 vertex 기반으로 확장하여 곡선 형상을 자연스럽게 처리한다. Full-chip 보정 결과를 통해 contact 및 line/space 패턴 모두에서 curvilinear 마스크의 성능을 검증한다.

## 주요 기여
1. **Vertex 기반 OPC 일반화**: 기존 edge 기반 OPC를 vertex 이동으로 확장하여 곡선 형상 생성
2. **기존 OPC 워크플로우 호환**: 별도의 ILT 엔진 없이 기존 OPC 플로우에서 curvilinear 마스크 생성
3. **Full-chip 검증**: Contact 패턴과 line/space 패턴 모두에 대한 full-chip 결과 제시
4. **런타임 효율**: Curvilinear 마스크 생성 시간이 Manhattan 마스크 대비 약 2배 수준
5. **범용성**: 다양한 레이어 타입에 적용 가능한 일반적인 접근법

## Recipe/Flow 상세
- **Curvilinear Mask OPC 플로우 (Vertex 기반)**:
  1. **초기화**: Manhattan OPC 결과를 곡선 세그먼트로 변환
     - 각 edge를 베지어/스플라인으로 표현
     - Vertex 위치를 보정 자유도(degree of freedom)로 설정
  2. **Curvilinear OPC 수렴 루프**:
     - 현재 vertex 위치에서 웨이퍼 이미지 시뮬레이션
     - 각 vertex에서 EPE 및 이미지 기울기 계산
     - Vertex 이동량 계산 (edge 보정의 vertex 버전)
     - Curvilinear MRC 제약 적용 (최소 곡률 반경 등)
  3. **수렴 판정**: EPE RMS < 임계값
  4. **Full-chip 처리**: 타일 기반 병렬 처리로 full-chip 런타임 관리
- **Edge vs. Vertex 보정 비교**:
  - Edge 기반: 직선 segment를 수직 방향으로 이동 (Manhattan 결과)
  - Vertex 기반: 곡선 제어점을 임의 방향으로 이동 (Curvilinear 결과)
- **런타임**: Manhattan 대비 ~2× (full-chip 수준에서 실용적)
- **검증 레이어**: Contact hole, Line/Space (범용 검증)

## OPC 툴 구현 관련성
- SKOPC curvilinear OPC 구현의 핵심 참고: vertex 기반 보정 구조
- 기존 edge 기반 OPC 엔진을 vertex 기반으로 확장하는 방법
- `curvilinear_opc.py`: vertex 이동 기반 수렴 루프 구현
- Full-chip 타일 병렬 처리와 curvilinear 형상 경계 처리 방법

## 태그
`CurvilinearMask`, `OPC`, `VertexBased`, `EdgeBased`, `FullChip`, `Contact`, `LineSpace`, `JMM`, `2023`
