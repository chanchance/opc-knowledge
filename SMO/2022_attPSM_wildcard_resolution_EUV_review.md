# Attenuated Phase Shift Masks: A Wild Card Resolution Enhancement for Extreme Ultraviolet Lithography?

## 메타데이터
- **저자**: (JMM 저자 정보)
- **연도**: 2022
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology (JMM), Vol. 21, Issue 2, 020901
- **DOI/URL**: https://doi.org/10.1117/1.JMM.21.2.020901

## 핵심 요약
EUV 리소그래피에서 감쇠형 위상 이동 마스크(attPSM)의 해상도 향상 가능성을 종합 검토한다. attPSM의 근본 이미징 특성에 대한 모델링과 이해를 중심으로, 대안 흡수층 재료와 이미징 성능에 대한 발표된 연구를 체계적으로 정리한다.

## 주요 기여
1. **attPSM EUV 종합 리뷰**: 발표된 연구의 체계적 검토 및 정리
2. **이미징 특성 모델링**: attPSM의 근본 광학 특성 및 이미징 원리 분석
3. **대안 흡수층 재료 비교**: 다양한 재료의 (n, k)에 따른 attPSM 성능 비교
4. **EUV attPSM 실용화 로드맵**: 이론적 가능성과 제조 도전 과제 정리

## 알고리즘/수식
### attPSM 이미징 모델
```
attPSM 전달 함수:
  T_attPSM(f) = T_PSM_fundamental + T_PSM_M3D

attPSM 파라미터:
  투과율 (반사율): R_att = |r_att|²
  위상 이동: φ = arg(r_att) ≈ π (반전상)

이미지 대비 향상 메커니즘:
  부분 반사 + 위상 반전 → 엣지 근방 전기장 부분 상쇄
  → 이미지 대비 향상 (NILS ↑)
  → 공정 창 개선 (DOF ↑, EL ↑)

M3D와 attPSM 상호작용:
  위상 이동 효과 + M3D 효과 → 복잡한 상호작용
  → 엄격한 RCWA 시뮬레이션 필요
```

### attPSM 재료 설계 공간
```
EUV 반사율 기준:
  이진 마스크 (TaBN): R ≈ 0.5%
  attPSM 목표: R ≈ 5~20%
  위상 목표: φ ≈ 180°

재료별 특성:
  Ru, Rh 등 전이금속: EUV 범위 특정 (n, k) 가능
  Mo 기반: 기존 EUV 마스크 다층막 재료와 호환

최적화 기준:
  R_att, φ 동시 만족하는 재료 + 두께 조합 탐색
```

## OPC 툴 SMO 구현 관련성
- attPSM 이미징 모델 리뷰: SKOPC OPC/SMO에서 attPSM 모델 설계 기초
- 재료별 (n, k) 데이터베이스: 다양한 흡수층 재료의 OPC 모델 파라미터
- SMO와 attPSM 결합 최적화: attPSM 특성에 맞는 소스 형상 최적화
- EUV 마스크 기술 옵션 정리: TaBN / low-n / attPSM 선택 기준 제공

## 태그
`EUV`, `attPSM`, `phase_shift_mask`, `alternative_absorber`, `resolution_enhancement`, `NILS`, `M3D`, `imaging_model`, `OPC`, `SMO`, `JMM`, `2022`
