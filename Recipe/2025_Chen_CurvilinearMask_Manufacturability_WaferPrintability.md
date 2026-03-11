# The Exploration of Curvilinear Mask Manufacturability and Wafer Printability

## 메타데이터
- **저자**: Sheng Tse Chen, Kevin Lu, Gloria Yeh (Beijing Superstring Academy of Memory Technology, Lithography R&D Dept.)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 1342512
- **DOI/URL**: https://doi.org/10.1117/12.3050611

## 핵심 요약
ILT(Inverse Lithography Technology)로 생성된 curvilinear 마스크의 제조성(manufacturability)과 웨이퍼 프린터빌리티(printability)를 체계적으로 탐색한다. MRC(Mask Rule Check) 규칙 변화에 따른 curvilinear 마스크의 제조 가능성과 웨이퍼 패터닝 성능의 상관관계를 분석하고, 코너 패턴 충실도 제어(pattern fidelity control at corners) 및 MBAF(Model-Based Assist Features)의 마스크 제조성과 웨이퍼 프린터빌리티에 대한 영향을 종합 평가한다.

## 주요 기여
1. **Curvilinear 마스크 제조성-웨이퍼 프린터빌리티 상관관계**: ILT 생성 curvilinear 마스크의 MRC 변화에 따른 마스크 제조성 및 웨이퍼 인쇄 성능 체계적 평가
2. **MRC 규칙 영향 분석**: 다양한 MRC 설정(최소 선폭, 최소 간격, 코너 곡률 등)이 curvilinear 형상 및 웨이퍼 CD에 미치는 영향 정량화
3. **코너 패턴 충실도 제어**: curvilinear 마스크 코너부 형상 정밀도가 웨이퍼 임계치수에 미치는 영향 분석
4. **MBAF 마스크 적용**: 모델 기반 보조 피처(MBAF)의 curvilinear 형태 적용 시 마스크 제조성 및 웨이퍼 인쇄 개선 효과
5. **메모리 기술 응용**: 베이징 슈퍼스트링 메모리 기술 연구소에서 메모리 패터닝 관점에서의 curvilinear 마스크 실용성 평가

## Recipe/Flow 상세
- **Curvilinear 마스크 제조성 및 프린터빌리티 평가 플로우**:
  1. **ILT 기반 Curvilinear 마스크 생성**:
     - ILT 알고리즘으로 최적 curvilinear 마스크 패턴 생성
     - 다양한 MRC 규칙 적용: 엄격→완화된 MRC 시나리오
     - Curvilinear 형상의 코너 곡률 및 최소 피처 크기 변화
  2. **마스크 제조성 평가**:
     - MBMW(Multi-Beam Mask Writer) 기반 curvilinear 마스크 제조 시뮬레이션
     - MRC 위반 항목 분류: corner rounding, minimum CD, tip-to-tip 간격
     - MRC 허용 범위에 따른 마스크 기록 시간 및 복잡도 변화
  3. **패턴 충실도 제어 (Corners)**:
     - 코너부 curvilinear 형상의 마스크 제조 정밀도 분석
     - 코너 라운딩 허용 범위 최적화: 제조성 vs. 광학 성능 트레이드오프
     - 코너 처리 방식별(sharp vs. rounded vs. intermediate) 웨이퍼 CD 변화
  4. **MBAF 적용 및 효과 분석**:
     - 기존 사각형 SRAF → curvilinear MBAF 전환 효과
     - MBAF curvilinear 형상의 마스크 제조 복잡도 증가 분석
     - MBAF curvilinear 적용 시 웨이퍼 공정 창(DOF/EL) 변화
  5. **Wafer Printability 검증**:
     - 리소그래피 시뮬레이션으로 웨이퍼 인쇄 성능 예측
     - EPE(Edge Placement Error), CD 균일도, 공정 창 평가
     - Curvilinear vs. 맨해튼(Manhattan) 마스크 웨이퍼 인쇄 성능 비교
- **MRC-웨이퍼 성능 트레이드오프**:
  - 엄격한 MRC → 마스크 제조 용이, 웨이퍼 성능 일부 저하
  - 완화된 MRC → 마스크 복잡도 증가, 웨이퍼 CD 개선
  - 최적 MRC 설정: 마스크 제조성과 웨이퍼 성능의 균형점
- **소속**: Beijing Superstring Academy of Memory Technology, Lithography R&D Department (중국 베이징)

## OPC 툴 구현 관련성
- SKOPC ILT/curvilinear OPC 플로우에서 MRC 규칙 설정 가이드라인
- `curvilinear_mrc_optimizer.py`: MRC 제약 조건 하에서 curvilinear 형상 최적화
- MBAF curvilinear 형태 지원: 모델 기반 보조 피처 curvilinear 전환 모듈
- 코너 패턴 충실도 제어를 위한 OPC 후처리 알고리즘 기준

## 태그
`CurvilinearMask`, `ILT`, `MRC`, `WaferPrintability`, `Manufacturability`, `MBAF`, `CornerFidelity`, `Memory`, `BeijingSuperstring`, `OPC`, `SPIE`, `2025`
