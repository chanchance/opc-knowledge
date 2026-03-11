# Process Window Analysis of Post OPC SRAF Placement

## 메타데이터
- **저자**: (IEEE document 9972322 - 2022 IEEE Conference)
- **연도**: 2022
- **게재지**: IEEE Conference Publication
- **DOI/URL**: https://ieeexplore.ieee.org/document/9972322/
- **인용수**: ~10

## 핵심 요약
기존 SRAF 연구는 목표 주 패턴과 SRAF를 대상으로 하지만, OPC가 목표 패턴의 형상을 변경한다는 사실을 간과한다. 본 논문은 OPC 완료 후의 SRAF 배치(post-OPC SRAF 배치)와 공정 윈도우 간의 관계를 조사한다. OPC가 패턴 형상을 변경한 후의 SRAF 최적 배치 전략을 분석하여 전통적 OPC 전 SRAF 삽입 방식의 한계를 밝히고 개선 방향을 제시한다.

## 주요 기여
1. OPC에 의한 주 패턴 형상 변화가 SRAF 효과에 미치는 영향 분석
2. Post-OPC SRAF 배치의 공정 윈도우 특성 체계적 연구
3. 전통적 pre-OPC SRAF vs. post-OPC SRAF 공정 윈도우 비교
4. SRAF-OPC 상호작용을 고려한 통합 최적화 필요성 제시

## Recipe/Process Flow 상세

### Pre-OPC vs. Post-OPC SRAF 배치 비교
```
전통적 Pre-OPC SRAF 흐름:
  원본 레이아웃 → SRAF 삽입 → OPC 실행 → 최종 마스크

  문제점:
  - SRAF는 원본 패턴 기준으로 배치
  - OPC가 주 패턴 에지를 이동 → SRAF 위치 최적성 손실
  - OPC 후 SRAF-주패턴 이격 변화

Post-OPC SRAF 흐름:
  원본 레이아웃 → OPC 실행 → SRAF 삽입 → 최종 마스크

  장점:
  - OPC 후 실제 마스크 형상에 최적화된 SRAF 배치
  - SRAF-주패턴 이격이 설계 의도와 일치
  - 더 정확한 공정 윈도우 예측
```

### Post-OPC SRAF 배치 분석 방법론
```
1. OPC 수행
   - 표준 Model-based OPC 실행
   - OPC 후 마스크 형상 분석 (원본 대비 변화량)

2. Post-OPC SRAF 후보 위치 결정
   - OPC 후 마스크의 공간 분석
   - 이격 거리, 밀도 기반 SRAF 위치 결정
   - 원본 규칙 테이블 vs. OPC 후 조정 규칙 비교

3. 공정 윈도우 평가
   - Pre-OPC SRAF와 Post-OPC SRAF 각각에 대해
   - 리소그래피 시뮬레이션 실행
   - DOF, EL, PV 밴드 측정

4. 비교 분석
   - 공정 윈도우 개선량 정량화
   - SRAF 배치 차이의 영향 분리
```

### 핵심 발견
```
OPC 효과:
  - 주 패턴 에지 이동량: 일반적으로 ±수 nm
  - 코너, 라인-엔드에서 더 큰 변화

공정 윈도우:
  - Post-OPC SRAF가 일반적으로 더 나은 PV 밴드
  - 특히 밀집 패턴(dense pattern)에서 효과 두드러짐
  - OPC에 의한 형상 변화가 클수록 개선 효과 증가
```

## OPC 툴 구현 관련성
- **SKOPC OPC+SRAF 순서**: `skopc/recipe/` 배치 실행기에서 OPC → SRAF 순서(post-OPC SRAF) 또는 SRAF → OPC 순서(pre-OPC SRAF) 선택 가능
- **통합 최적화**: OPC와 SRAF를 동시 최적화하는 공동 최적화(co-optimization) 방향 시사
- **공정 윈도우 평가**: `skopc/pwo/` PWO 모듈에서 SRAF 배치 타이밍에 따른 공정 윈도우 차이 분석 가능
- **레시피 설계**: OPC Recipe에서 SRAF 삽입 단계를 OPC 전/후로 설정하는 파라미터 추가 필요성

## 참고문헌
- IEEE Conference Publication 2022, Document 9972322
- 관련: SRAF rule extraction and insertion based on ILT (SPIE 10961, 2019)
- 관련: CTM-SRAF (IEEE TCAD, 2023)
- 관련: Process window tripling by SRAF placement rules (IEEE, 2016)

## 태그
`Recipe`, `IEEE`, `SRAF`, `PostOPC`, `ProcessWindow`, `OPC-SRAF-Interaction`, `PVBand`, `SequentialOptimization`, `2022`
