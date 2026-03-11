# Patterning Assessment Using 0.33NA EUV Single Mask for Next Generation DRAM Manufacturing

## 메타데이터
- **저자**: (SPIE 12495 저자 정보)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950S (2023)
- **DOI/URL**: https://doi.org/10.1117/12.2660763

## 핵심 요약
차세대 DRAM 제조를 위한 0.33NA EUV 단일 마스크 패터닝 가능성을 평가한다. SMO와 에어리얼 이미지 기반 OPC를 사용하여 주 패터닝 마스크의 이미지 데이터를 분류하고 잠재적 취약점을 식별한다. 단일 마스크 EUV 패터닝이 차세대 DRAM에서 실현 가능한지 공정 창과 확률론적 지표로 평가한다.

## 주요 기여
1. **0.33NA EUV 단일 마스크 DRAM 평가**: SMO+OPC로 단일 마스크 패터닝 가능성 분석
2. **취약점 식별**: 에어리얼 이미지 기반 ORC로 핫스팟 패턴 식별
3. **공정 창 평가**: SMO 최적화 후 DOF/EL/LCDU 등 공정 창 메트릭 정량화
4. **DRAM 패턴 적용**: 실제 차세대 DRAM 레이아웃에 SMO/OPC 적용 검증

## 알고리즘/수식
### SMO + OPC 패터닝 평가 플로우
```
단계 1: SMO
  min_{J, M} Cost_SMO(DRAM 패턴)
  Cost_SMO = Σ_i [||CD_i - CD_t||² + w_EPE·||EPE_i||²]
  → 최적 소스 형상 J* 도출

단계 2: 에어리얼 이미지 기반 OPC
  에어리얼 이미지 → CD 예측 → OPC 보정
  → 전체 DRAM 마스크 OPC 완료

단계 3: ORC (Optical Rule Check)
  ORC_fail = {패턴 i : EPE_i > EPE_limit 또는 PW_i < PW_min}
  → 핫스팟 패턴 목록 생성

단계 4: 취약점 분석
  핫스팟 분류: CD 오차, 공정 창 부족, 확률론적 실패 위험
  → 설계/마스크 수정 방향 제시
```

### DRAM 단일 마스크 패터닝 메트릭
```
평가 지표:
  DOF: 焦点 심도 (nm)
  EL: 노출 위도 (%)
  LCDU: 로컬 CD 균일성 (nm)
  P_fail: 확률론적 고장 확률 (ppm)

단일 마스크 vs 이중 마스크 비교:
  단일 마스크: 처리량↑, 오버레이 오차 없음
  이중 마스크: DOF↑, 더 낮은 피치 가능
```

## OPC 툴 SMO 구현 관련성
- DRAM SMO 플로우: SKOPC SMO 모듈의 DRAM 레이어 지원
- ORC 통합: SMO/OPC 후 에어리얼 이미지 기반 ORC 자동 실행
- 단일 마스크 평가: 이중 패터닝 전환 결정을 위한 단일 마스크 SMO 먼저 시도
- 취약점 기반 재최적화: 핫스팟 패턴에 집중한 SMO/OPC 반복 최적화

## 태그
`SMO`, `OPC`, `EUV`, `0p33NA`, `DRAM`, `single_mask`, `ORC`, `hotspot`, `process_window`, `LCDU`, `DTCO`, `SPIE`, `2023`
