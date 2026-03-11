# Automatic SRAF Size Optimization During OPC

## 메타데이터
- **저자**: Srividya Jayaram, James Word
- **소속**: Mentor Graphics
- **연도**: 2009
- **게재지**: Proc. SPIE 7274, Optical Microlithography XXII, 72742F
- **DOI/URL**: https://doi.org/10.1117/12.814679

## 핵심 요약
OPC 실행 중에 SRAF(Sub-Resolution Assist Feature) 크기를 자동으로 최적화하는 방법론을 제안한다. 고립 패턴(isolated feature)의 process window 개선을 위해 SRAF가 필수적인 low-k1 마스크에서, 기존의 rule-based SRAF 크기 결정 방식 대신 OPC 루프 내에서 동적으로 SRAF 크기를 최적화한다.

## 주요 기여
1. **OPC 내 SRAF 크기 자동 최적화**: OPC 반복(iteration) 루프 안에서 SRAF 크기를 동적으로 조정
2. **Process window 개선**: 고립 패턴 대상으로 SRAF 크기 최적화를 통한 overlapped process window 확대
3. **Rule-based 한계 극복**: 고정 SRAF 크기 규칙 대신 패턴별 최적 크기 자동 산출
4. **OPC 통합**: 별도의 SRAF 삽입 단계 없이 OPC flow 내에서 통합 처리

## Recipe/Flow 상세
```
[Auto-SRAF-OPC Flow]
1. 초기 SRAF 삽입 (rule-based 초기값 사용)
2. OPC 반복 루프 시작:
   a. 현재 mask (main feature + SRAF)로 리소그래피 시뮬레이션
   b. EPE(Edge Placement Error) 및 process window 계산
   c. SRAF 크기 최적화:
      - SRAF 인쇄(printing) 위험 없는 범위 내에서 크기 조정
      - Process window 최대화 목표 함수
   d. Main feature OPC 보정값 계산
   e. 수렴 판정 (EPE < threshold)
3. 최종 mask 출력 (최적화된 SRAF 포함)
4. SRAF 인쇄 위험 검증 (SRAF printing check)
```

### 핵심 파라미터
- **SRAF 크기 범위**: MRC(Mask Rule Check) 허용 범위 내
- **최적화 목표**: process window (DOF × EL) 최대화
- **수렴 조건**: EPE < target 및 SRAF printing risk = 0
- **적용 대상**: low-k1 고립 패턴 (isolated lines, contacts)

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: OPC 반복 루프에 SRAF 크기 자동 조정 모듈 통합 참고
- `skopc/pwo/`: PWO(Process Window Optimizer)와 연계하여 SRAF 크기 최적화 목표 함수 공유 가능
- **레시피 파라미터**: `sraf_min_width`, `sraf_max_width` 설정 시 이 논문의 최적화 범위 참고
- `recipes/example_arfimm.yaml`: ArF 침지 리소그래피 SRAF 크기 파라미터 설정에 직접 적용

## 태그
`Recipe`, `SPIE`, `SRAF`, `Process Window`, `OPC`, `Automatic Optimization`, `Isolated Feature`, `Low-k1`
