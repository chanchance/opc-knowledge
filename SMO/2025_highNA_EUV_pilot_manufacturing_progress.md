# Progress Towards Adoption of High-NA EUV Lithography in Pilot Manufacturing

## 메타데이터
- **저자**: Herman Heijmerikx et al.
- **연도**: 2025
- **게재지**: Proc. SPIE PC13424, Optical and EUV Nanolithography XXXVIII, PC134240H (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051022

## 핵심 요약
고NA EUV 리소그래피(0.55NA)의 파일럿 양산 도입 진행 현황을 종합적으로 보고한다. TWINSCAN EXE:5000/5200 시스템의 파일럿 제조 환경 도입 진척 상황, 기술적 도전 과제 해결 현황, 그리고 실제 생산 환경에서의 성능 데이터를 제시한다.

## 주요 기여
1. **파일럿 양산 현황 보고**: 0.55NA EUV 시스템의 파일럿 제조 도입 진척 상황
2. **기술적 도전 과제 해결**: 스티칭, 오버레이, 처리량 등 핵심 도전 과제 해결 방안
3. **성능 데이터 제시**: 파일럿 환경에서의 패터닝 성능 (CD, 오버레이, 처리량) 측정
4. **양산 로드맵**: 파일럿에서 고NA EUV 본격 양산으로의 전환 일정

## 알고리즘/수식
### 고NA EUV 파일럿 양산 핵심 지표
```
TWINSCAN EXE:5000/5200 성능 목표:
  NA = 0.55 (아나모픽)
  웨이퍼/시간: >100 WPH (목표)
  오버레이: <2nm (3σ)
  스티칭 정밀도: <1nm (3σ)

파일럿 양산 도전 과제:
  1. 스티칭 수율:
     스티칭 경계 CD 불일치 → 수율 손실
     OPC/RET 최적화로 개선

  2. 오버레이 관리:
     두 번 노출 간 오버레이 오차
     SMASH 센서 + 피드백 제어

  3. 처리량:
     스티칭으로 인한 노출 횟수 2배
     → UPH (Usable Wafers Per Hour) 분석
```

### 양산 도입 진척
```
도입 단계:
  Phase 1: 설치/검증 (베타 도구)
  Phase 2: 파일럿 공정 개발
  Phase 3: 파일럿 양산
  Phase 4: 고NA EUV 본격 양산 (2026-2027)

OPC/SMO 준비 상태:
  스티칭 인식 OPC 플로우 완성도
  고NA EUV 모델 교정 데이터 충족
  → SMO/OPC 준비 상태 파일럿에서 검증
```

## OPC 툴 SMO 구현 관련성
- 파일럿 양산 OPC: 실제 고NA EUV 파일럿 환경에서의 OPC 검증 데이터
- 스티칭 OPC 검증: 파일럿 양산에서 스티칭 OPC 성능 실증
- 오버레이 인식 OPC: 두 노출 간 오버레이를 고려한 OPC 전략
- 처리량-품질 트레이드오프: 파일럿에서 검증된 OPC 최적화 vs 처리량 균형

## 태그
`high_NA`, `EUV`, `0.55NA`, `pilot_manufacturing`, `EXE5000`, `EXE5200`, `stitching`, `overlay`, `throughput`, `OPC`, `SMO`, `SPIE`, `2025`
