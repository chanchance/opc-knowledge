# Affordable Optical Proximity Correction Runtime for EUV Curvilinear Mask Tape-Out Flow

## 메타데이터
- **저자**: Ping Digaum, Kazuto Kajiwara, Nobue Kosa, Ming-Chuan Yang, Ezequiel Vidal Russell, Jianhong Qiu, Omar Ndiaye, Nicolas Martin, Hesham Omar, Ehsan Kabiri Rahani, Peigen Cao, Michael Crouse
- **소속**: (SPIE DTCO and Computational Patterning III 게재)
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540T
- **DOI/URL**: https://doi.org/10.1117/12.3009981

## 핵심 요약
EUV curvilinear mask tape-out을 위한 현실적인 OPC/검증 런타임을 달성하는 통합 플로우를 제시한다. Source optimization, OPC, 검증, MPC(Mask Process Correction), 데이터 볼륨 처리, 마스크 writing 시간 등 tape-out 전 과정의 런타임 문제를 다양한 엔진의 역량을 연결하여 정확도와 마스크 TAT(Turn-Around Time) 간 균형을 달성한다.

## 주요 기여
1. **런타임-정확도 균형 플로우**: 여러 엔진(fast approximate + high-accuracy)을 단계별로 조합하는 hybrid tape-out 전략
2. **EUV curvilinear 전용**: Manhattan OPC와 달리 곡선형 마스크의 OPC/검증에서 발생하는 데이터량 폭증 문제 해결
3. **Source optimization 통합**: SMO를 EUV curvilinear OPC 루프에 통합하여 전체 공정 마진 최적화
4. **MPC 런타임 단축**: curvilinear mask 특유의 MPC 계산 부담을 경감하는 근사화 전략
5. **Full chip 확장성**: 산업적 full-chip 규모에서 적용 가능한 실용적 런타임 달성

## Recipe/Flow 상세
```
[EUV Curvilinear Tape-Out OPC Flow]
1. Source Optimization (SMO):
   - EUV 광원 최적화 (pupil 형상 최적화)
   - Curvilinear mask와 co-optimization
2. Fast OPC (1차 보정):
   - 빠른 근사 엔진으로 초기 curvilinear 보정값 생성
   - 전체 칩 영역 커버리지 확보
3. High-Accuracy OPC/검증 (선택적 정밀화):
   - 임계 영역(hot spot 후보)에 고정밀 엔진 적용
   - Electromagnetic 마스크 3D 효과 포함 시뮬레이션
4. Mask Process Correction (MPC):
   - E-beam writing의 proximity effect 보정
   - Curvilinear 형상의 MPC 근사화로 런타임 단축
5. 데이터 fracture 및 볼륨 관리:
   - Curvilinear mask 특유의 대용량 fracture 데이터 처리
   - Mask writing time 최적화
6. 최종 검증 및 ORC
```

### 핵심 파라미터
- **목표 노드**: EUV (13.5nm) 선단 노드
- **마스크 유형**: Curvilinear (곡선형)
- **런타임 목표**: 산업적 tape-out TAT 내 처리
- **정확도 지표**: OPC/검증 엔진 혼합 사용으로 최적 균형

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: EUV curvilinear OPC 플로우 설계 시 multi-engine 전략 참고
- `skopc/pwo/`: Process window 최적화와 SMO 연계 구조 참고
- **Curvilinear OPC**: SKOPC의 GDS curvilinear 형상 처리 및 OPC 보정 기능 확장 시 핵심 참고 문헌
- `recipes/example_euv.yaml`: EUV 7nm 노드 recipe에 curvilinear OPC 파라미터 추가 시 활용

## 태그
`Recipe`, `SPIE`, `EUV`, `Curvilinear Mask`, `OPC`, `Tape-Out`, `Runtime`, `MPC`, `SMO`, `Full-Chip`, `2024`
