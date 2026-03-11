# A Novel and Unified Full-Chip CMP Model Aware Dummy Fill Insertion Framework With SQP-Based Optimization Method

## 메타데이터
- **저자**: (IEEE Xplore document 9113505, Peking University CECA 연구팀)
- **연도**: 2020
- **게재지**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD)
- **DOI/URL**: https://ieeexplore.ieee.org/document/9113505/

## 핵심 요약
CMP(Chemical-Mechanical Polishing) 공정의 평탄화 품질을 향상시키기 위해 dummy fill을 삽입하는 것이 일반적이지만, fill 양, 평탄도, 기생 커패시턴스 등 여러 목표를 동시에 최적화하는 것은 어렵다. 본 논문은 full-chip CMP 시뮬레이터와 MSP-SQP(Multiple Starting Points - Sequential Quadratic Programming) 최적화를 통합한 통일된 dummy fill 삽입 프레임워크를 제안한다.

## 주요 기여
1. **통합 최적화 프레임워크**: fill 양, 평탄도, 기생 커패시턴스를 근사 없이 동시 최적화
2. **MSP-SQP 최적화**: Multiple Starting Points로 전역 최적해 탐색 + SQP로 정밀 수렴
3. **Full-chip CMP 모델 통합**: 전체 칩 규모에서 CMP 시뮬레이션 기반 fill 배치
4. **룰 기반 대비 우수성**: 기존 룰 기반 dummy fill 대비 평탄도 및 RC 특성 동시 개선
5. **확장성**: 대용량 칩 레이아웃에 적용 가능한 효율적 알고리즘

## Recipe/Flow 상세
- **CMP-aware Dummy Fill 삽입 플로우**:
  1. **CMP 모델 초기화**:
     - 패턴 밀도 맵 계산 (윈도우 기반)
     - 패턴 크기 효과 모델링 (Greenwood-Williamson 등)
  2. **Fill 후보 위치 생성**:
     - DRC 규칙 만족하는 fill 가능 영역 추출
     - Fill 크기 및 형상 옵션 정의
  3. **최적화 문제 수식화**:
     - 목적함수: 평탄도 최대화 (CMP 높이 차 최소화)
     - 제약: 최대 기생 커패시턴스 한계, DRC 규칙
     - 변수: 각 fill 위치의 삽입 여부 및 크기
  4. **MSP-SQP 최적화**:
     - Multiple Starting Points: 다양한 초기 fill 배치에서 시작
     - SQP: 각 시작점에서 연속 완화 후 정밀 수렴
  5. **Fill 삽입 및 검증**:
     - 최적 fill 배치 적용
     - CMP 시뮬레이션으로 평탄도 검증
     - RC 추출로 기생 커패시턴스 확인
- **OPC와의 연관성**: CMP 후 토폴로지 변화 → OPC 모델에 영향 → CMP-aware OPC 필요
- **평가 지표**: 높이 차(height variation), fill ratio, 기생 커패시턴스 증가량

## OPC 툴 구현 관련성
- CMP-aware OPC 구현 시 dummy fill 삽입 후 토폴로지 입력 처리
- 패턴 밀도 맵 기반 CMP 모델과 OPC 모델의 연동 구조
- `cmp_fill_insertion.py`: 밀도 맵 → SQP 최적화 → fill 배치 파이프라인
- BEOL 레이어 OPC 정확도 향상을 위한 CMP 시뮬레이션 선행 처리

## 태그
`CMP`, `DummyFill`, `ModelBased`, `Optimization`, `SQP`, `FullChip`, `BEOL`, `IEEE`, `2020`
