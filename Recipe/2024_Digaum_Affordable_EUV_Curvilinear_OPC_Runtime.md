# Affordable Optical Proximity Correction Runtime for EUV Curvilinear Mask Tape-Out Flow

## 메타데이터
- **저자**: Ping Digaum, Kazuto Kajiwara, Nobue Kosa, Ming-Chuan Yang, Ezequiel Vidal Russell, Jianhong Qiu, Omar Ndiaye, Nicolas Martin, Hesham Omar, Ehsan Kabiri Rahani, Peigen Cao, Michael Crouse
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540T
- **DOI/URL**: https://doi.org/10.1117/12.3009981

## 핵심 요약
EUV curvilinear 마스크 tape-out을 위한 OPC 및 검증 플로우에서 런타임을 허용 가능한 수준으로 유지하면서 정확도를 보장하는 방법을 제시한다. 서로 다른 엔진들의 능력을 연결하여 정확도와 마스크 TAT(Turn-Around Time)를 균형 있게 맞추는 실용적인 tape-out 플로우를 구현한다.

## 주요 기여
1. **다중 엔진 연계 플로우**: 서로 다른 강점을 가진 OPC/검증 엔진들을 연계하여 효율화
2. **Affordable 런타임 달성**: EUV curvilinear 마스크 full-chip OPC의 실용적 TAT 실현
3. **정확도-속도 균형**: 정확한 엔진과 빠른 엔진의 하이브리드 조합 전략
4. **Tape-out 플로우 통합**: OPC + 검증의 end-to-end tape-out 플로우 완성
5. **EUV 특화**: EUV 리소그래피 특유의 curvilinear 마스크 요구사항 반영

## Recipe/Flow 상세
- **EUV Curvilinear Mask Tape-Out OPC 플로우**:
  1. **레이아웃 전처리**:
     - Manhattan 설계 → Curvilinear OPC 타겟 변환
     - 레이어별 OPC 레시피 선택 (정확도 요구 수준별)
  2. **다중 엔진 OPC 전략**:
     - **빠른 엔진 (1차)**: 대부분의 패턴에 빠른 curvilinear OPC 적용
     - **정밀 엔진 (2차)**: 임계 패턴, 핫스팟 위치에 정밀 엔진 집중 적용
     - **엔진 전환 기준**: EPE, NILS, 패턴 복잡도 등 자동 분류
  3. **Curvilinear 검증**:
     - 빠른 시뮬레이션으로 전체 칩 1차 검증
     - 실패 위치에 정밀 시뮬레이션 집중
  4. **MRC 및 MPC**:
     - Curvilinear MRC 검사
     - EUV 마스크용 MPC 적용
  5. **Tape-out 완성**: GDS/OASIS 포맷으로 마스크 데이터 출력
- **런타임 최적화 전략**:
  - 타일 기반 병렬 처리
  - 이전 OPC 결과 재활용 (incremental OPC)
  - 빠른 엔진의 curvilinear 근사와 정밀 엔진의 선택적 보완
- **평가 지표**: Full-chip OPC TAT, EPE 분포, 핫스팟 수, MRC 통과율

## OPC 툴 구현 관련성
- Full-chip curvilinear OPC의 런타임 최적화 전략 참고
- 다중 엔진 하이브리드 OPC 플로우 구조 설계
- `fullchip_curvilinear_opc.py`: 패턴 분류 → 엔진 선택 → 병렬 처리 파이프라인
- Tape-out 체크리스트: OPC → 검증 → MRC → MPC → GDS 출력

## 태그
`EUV`, `CurvilinearMask`, `OPC`, `Runtime`, `TapeOut`, `FullChip`, `MultiEngine`, `SPIE`, `2024`
