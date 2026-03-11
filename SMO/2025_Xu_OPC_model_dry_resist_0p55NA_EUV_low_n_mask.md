# OPC Model Accuracy of Dry Resist Readiness for 0.55NA EUVL by Using Low-n Bright Field Mask

## 메타데이터
- **저자**: Dongbo Xu et al.
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250Y (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051855

## 핵심 요약
0.55NA EUV 리소그래피에서 건식 레지스트(dry resist)의 OPC 모델 정확도를 검증한다. imec N2 설계(28nm 피치 금속 레이어)에서 low-n 밝은 필드 감쇠 위상 이동 마스크를 사용하여 건식 레지스트의 0.55NA EUV 패터닝 준비 상태를 평가하고, OPC 모델 보정 방법론을 제시한다.

## 주요 기여
1. **0.55NA 건식 레지스트 OPC 모델 검증**: 고NA EUV에서 dry resist OPC 모델 정확도 평가
2. **Low-n BF 마스크 조합**: 저굴절률 밝은 필드 마스크와 건식 레지스트의 시너지 효과
3. **imec N2 설계 적용**: 28nm 피치 메탈 레이어에서 실제 설계 OPC 검증
4. **0.55NA 준비 상태 평가**: 건식 레지스트의 고NA EUV 생산 준비 상태 정량화

## 알고리즘/수식
### 0.55NA 건식 레지스트 OPC 모델
```
0.55NA EUV 광학 설정:
  NA = 0.55 (아나모픽: NA_x = 0.55, NA_y = 0.33)
  배율: M_x = 4x, M_y = 8x
  타겟 레이어: imec N2 메탈 (28nm 피치)

Low-n BF 마스크 특성:
  기존 TaBN 흡수층 대신 low-n 재료
  밝은 필드(bright field) 구성
  → 위상 이동 효과 + M3D 감소

건식 레지스트 OPC 모델 보정:
  min_{θ} Σ_CD ||CD_model(θ) - CD_meas||²
  건식 레지스트 특화 파라미터:
    - 건식 현상 계수 (dry development)
    - 도즈-CD 감도 (습식 대비 향상)
    - LWR 특성
```

### 0.55NA 패터닝 성능
```
28nm 피치 메탈 패터닝:
  0.55NA EUV + dry resist + low-n BF 마스크
  → 더 낮은 LCDU (국소 CD 균일성 향상)
  → 더 작은 LWR (라인 에지 거칠기)

OPC 모델 정확도 지표:
  3σ(CD_model - CD_meas) < 목표값
  평균 절대 오차 (MAE) < 1nm 목표
  다양한 피처 타입에서 일관된 정확도
```

## OPC 툴 SMO 구현 관련성
- 0.55NA 건식 레지스트 OPC: SKOPC에서 고NA EUV dry resist 전용 모델 지원 필요
- Low-n BF 마스크 OPC: 새로운 마스크 기술과 레지스트 조합 OPC 모델링
- imec N2 호환: 최첨단 노드 설계 OPC 검증 데이터
- 고NA EUV 전환: 0.33NA에서 0.55NA 전환 시 OPC 모델 업데이트 전략

## 태그
`OPC`, `dry_resist`, `0.55NA`, `EUV`, `low_n_mask`, `bright_field`, `model_accuracy`, `N2`, `28nm_pitch`, `imec`, `SPIE`, `2025`
