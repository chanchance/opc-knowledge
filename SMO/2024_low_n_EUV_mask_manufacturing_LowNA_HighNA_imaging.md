# Low-n Absorber EUV Masks: Mask Manufacturing Assessment Through Process Characterization and Optimization with Early Look at EUV Low-NA and High-NA Imaging Performance

## 메타데이터
- **저자**: (SPIE 13216 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 13216, Photomask Technology + EUV Lithography 2024, 132160C (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3037087

## 핵심 요약
저굴절률(low-n) 흡수층 EUV 마스크의 제조 가능성을 공정 특성화와 최적화를 통해 평가하고, 0.33NA(Low-NA) 및 0.55NA(High-NA) EUV 이미징 성능을 초기 결과로 제시한다. Low-n 마스크 제조 공정의 완성도와 이미징 성능 간의 관계를 분석한다.

## 주요 기여
1. **Low-n 마스크 제조 평가**: 공정 특성화로 low-n 흡수층 마스크 제조 가능성 검증
2. **0.33NA vs 0.55NA 이미징 비교**: Low-NA와 High-NA EUV에서 low-n 마스크 성능 비교
3. **공정 최적화**: Low-n 흡수층 증착/패터닝 공정 파라미터 최적화
4. **이미징 성능 정량화**: SMO/OPC와 결합한 low-n 마스크 이미징 메트릭 측정

## 알고리즘/수식
### Low-n 마스크 제조-이미징 연계 분석
```
Low-n 흡수층 특성:
  굴절률: n < 1.0 at λ=13.5nm (표준 TaBN n ≈ 0.94, k ≈ 0.04)
  low-n 목표: n << 0.94, 위상 이동 최소화

제조 공정 파라미터:
  증착 조건 (sputter 타겟, 가스 비율, 압력)
  패터닝 조건 (e-beam lithography, etch)
  MRC 충족 여부

이미징 성능 (0.33NA vs 0.55NA):
  NILS(low-n, 0.33NA) > NILS(TaBN, 0.33NA)
  NILS(low-n, 0.55NA) vs NILS(TaBN, 0.55NA): 비교 분석

M3D 효과:
  low-n 흡수층: M3D 효과 감소 (위상 이동 감소)
  → 0.55NA에서 더 강한 M3D → low-n의 이점 더 큼
```

### SMO/OPC와 Low-n 마스크 결합
```
Low-n 마스크 SMO:
  소스 최적화: low-n 마스크에 맞는 최적 조명 형상
  OPC 보정: low-n 마스크 OPC 모델로 CD 보정

성능 메트릭:
  DOF, EL, LCDU (0.33NA, 0.55NA 각각 측정)
  CD 균일성: 제조 공정 변동 포함
```

## OPC 툴 SMO 구현 관련성
- Low-n 마스크 제조-이미징 연계: SKOPC에서 low-n 마스크 공정 변동 고려 OPC
- 0.33NA/0.55NA 이중 지원: 두 NA 모드에서 low-n 마스크 SMO/OPC 통합
- 마스크 제조 공정 인식 OPC: 제조 공정 변동을 OPC 비용 함수에 반영
- High-NA EUV 마스크 기술 로드맵: low-n 마스크의 0.55NA 적용 준비

## 태그
`EUV`, `low_n`, `mask_manufacturing`, `0p33NA`, `0p55NA`, `high_NA`, `imaging`, `SMO`, `OPC`, `process_characterization`, `SPIE`, `2024`
