# Using Programmed Defect Vehicle to Understand Printability of Defect/2D Structures and Characterize It Through EUV Process Impact

## 메타데이터
- **저자**: (SPIE 13426 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13426, Metrology, Inspection, and Process Control XXXIX, 3052510 (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3052510

## 핵심 요약
프로그램 결함 벡터(programmed defect vehicle)를 이용하여 EUV 리소그래피에서 결함/2D 구조의 인쇄 가능성을 이해하고 EUV 공정 영향을 분석한다. P28 라인-스페이스 피처에서의 브리지(bridge)와 브레이크(break) 결함의 마스크-웨이퍼 전사 특성을 분석하여 OPC 기반 결함 완화 전략에 활용한다.

## 주요 기여
1. **프로그램 결함 벡터 설계**: 다양한 유형의 결함을 체계적으로 검사하는 테스트 패턴 개발
2. **EUV 결함 인쇄 가능성 분석**: 마스크 결함의 EUV 리소그래피 후 웨이퍼 전사 특성
3. **2D 구조 결함 특성화**: 라인-스페이스, 컨택, 비아 등 2D 피처에서의 결함 거동
4. **공정 영향 분석**: ADI(After Develop Inspection) 및 AEI(After Etch Inspection) 단계별 결함 진화

## 알고리즘/수식
### 프로그램 결함 인쇄 가능성 모델
```
결함 유형 (P28 L/S 기준):
  브리지(bridge): 인접 라인 연결 결함
    크기: d_bridge (브리지 폭)
    임계값: d_bridge > d_crit → 인쇄됨
  브레이크(break): 라인 단절 결함
    크기: d_break (단절 길이)
    임계값: d_break > d_crit → 인쇄됨

MEEF 분석:
  CD_wafer_defect = MEEF × CD_mask_defect / M
  결함 크기별 MEEF 특성 → 결함 인쇄 임계값

결함 인쇄 가능성:
  P_print(d) = Φ((d - d_crit) / σ_print)
  σ_print: 인쇄 공정 변동
```

### 공정 영향 분석
```
마스크 → ADI → AEI 결함 전파:
  d_ADI = f(d_mask, exposure_conditions)
  d_AEI = g(d_ADI, etch_conditions)

OPC 완화 전략:
  결함 위치에서 OPC 바이어스 조정
  → 결함 주변 CD 마진 확보
  → 결함 인쇄 가능성 감소

결함 회피 전략:
  패턴 이동(pattern shift): 결함을 비임계 위치로
  OPC 보정: 결함 영향 최소화
```

## OPC 툴 SMO 구현 관련성
- 결함 인식 OPC: 마스크 결함 위치와 크기를 고려한 OPC 보정 전략
- 프로그램 결함 데이터: OPC 모델 검증을 위한 체계적인 결함 인쇄 데이터
- 결함 완화 OPC: 결함 주변 OPC 바이어스 조정으로 인쇄 가능성 감소
- SMO 결함 강건성: 마스크 결함에 강건한 소스 최적화 전략

## 태그
`EUV`, `defect`, `printability`, `programmed_defect`, `bridge`, `break`, `P28`, `OPC`, `ADI`, `AEI`, `MEEF`, `SPIE`, `2025`
