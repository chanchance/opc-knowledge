# Increasing Throughput in EUV Logic Applications with Thinner Low-n Masks and Wavefront Optimization

## 메타데이터
- **저자**: (SPIE 13215 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 13215, Optical and EUV Nanolithography XXXVII, 1321505 (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3033432

## 핵심 요약
파면(wavefront) 최적화와 저굴절률(low-n) 마스크 흡수층 박막화를 결합하여 EUV 로직 응용에서 처리량(throughput)을 향상시키는 방법을 제시한다. Low-n 흡수층을 24~26nm로 얇게 만들고 파면 최적화를 통해 단일 인쇄 EUV 로직 응용에서 20~30%의 도즈 감소를 달성한다.

## 주요 기여
1. **Low-n 흡수층 박막화**: 24~26nm 두께 low-n 흡수층으로 M3D 효과 완화
2. **파면 최적화**: 박막 low-n 마스크에 최적화된 파면(소스 형상 + 수차 보정)
3. **도즈 20~30% 감소**: 박막 low-n + 파면 최적화로 필요 노출 도즈 대폭 감소
4. **처리량 향상**: 도즈 감소 → EUV 스캐너 처리량 직접 향상

## 알고리즘/수식
### Low-n 박막 마스크 + 파면 최적화 프레임워크
```
Low-n 흡수층 박막화 효과:
  두꺼운 TaBN (~60nm): 강한 M3D 효과, 높은 도즈 필요
  박막 low-n (~24nm): M3D 효과 감소, NILS 향상

  M3D 보정 감소:
    ΔCD_M3D(t_abs = 24nm) < ΔCD_M3D(t_abs = 60nm)

파면 최적화 (SMO 유사):
  min_{J, W} ||CD_litho(J, M_low-n, W) - CD_target||²
  변수:
    J: 소스 형상 (pixelated illumination)
    W: 파면 수차 보정 항 (lens heating 보상 등)

도즈 감소 메커니즘:
  NILS_low-n > NILS_TaBN → 더 낮은 도즈에서 안정적 CD
  Dose_required ∝ 1 / NILS²
  → NILS 향상 → 도즈 20~30% 감소
```

### 처리량-성능 트레이드오프
```
처리량 향상:
  Throughput ∝ 1 / Dose_required
  도즈 20~30% 감소 → 처리량 25~43% 향상

성능 유지 조건:
  CD_uniformity, LWR, EPE: 도즈 감소 후에도 스펙 충족
  파면 최적화로 성능 유지 보장
```

## OPC 툴 SMO 구현 관련성
- 박막 low-n 마스크 SMO: SKOPC SMO에서 흡수층 두께 파라미터 포함 최적화
- 파면 최적화 통합: 소스 최적화 + 수차 보정을 결합한 파면 SMO
- 도즈 목표 SMO: 처리량 향상을 위한 도즈 최소화 SMO 비용 함수
- EUV 로직 응용: 단일 인쇄 로직 레이어에서 SMO/파면 최적화 활용

## 태그
`EUV`, `low_n`, `thin_absorber`, `wavefront_optimization`, `throughput`, `dose_reduction`, `SMO`, `logic`, `NILS`, `M3D`, `SPIE`, `2024`
