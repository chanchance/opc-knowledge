# Reducing Mask Process Correction Time with Hybrid Rule-Based and Model-Based Solution

## 메타데이터
- **저자**: Xuan Zhu, Chia-Wei Chang (New Ray Mask Technology Corp.), Yongming Wen, Ao Chen, Yu Zhu (SEIDA Technology Co. Ltd)
- **연도**: 2024
- **게재지**: Proc. SPIE 13216, Photomask Technology 2024, 1321624
- **DOI/URL**: https://doi.org/10.1117/12.3034092

## 핵심 요약
모델 기반 MPC(Model-Based Mask Process Correction)는 마스크 패턴 충실도 보장에 효과적이지만 런타임이 길다는 단점이 있다. 본 논문은 룰 기반 MPC와 모델 기반 MPC를 결합한 하이브리드 솔루션을 제안하여 MPC 런타임을 단축하면서도 보정 품질을 유지하는 접근법을 제시한다.

## 주요 기여
1. **하이브리드 MPC 아키텍처**: 단순 패턴은 룰 기반으로 빠르게 처리, 복잡 패턴은 모델 기반으로 정밀 보정
2. **런타임 감소**: 전체 모델 기반 대비 유의미한 TAT(Turn-Around Time) 단축
3. **패턴 분류 전략**: MPC 복잡도에 따라 패턴을 자동 분류하는 기준 정의
4. **보정 품질 유지**: 하이브리드 적용 후 마스크 CD 균일도 및 EPE 지표 비교 검증

## Recipe/Flow 상세
- **MPC 플로우 (하이브리드)**:
  1. **패턴 분류**: 형상 복잡도, 주변 밀도, 임계 치수 기반 분류
     - Class A (단순): 고립 line, 단순 contact → Rule-based MPC
     - Class B (복잡): 밀집 패턴, 2D 형상, critical CD → Model-based MPC
  2. **Rule-based MPC**: 미리 정의된 바이어스 테이블 적용 (빠름, ~10x 속도)
  3. **Model-based MPC**: e-beam 쓰기 공정 시뮬레이션 기반 반복 보정 (정밀)
  4. **통합 검증**: 두 결과 병합 후 MRC 및 CD 검증
- **적용 마스크 레이어**: 범용 (로직, 메모리 레이어 모두 적용)
- **평가 지표**: MPC 런타임, 마스크 CD 오차, CDU, MRC 통과율

## OPC 툴 구현 관련성
- MPC 모듈 설계 시 rule-based와 model-based 병행 구조 참고
- 패턴 복잡도 기반 자동 분류 로직 구현 아이디어
- 전체 OPC → MPC 플로우의 TAT 최적화 전략
- `mask_process_correction.py`: 패턴 분류 → 하이브리드 보정 적용 파이프라인

## 태그
`MPC`, `HybridCorrection`, `RuleBased`, `ModelBased`, `Mask`, `Runtime`, `SPIE`, `2024`
