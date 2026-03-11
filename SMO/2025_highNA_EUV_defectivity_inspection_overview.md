# High-NA EUV Defectivity Inspection: Overview and Challenges

## 메타데이터
- **저자**: C. Beral et al.
- **연도**: 2025
- **게재지**: Proc. SPIE 13426, Metrology, Inspection, and Process Control XXXIX, 134261H (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051293

## 핵심 요약
고NA EUV 리소그래피(0.55NA)에서의 결함 검사 현황과 도전 과제를 종합적으로 다룬다. 최초 0.55NA 웨이퍼 노출 이후 고NA 스캐너에서 프로그램 결함의 마스크-웨이퍼 인쇄 가능성과 리소그래피(ADI) 및 에칭(AEI) 단계별 결함 진화를 분석한다. 마이크로브리지, 확률론적 결함, 라인 에지 거칠기 등 고NA EUV 특유의 결함 증가 가능성을 평가한다.

## 주요 기여
1. **고NA EUV 결함 검사 현황**: 0.55NA에서의 결함 유형 및 밀도 최초 분석
2. **마스크-웨이퍼 결함 전사 분석**: 마스크 결함의 ADI/AEI 단계별 웨이퍼 영향
3. **고NA 특유 결함 식별**: 마이크로브리지, 확률론적 결함, LER 변화 분석
4. **결함 검사 도전 과제**: 더 높은 해상도와 좁아진 결함 허용 공간에서의 검사 한계

## 알고리즘/수식
### 고NA EUV 결함 분석 프레임워크
```
고NA EUV 결함 유형:
  1. 마이크로브리지(microbridge):
     인접 피처 연결 → 높은 해상도에서 증가
     P_bridge ∝ exp(-gap²/(2σ_stoch²))

  2. 확률론적 결함:
     광자 샷 노이즈 → 국소 도즈 변동
     P_stoch = f(photon_count, NILS)

  3. LER/LWR 변화:
     고NA에서 더 좁은 피처 → LER 영향 증가
     LER ∝ 1/NILS × resist_noise

결함 검사 단계:
  ADI (After Develop Inspection): 현상 직후
  AEI (After Etch Inspection): 에칭 후
  결함 전파율: P_print(ADI) → P_fail(AEI)
```

### 결함 허용 공간 분석
```
고NA EUV 결함 허용:
  더 좁은 피처 → 더 작은 CD 허용 공간
  ΔCD_fail = CD_nominal - CD_min (결함 임계값)

결함 검사 민감도 요구:
  검출 한계 < 결함 크기 (수 nm 수준)
  고NA EUV에서 더 작은 결함 검출 필요

검사 도전 과제:
  광학 검사: 해상도 한계 (193nm DUV 검사 도구)
  eBeam 검사: 처리량 제한
  → 고NA 전용 새로운 검사 도구 필요
```

## OPC 툴 SMO 구현 관련성
- 결함 인식 OPC: 고NA EUV 결함 유형을 OPC 최적화 비용 함수에 반영
- 마이크로브리지 방지: OPC에서 인접 피처 간격 CD 마진 확보
- 확률론적 OPC: P_fail 맵 기반 고NA EUV 결함 예방적 OPC
- 검사 루프 통합: OPC 결과의 결함 검사 데이터 기반 교정 루프

## 태그
`high_NA`, `EUV`, `0.55NA`, `defectivity`, `inspection`, `microbridge`, `stochastic`, `LER`, `ADI`, `AEI`, `SPIE`, `2025`
