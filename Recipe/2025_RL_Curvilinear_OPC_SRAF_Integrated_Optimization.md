# Integrated Curvilinear OPC and SRAF Optimization through Reinforcement Learning

## 메타데이터
- **저자**: (SPIE Photomask Technology 2025, 발표 136871C)
- **연도**: 2025
- **게재지**: Proc. SPIE 13687, Photomask Technology 2025, 136871C
- **DOI/URL**: https://doi.org/10.1117/12.3071663

## 핵심 요약
Curvilinear OPC와 SRAF(Sub-Resolution Assist Feature) 배치를 강화학습(Reinforcement Learning)을 통해 통합 최적화하는 방법을 제안한다. 기존에 순차적으로 수행하던 SRAF 삽입과 OPC 보정을 공동으로 최적화하여, 리소그래피 공정 창과 마스크 제조 가능성을 동시에 향상시킨다.

## 주요 기여
1. **통합 CL-OPC + SRAF 최적화**: 순차적 SRAF-OPC가 아닌 공동(joint) 최적화로 전역 최적해 탐색
2. **강화학습 기반 에이전트**: SRAF 배치 및 OPC 보정량을 동시에 결정하는 RL 정책 학습
3. **Curvilinear SRAF 지원**: Manhattan SRAF뿐 아니라 curvilinear 형상의 SRAF 최적화 가능
4. **공정 창 최대화**: 에이전트의 보상 함수로 DOF×EL 및 NILS를 직접 사용
5. **Photomask Technology 2025 발표**: 최신 마스크 기술 동향 반영

## Recipe/Flow 상세
- **RL 기반 통합 CL-OPC + SRAF 최적화 플로우**:
  1. **환경 정의**:
     - 상태(State): 현재 마스크 형상 + 웨이퍼 이미지 시뮬레이션 결과
     - 행동(Action): SRAF 위치/크기 조정 + OPC 세그먼트 이동
     - 보상(Reward): NILS 향상 + EPE 감소 + MRC 위반 페널티
  2. **RL 학습**:
     - Policy Gradient 또는 PPO 기반 에이전트 학습
     - 다양한 레이아웃 패턴으로 범용 정책 학습
  3. **추론 단계**:
     - 새 레이아웃에 학습된 정책 적용
     - SRAF 삽입 → curvilinear OPC 수렴 동시 진행
  4. **Curvilinear MRC 검증**:
     - 생성된 curvilinear SRAF + OPC 형상의 MRC 확인
     - 위반 시 페널티 반영하여 재최적화
- **핵심 차별점**: SRAF와 OPC 상호 의존성(SRAF 위치가 OPC 수렴에 영향)을 공동 최적화로 해결
- **평가 지표**: 공정 창 (DOF, EL), NILS, EPE, SRAF MRC 통과율

## OPC 툴 구현 관련성
- SKOPC의 SRAF 모듈 + OPC 모듈 공동 최적화 구조 참고
- RL 에이전트를 OPC 수렴 루프에 통합하는 방법
- Curvilinear SRAF 형상 표현 및 MRC 검사
- `rl_opc_sraf.py`: RL 환경 → joint SRAF+OPC 정책 학습 파이프라인

## 태그
`CurvilinearOPC`, `SRAF`, `ReinforcementLearning`, `JointOptimization`, `ProcessWindow`, `Mask`, `SPIE`, `2025`
