# Wafer Sub-Layer Impact in OPC/ORC Models for Advanced Node Implant Layers

## 메타데이터
- **저자**: Jean-Christophe Le-Denmat, Jean-Christophe Michel, Elodie Sungauer, Emek Yesilada, Frederic Robert, Song Lan, Mu Feng, Lei Wang, Laurent Depre, Sanjay Kapasi
- **연도**: 2014
- **게재지**: Proc. SPIE 9052, Optical Microlithography XXVII, 90520D
- **DOI/URL**: https://doi.org/10.1117/12.2047115

## 핵심 요약
28nm 기술 노드 이하에서 BARC(Bottom Anti-Reflection Coating)를 사용하지 않는 이온 주입(implant) 레이어에서, 하층(prior layer)의 구조물로부터 발생하는 광 산란 효과(W3D: Wafer 3D topography proximity effect)가 OPC/ORC(Optical Rule Check) 모델에 미치는 영향을 분석한다. 하층 구조 의존적 OPC 보정의 필요성을 실험적으로 입증한다.

## 주요 기여
1. **W3D 효과 정량화**: 28nm 이하 implant 레이어에서 하층 구조가 OPC 모델에 미치는 영향 측정
2. **BARC-free 환경 특성**: BARC 없는 implant 레이어에서 하층 반사의 OPC 영향 분석
3. **OPC/ORC 모델 보정**: 하층 구조 정보를 포함한 3D wafer topography 보정항 추가
4. **공정 변동 분석**: 하층 패턴 밀도 및 형상 변화에 따른 OPC 모델 오차 평가
5. **28nm 노드 적용**: 실제 28nm 공정에서의 검증 데이터 제시

## Recipe/Flow 상세
- **Implant Layer W3D-aware OPC 플로우**:
  1. **하층 구조 분석**:
     - 이전 공정 단계의 레이어 구조 파악 (게이트, STI, 활성 영역 등)
     - 하층 패턴 밀도 및 높이 차 맵 생성
  2. **W3D 효과 모델링**:
     - 하층 구조에서 반사된 산란광 시뮬레이션
     - 국소 하층 밀도에 따른 CD 오차 상관관계 도출
  3. **OPC 모델 보정**:
     - 표준 2D OPC 모델에 W3D 보정항 추가
     - 하층 구조별 bias 테이블 또는 모델 파라미터 조정
  4. **ORC 룰 업데이트**:
     - W3D 효과 고려한 ORC(Optical Rule Check) 기준 재설정
  5. **검증**: W3D 보정 전후 CD 오차 및 공정 여유 비교
- **28nm Implant 레이어 특성**:
  - BARC 미사용: 하층 반사를 직접 받음
  - 넓은 패턴 범위: 고밀도 ~ 저밀도 영역 공존
  - 하층 구조: STI, 활성 영역, 게이트 등 다양한 높이

## OPC 툴 구현 관련성
- Implant 레이어 OPC 모델에 W3D 보정항 통합 방법
- 하층 밀도 맵 기반 OPC bias 조정 로직
- `implant_w3d_opc.py`: 하층 구조 → W3D 효과 계산 → OPC 보정 파이프라인
- BARC-free 공정 OPC 레시피 설계 기준

## 태그
`ImplantLayer`, `OPC`, `WaferTopography`, `W3D`, `SubLayer`, `28nm`, `BARC`, `SPIE`, `2014`
