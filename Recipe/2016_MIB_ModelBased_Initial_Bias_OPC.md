# Model-Based Initial Bias (MIB): Toward a Single-Iteration Optical Proximity Correction

## 메타데이터
- **저자**: (IEEE Xplore 문서 7368170, 저자 정보 상세 접근 필요)
- **소속**: 미상 (IEEE 게재)
- **연도**: 2016
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD) 추정
- **DOI/URL**: https://ieeexplore.ieee.org/document/7368170

## 핵심 요약
모델 기반 초기 편향(Model-Based Initial Bias, MIB) 방법론을 제안하여 OPC 반복 횟수를 대폭 줄인다. 광학 시뮬레이션 파라미터를 이용해 최종 OPC 형상을 높은 정확도로 예측하는 compact bias-model을 구축하고, 이를 OPC의 초기 조건으로 사용한다. 10nm 메탈 레이어 테스트에서 OPC 반복 횟수의 약 50%를 절감함을 검증한다.

## 주요 기여
1. **Compact bias-model 구축**: 광학 시뮬레이션 파라미터 기반으로 최종 OPC 형상을 근사 예측하는 범용 모델
2. **OPC 초기 조건 개선**: 기본 초기 조건 대신 MIB로 시작 → OPC 시작점이 최종 해에 훨씬 가까워짐
3. **반복 횟수 50% 절감**: 10nm 메탈 레이어에서 약 절반의 OPC 반복 횟수로 동일 수렴 달성
4. **범용성**: 다양한 레이아웃 패턴에 적용 가능한 generic compact model 설계
5. **단일 반복 OPC 지향**: 궁극적으로 single-iteration OPC 달성을 목표로 하는 연구 방향

## Recipe/Flow 상세
```
[MIB-Enhanced OPC Flow]
1. Compact Bias-Model 구축 (오프라인):
   - 광학 시뮬레이션 파라미터 추출 (aerial image 특성값)
   - 다양한 패턴에서 최종 OPC 결과 수집
   - 파라미터 → OPC 결과 매핑 compact model 훈련
2. MIB 초기값 생성 (온라인):
   - 입력 레이아웃 각 segment에서 광학 파라미터 계산
   - Compact model로 초기 bias 예측
   - 설계 타겟에 초기 bias 적용 → MIB 초기 마스크 생성
3. OPC 반복 최적화 (MIB 초기값에서 시작):
   - 기존 model-based OPC 알고리즘 동일 적용
   - 단, 초기 조건이 MIB로 개선됨
   - 수렴까지 반복 횟수 ~50% 절감
4. 수렴 검증 및 ORC
```

### 핵심 파라미터
- **Compact model 입력**: 광학 시뮬레이션 파라미터 (aerial image 특성)
- **Compact model 출력**: 초기 edge bias 예측값
- **반복 횟수 절감**: 약 50% (10nm 메탈 레이어 기준)
- **목표**: single-iteration OPC (장기)

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: OPC 반복 루프의 초기 조건 설정에 MIB 방법 통합 — 수렴 속도 향상
- **런타임 최적화**: SKOPC의 OPC 실행 시간 단축을 위한 핵심 전략으로 활용 가능
- **Compact model**: GNN-OPC와 유사하게 neural network 기반 compact bias model로 MIB 구현 가능
- `skopc/modeling/gnn/`: GNN을 MIB compact model로 활용하는 hybrid OPC 플로우 설계 참고
- **Recipe 파라미터**: `opc_max_iterations` 값을 MIB 적용 시 절반으로 줄이는 전략

## 태그
`Recipe`, `IEEE`, `Model-Based OPC`, `Initial Bias`, `MIB`, `OPC Convergence`, `Iteration Reduction`, `Compact Model`, `10nm`, `Single-Iteration OPC`
