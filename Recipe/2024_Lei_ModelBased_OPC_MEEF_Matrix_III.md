# Model-Based OPC Using the MEEF Matrix III

## 메타데이터
- **저자**: Junjiang Lei, Yi Yang, George Lippincott, Xima Zhang
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 1295418
- **DOI/URL**: https://doi.org/10.1117/12.3010562

## 핵심 요약
MEEF(Mask Error Enhancement Factor) 행렬을 이용한 모델 기반 OPC 방법론의 3번째 연구. 2002년 Cobb & Granik의 MEEF matrix OPC(Part I)와 2014년 Lei et al.의 Part II를 이어, 최신 기술 노드와 curvilinear 마스크 환경에서 MEEF matrix 접근법을 확장하고 개선한다.

## 주요 기여
1. **MEEF Matrix OPC 확장**: 이전 Part I, II의 방법론을 최신 advanced node 및 curvilinear 환경에 적용
2. **수렴 개선**: MEEF 행렬 기반 Newton-Raphson 수렴 알고리즘 개선
3. **Curvilinear 적용**: 베지어/곡선 세그먼트에 MEEF matrix OPC 적용 가능성 탐구
4. **고정밀 보정**: 선형 근사(MEEF scalar) 대비 행렬 접근법의 정확도 향상 입증
5. **Advanced node 검증**: 최신 노드 레이아웃에 대한 수렴성 및 정확도 검증

## Recipe/Flow 상세
- **MEEF Matrix OPC 알고리즘 구조**:
  1. **MEEF 행렬 계산**:
     - 현재 마스크 형상에서 MEEF = d(wafer CD) / d(mask CD) Jacobian 계산
     - 인접 fragment 간의 상호 영향(off-diagonal terms) 포함
  2. **Newton-Raphson 업데이트**:
     - 현재 EPE 벡터 계산
     - MEEF^-1 × EPE → 마스크 fragment 이동량 계산
     - 단순 비례 보정(1/MEEF scalar) 대비 coupling 효과 정확히 반영
  3. **수렴 가속**:
     - 행렬 역산 최적화 (희소 행렬 구조 활용)
     - Damping factor로 오버슈트 방지
  4. **수렴 판정**: EPE 벡터 놈 < 임계값
- **MEEF Matrix vs. Scalar 비교**:
  - Scalar: 각 fragment 독립적으로 1/MEEF 적용 (빠르지만 coupling 무시)
  - Matrix: 인접 fragment 상호 영향 고려 (정확하지만 계산 비용 큼)
- **적용 레이어**: Dense 2D 패턴, contact, metal (coupling이 중요한 경우)

## OPC 툴 구현 관련성
- SKOPC 모델링 모듈의 OPC 수렴 알고리즘 개선 참고
- Fragment coupling 고려한 Jacobian 기반 업데이트 구현
- `meef_matrix_opc.py`: 희소 MEEF 행렬 계산 → Newton 업데이트 파이프라인
- Part I (2002), Part II (2014)와 함께 MEEF matrix OPC 이론 체계 완성

## 태그
`MEEF`, `ModelBased`, `OPC`, `Matrix`, `NewtonRaphson`, `Convergence`, `SPIE`, `2024`
