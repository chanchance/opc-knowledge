# Rounded-Corner Aware OPC for Convergency and Lithography Performance Improving

## 메타데이터
- **저자**: Ruihua Liu, Fu Li, Chunlong Yu, Jingjing Fan, Yu Mu, Song Sun, Chong Wang, Jiangliu Shi, Qingchen Cao
- **소속**: (SPIE Photomask Technology 2023 게재)
- **연도**: 2023
- **게재지**: Proc. SPIE 12751, Photomask Technology 2023, 1275115
- **DOI/URL**: https://doi.org/10.1117/12.2686228

## 핵심 요약
마스크 제조 과정에서 e-beam 노광 시스템의 한계(beam blur, proximity effect, resist 노광 공정)로 인해 발생하는 마스크 코너 라운딩(Mask Corner Rounding, MCR)을 OPC 루프에 통합하는 RC-OPC(Rounded Corner Aware OPC)를 제안한다. 기존 OPC는 단일 코너 라운딩 값을 사용하지만, RC-OPC는 치수별로 다른 코너 라운딩 거동을 반영하여 정확도, 리소그래피 성능, 패턴 충실도를 크게 향상시킨다.

## 주요 기여
1. **치수별 MCR 모델**: 다양한 e-beam 크기에 따른 코너 라운딩 거동 비교 분석 및 치수 의존적 모델 구축
2. **RC-OPC 프레임워크**: 단일 MCR 값 대신 형상별 실제 코너 라운딩을 OPC 시뮬레이션에 반영
3. **수렴성 개선**: 코너 라운딩을 정확히 반영함으로써 OPC 반복 수렴 안정성 향상
4. **리소그래피 성능 향상**: 기존 OPC 대비 실질적인 패턴 충실도 및 공정 마진 개선
5. **강건성**: 다양한 직사각형 형상에서 검증된 방법론

## Recipe/Flow 상세
```
[RC-OPC (Rounded-Corner Aware OPC) Flow]
1. 마스크 코너 라운딩 특성화:
   - 다양한 e-beam 크기별 MCR 측정
   - 치수(패턴 크기)에 따른 MCR 변화 모델링
   - 형상별 (라인, 공간, 코너 유형별) MCR 룩업 테이블 구축
2. OPC 모델에 MCR 통합:
   - 기존: 전체 마스크에 단일 MCR 값 적용
   - RC-OPC: 각 feature 치수에 맞는 MCR 값 개별 적용
3. OPC 반복 루프:
   a. 현재 mask → MCR 적용 → "실제 마스크 형상" 시뮬레이션
   b. 웨이퍼 이미지 예측 (resist 시뮬레이션)
   c. EPE 계산 및 보정값 산출
   d. 수렴 판정
4. 검증:
   - MCR-aware 시뮬레이션으로 최종 패턴 충실도 확인
   - 기존 OPC 대비 개선량 정량화
```

### 핵심 파라미터
- **MCR 모델**: e-beam 크기 및 패턴 치수의 함수
- **적용 단위**: 형상별 개별 MCR 값 (단일 전역값 아님)
- **성능 지표**: 수렴성(convergency), 리소그래피 성능, 패턴 충실도
- **검증 방식**: 다양한 직사각형 형상 대상 시뮬레이션 비교

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: OPC 시뮬레이션에서 마스크 코너 라운딩 효과를 모델에 반영하는 구현 참고
- **Mask 3D 효과**: SKOPC의 마스크 모델에 MCR을 치수 의존적으로 추가하는 고도화 방향
- `skopc/modeling/`: 리소그래피 모델 calibration 시 MCR 파라미터 피팅 참고
- **Recipe 파라미터**: `mask_corner_rounding_radius` 파라미터를 치수별로 다르게 설정하는 방식 참고

## 태그
`Recipe`, `SPIE`, `Corner Rounding`, `Mask Corner Rounding`, `RC-OPC`, `OPC Convergence`, `Photomask`, `E-beam`, `Pattern Fidelity`, `2023`
