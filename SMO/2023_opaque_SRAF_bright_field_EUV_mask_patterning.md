# EUV Mask Patterning Process to Enable Opaque SRAFs for Bright Field EUV Mask Imaging

## 메타데이터
- **저자**: (SPIE 12751 저자 정보)
- **연도**: 2023
- **게재지**: Proc. SPIE 12751, Photomask Technology 2023, 127510M (21 November 2023)
- **DOI/URL**: https://doi.org/10.1117/12.2689665

## 핵심 요약
밝은 필드(bright field) EUV 마스크 이미징에서 불투명(opaque) SRAF를 구현하기 위한 EUV 마스크 패터닝 공정을 개발한다. SRAF는 밝은 필드와 어두운 필드 이미징 모두 공정 창을 최대화하는 데 중요한 도구이며, 불투명 SRAF를 통해 밝은 필드 EUV 마스크에서도 SRAF의 이점을 활용할 수 있는 마스크 제조 공정을 제시한다.

## 주요 기여
1. **불투명 SRAF EUV 마스크 공정**: 밝은 필드 마스크에서 불투명 SRAF 구현 마스크 제조 공정
2. **밝은/어두운 필드 SRAF 비교**: 두 톤에서 SRAF 적용 가능성 및 공정 창 향상 비교
3. **공정 창 최대화**: SRAF로 밝은 필드 EUV 마스크의 공정 창 향상 정량화
4. **마스크 제조 가능성**: 불투명 SRAF를 포함한 밝은 필드 마스크의 제조 가능성 검증

## 알고리즘/수식
### 밝은/어두운 필드 EUV 마스크와 SRAF
```
어두운 필드(Dark Field) 마스크:
  배경: 반사 (밝음)
  패턴: 흡수 (어두움)
  SRAF: 소형 흡수 피처 → 기존 SRAF 방식과 동일

밝은 필드(Bright Field) 마스크:
  배경: 흡수 (어두움)
  패턴: 반사 (밝음)
  SRAF: 소형 반사 피처 → 불투명 SRAF 필요
  문제: 밝은 필드 마스크에서 SRAF = 반사 → 별도 공정 필요

불투명 SRAF:
  밝은 필드 마스크에 흡수 SRAF 추가
  → 추가 마스크 패터닝 공정 필요
  → 공정 창 향상 효과: ΔNILS, ΔDOF 정량화
```

### SRAF 공정 창 기여
```
SRAF 없는 공정 창:
  DOF_no_SRAF, EL_no_SRAF

SRAF 있는 공정 창 (불투명 SRAF):
  DOF_SRAF > DOF_no_SRAF
  EL_SRAF > EL_no_SRAF

SRAF 위치/크기 최적화:
  SRAF_pos*, SRAF_width* = argmax_{pos, width} DOF × EL
  subject to: MRC(SRAF) ≥ MRC_min
```

## OPC 툴 SMO 구현 관련성
- 밝은 필드 마스크 SRAF: SKOPC SMO/OPC에서 밝은 필드 톤의 SRAF 삽입 지원
- 불투명 SRAF 최적화: SMO 비용 함수에서 SRAF 위치/크기 최적화 확장
- 톤 선택 + SMO: 밝은/어두운 필드 톤 선택과 SMO 결합 최적화
- EUV 마스크 제조 연계: 불투명 SRAF 공정 가능 여부를 OPC/SMO 제약으로 반영

## 태그
`EUV`, `SRAF`, `bright_field`, `dark_field`, `opaque_SRAF`, `mask_patterning`, `process_window`, `DOF`, `EL`, `SMO`, `OPC`, `SPIE`, `2023`
