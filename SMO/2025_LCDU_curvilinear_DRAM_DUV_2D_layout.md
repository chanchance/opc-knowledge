# LCDU Enhancement of 2D Layout Through Curvilinear Solutions for DRAM DUV Critical Layers

## 메타데이터
- **저자**: (SPIE 13424 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 1342414 (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3050267

## 핵심 요약
DRAM DUV 임계 레이어의 2D 레이아웃에서 곡선형 마스크 솔루션을 통한 LCDU(Local Critical Dimension Uniformity) 향상을 연구한다. ILT/곡선형 OPC를 DUV DRAM 핵심 레이어에 적용하여 CD 균일성을 개선하고, 2D 복잡 패턴에서 기존 직선형 마스크 대비 LCDU 향상 효과를 정량화한다.

## 주요 기여
1. **DRAM DUV 곡선형 솔루션**: DUV 리소그래피 DRAM 임계 레이어에 곡선형 마스크 적용
2. **LCDU 향상**: 2D 레이아웃에서 ILT/곡선형 OPC로 국소 CD 균일성 개선
3. **2D 패턴 최적화**: 복잡한 DRAM 2D 패턴에서 곡선형 마스크 효과 검증
4. **MBMW 활용**: 다중 빔 마스크 라이터를 통한 곡선형 DRAM 마스크 제조

## 알고리즘/수식
### DRAM 2D 레이아웃 곡선형 OPC
```
DRAM DUV 임계 레이어 특성:
  레이어: 활성 영역, 게이트 레이어, 컨택 레이어
  패턴: 2D 복잡 구조 (코너, T-접합, 끝단 등)
  요구사항: LCDU < 목표값 (수율 보장)

기존 직선형 OPC 한계:
  2D 피처 코너에서 광학 근접 효과
  → LCDU 저하, 코너 라운딩
  → 수율 손실

곡선형 마스크 OPC (ILT):
  min_{M_curv} LCDU(aerial image)
  M_curv: 곡선형 마스크 (B-spline/픽셀)
  → 코너, 끝단, 2D 전환부 최적화
  → 직선형 대비 LCDU 향상
```

### LCDU 향상 메트릭
```
LCDU 정의:
  LCDU = 3σ(CD_local - CD_mean)
  국소 CD 편차의 3시그마

곡선형 OPC 효과:
  ΔLCDU = LCDU_rectilinear - LCDU_curvilinear
  > 0: 곡선형 마스크가 더 균일한 CD

DRAM 2D 레이아웃 적용:
  코너 피처: LCDU 개선 두드러짐
  라인끝: 끝단 단축 감소
  T-접합: 선폭 변동 감소
```

## OPC 툴 SMO 구현 관련성
- DRAM 곡선형 OPC: SKOPC에서 DUV DRAM 레이어용 곡선형 ILT/OPC 지원
- LCDU 기반 최적화: OPC 비용 함수에 LCDU 항 추가하여 CD 균일성 최적화
- 2D 패턴 곡선형: 복잡한 2D 레이아웃에서 곡선형 마스크 생성 알고리즘
- DUV DRAM 확장: EUV뿐만 아니라 DUV DRAM에도 곡선형 솔루션 적용

## 태그
`LCDU`, `curvilinear`, `DRAM`, `DUV`, `2D_layout`, `ILT`, `OPC`, `CD_uniformity`, `MBMW`, `SPIE`, `2025`
