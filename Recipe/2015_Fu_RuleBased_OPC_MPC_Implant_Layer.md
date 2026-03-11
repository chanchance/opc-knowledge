# Rule-Based OPC and MPC Interaction for Implant Layers

## 메타데이터
- **저자**: Nan Fu, Guoxiang Ning, Florian Werle, Stefan Roling, Sandra Hecker, Paul Ackmann, Christian Buergel
- **연도**: 2015
- **게재지**: Proc. SPIE 9635, Photomask Technology 2015, 96351H
- **DOI/URL**: https://doi.org/10.1117/12.2197195

## 핵심 요약
Implant 레이어는 로직과 SRAM 영역을 동시에 커버해야 하며 패턴 밀도와 피치가 크게 다르기 때문에, 단일 노출 조건으로는 전 영역에 걸쳐 리소그래피 목표를 달성하기 어렵다. 본 논문은 MPC(Mask Process Correction)의 일환으로 선택적 룰 기반 re-targeting과 리소그래피 허용 오차 MPC를 활용하여 implant 레이어 웨이퍼 불균일 문제를 해결하는 방법을 제시한다.

## 주요 기여
1. **OPC-MPC 상호작용 분석**: OPC와 MPC가 implant 레이어에서 어떻게 상호 영향을 미치는지 체계적으로 분석
2. **선택적 룰 기반 re-targeting**: 로직/SRAM 영역별로 서로 다른 mean-to-nominal 값 달성
3. **리소그래피 허용 오차 MPC**: reticle 제조 공정 중 MPC를 통해 영역별 보정 적용
4. **트레이드오프 분석**: 웨이퍼 균일도와 공정 여유 개선을 위한 방법들의 장단점 비교
5. **Implant 특화 플로우**: 이온 주입 레이어의 특수성(낮은 콘트라스트, 넓은 패턴 범위)을 반영한 OPC-MPC 플로우

## Recipe/Flow 상세
- **Implant Layer OPC-MPC 플로우**:
  1. **OPC 단계**:
     - Implant 레이어 특성에 맞춘 모델 캘리브레이션
     - 로직/SRAM 영역 패턴 특성에 따른 선택적 룰 기반 re-targeting
     - 모델 기반 OPC 적용
  2. **MPC 단계 (리소그래피 허용 오차 MPC)**:
     - e-beam 쓰기 공정 시뮬레이션
     - 로직/SRAM 영역별 서로 다른 MPC bias 적용
     - CD 균일도 목표에 따른 dose 조정
  3. **통합 검증**:
     - Resist/etch 레벨 CD 시뮬레이션
     - 공정 여유 (DOF × EL) 확인
- **Implant 레이어 특수 고려사항**:
  - 로직 영역: 낮은 패턴 밀도, 넓은 피치
  - SRAM 영역: 높은 패턴 밀도, 좁은 피치
  - 두 영역 간 노출 조건 최적화 충돌 → 선택적 보정 필요
- **MPC 유형**: 룰 기반 dose correction + 선택적 geometry correction

## OPC 툴 구현 관련성
- Implant 레이어 OPC 레시피에 영역별 re-targeting 로직 추가
- OPC-MPC 연동 플로우: OPC care-area → MPC dose 조정
- `implant_opc.py`: 로직/SRAM 영역 분리 처리 구조
- 마스크 레이어별 특화 OPC 전략의 실례

## 태그
`ImplantLayer`, `OPC`, `MPC`, `RuleBased`, `Retargeting`, `SRAM`, `Logic`, `SPIE`, `2015`
