# Curvilinear Optical Proximity Correction via Cardinal Spline

## 메타데이터
- **저자**: Su Zheng, Xiaoxiao Liang, Ziyang Yu, Yuzhe Ma, Bei Yu, Martin Wong
- **소속**: Chinese University of Hong Kong, Hong Kong University of Science and Technology (GZ), Hong Kong Baptist University
- **연도**: 2025
- **게재지**: IEEE/ACM Design Automation Conference (DAC) 2025
- **DOI/URL**: https://ieeexplore.ieee.org/document/11133367/

## 핵심 요약
마스크 패턴을 cardinal spline의 제어점(control point)으로 표현하고, 제어점을 반복적으로 조정하여 OPC를 수행하는 curvilinear OPC 프레임워크를 제안한다. ILT 결과를 cardinal spline으로 피팅하는 알고리즘과 MRC(Mask Rule Check) 위반을 해소하는 알고리즘을 함께 제시하며, 폭·공간·면적·곡률에 대한 포괄적인 MRC 검사 방법을 구현한다.

## 주요 기여
1. **Cardinal spline 기반 마스크 표현**: 마스크 형상을 제어점 집합으로 파라미터화 — 연속적 곡선 표현으로 curvilinear OPC 가능
2. **반복적 제어점 최적화**: 리소그래피 시뮬레이션 기반 EPE gradient로 제어점 위치를 반복 갱신
3. **포괄적 MRC 검사**: cardinal spline 형상에 대해 폭(width), 공간(space), 면적(area), 곡률(curvature) 네 가지 MRC 항목 모두 처리
4. **ILT 결과 피팅**: 기존 pixel-based ILT 출력을 cardinal spline으로 변환하는 피팅 알고리즘 — ILT와 OPC의 가교 역할
5. **MRC 위반 해소 알고리즘**: 최적화 중 발생하는 MRC 위반을 자동으로 수정하는 post-processing 루틴

## Recipe/Flow 상세
```
[Cardinal Spline Curvilinear OPC Flow]
1. 초기 마스크 표현:
   옵션 A: 직접 cardinal spline 초기화 (design intent polygon → 제어점 변환)
   옵션 B: ILT 결과 → cardinal spline 피팅 (고품질 초기값)
2. 리소그래피 시뮬레이션:
   - 현재 제어점 집합 → cardinal spline 마스크 생성
   - Hopkins/Abbe 광학 모델로 aerial image 계산
   - Resist 모델로 웨이퍼 contour 예측
3. EPE 계산 및 gradient 역전파:
   - 각 평가점에서 EPE 계산
   - 제어점에 대한 EPE gradient 산출
4. 제어점 업데이트:
   - Gradient descent 방향으로 제어점 이동
   - Step size: 학습률 파라미터 제어
5. MRC 검사 및 위반 해소:
   - 폭, 공간, 면적, 곡률 MRC 검사
   - 위반 제어점 자동 조정
6. 수렴 판정 (EPE < threshold) → 최종 curvilinear 마스크 출력
```

### 핵심 파라미터
- **마스크 표현**: Cardinal spline 제어점 (연속 곡선)
- **MRC 항목**: width, space, area, curvature (4가지)
- **최적화 방법**: gradient descent (리소그래피 시뮬레이션 기반)
- **ILT 연계**: pixel ILT → spline 피팅으로 초기값 활용 가능
- **적용 범위**: OPC/ILT 대안으로 모두 활용 가능

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: curvilinear OPC 기능 추가 시 cardinal spline 마스크 표현 채택 직접 참고
- `skopc/modeling/gnn/`: GNN-OPC의 edge segment displacement를 cardinal spline 제어점 이동으로 확장 가능
- **MRC 통합**: SKOPC의 OPC 루프에 곡률 기반 MRC 검사 추가 구현 참고
- `skopc/modeling/`: ILT와 OPC의 통합 플로우 설계 시 이 논문의 ILT→spline 피팅 알고리즘 활용
- `recipes/example_euv.yaml`: EUV 노드 curvilinear OPC recipe 파라미터 설계 기준

## 태그
`Recipe`, `IEEE`, `Curvilinear OPC`, `Cardinal Spline`, `Control Points`, `MRC`, `ILT`, `DAC 2025`, `Gradient Descent`, `Mask Optimization`
