# Optimizing Gate Layer OPC Correction and SRAF Placement for Maximum Design Manufacturability

## 메타데이터
- **저자**: Travis Brist, Le Hong, Ayman Yehia, Tamer Tawfik, Shumay Shang, Kyohei Sakajiri, John L. Sturtevant
- **연도**: 2007
- **게재지**: Proc. SPIE 6521, Design for Manufacturability through Design-Process Integration, 65211L
- **DOI/URL**: https://doi.org/10.1117/12.712748

## 핵심 요약
게이트 레이어는 트랜지스터 성능을 직접 결정하는 가장 중요한 리소그래피 레이어이다. 본 논문은 게이트 레이어에 대한 OPC 보정과 SRAF 배치를 동시에 최적화하여 설계 제조 가능성(design manufacturability)을 극대화하는 방법을 제시한다. 서로 다른 OPC 전략과 SRAF 규칙이 게이트 CD 균일도 및 공정 창에 미치는 영향을 체계적으로 분석한다.

## 주요 기여
1. **게이트 OPC-SRAF 공동 최적화**: OPC 보정량과 SRAF 크기/위치를 동시에 최적화하는 방법론
2. **설계 제조 가능성 메트릭**: 게이트 레이어 특화 DFM 지표 정의 및 평가
3. **공정 창 최대화**: 다양한 게이트 패턴(고립, 반고립, 밀집)에 걸친 공정 창 균형
4. **SRAF 규칙 최적화**: 게이트 레이어의 OPC 목표와 정합하는 SRAF 배치 규칙 도출
5. **실용적 플로우**: 실제 제품 게이트 레이어에 적용 가능한 실용적 OPC-SRAF 최적화 플로우

## Recipe/Flow 상세
- **게이트 레이어 OPC-SRAF 최적화 플로우**:
  1. **OPC 목표 정의**:
     - 게이트 CD 타겟 (nominal + 공정 여유)
     - 라인 엔드 단축(line-end pullback) 허용 범위
     - 코너 라운딩 허용 범위
  2. **SRAF 배치 규칙 설계**:
     - 고립/반고립/밀집 게이트에 따른 SRAF 크기 테이블
     - SRAF와 게이트 간 최소 간격 규칙
     - 게이트-게이트 간격에 따른 SRAF 개수 규칙
  3. **공동 최적화**:
     - OPC 수렴 후 SRAF 배치 → SRAF 고려 OPC 재수렴
     - 공정 창 시뮬레이션으로 각 조합 평가
  4. **설계 제조 가능성 검증**:
     - 전체 게이트 패턴 타입에 걸친 CD 균일도 확인
     - DOF, EL, MEEF 등 공정 창 지표 평가
- **게이트 레이어 특수 고려사항**:
  - 트랜지스터 on/off 전류에 직접 영향 → 엄격한 CD 목표
  - 라인 엔드 단축: 소스/드레인 접촉 실패 방지 필수
  - 2D 형상(T자, L자 게이트) 처리

## OPC 툴 구현 관련성
- SKOPC 모델링 모듈의 게이트 레이어 OPC 레시피 설계 기준
- SRAF 배치와 OPC 연동 구조 (`sraf_insertion.py` + `model_based_opc.py`)
- 게이트 레이어 특화 fragment 크기 및 수렴 파라미터 설정
- 라인 엔드 보정(serif/hammer head) 전략

## 태그
`GateLayer`, `OPC`, `SRAF`, `Manufacturability`, `ProcessWindow`, `DFM`, `SPIE`, `2007`
