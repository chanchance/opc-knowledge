# Advancing EUV Patterning Through Pattern Shaping at Intel 18A Process Technology Node

## 메타데이터
- **저자**: Intel (저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE (DTCO and Computational Patterning III 또는 관련 학회, 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010982

## 핵심 요약
Intel 18A 공정 기술 노드에서 패턴 쉐이핑(pattern shaping)을 통한 EUV 패터닝 발전을 다룬다. EUV 직접 인쇄가 피치 스케일링과 설계 규칙 유연성에 효과적임을 실증하고, 피처 크기 축소에 따른 확률론적 노이즈 도전 과제에 대응하는 혁신적인 패턴 쉐이핑 솔루션을 제시한다.

## 주요 기여
1. **패턴 쉐이핑 전략**: 확률론적 노이즈 완화를 위한 마스크 패턴 형상 최적화
2. **Intel 18A 확장**: EUV 직접 인쇄의 Intel 18A 스케일링 도전 과제 해결
3. **확률론적 솔루션**: EUV 스케일링에서 확률론적 노이즈를 억제하는 패턴 쉐이핑
4. **OPC/ILT 통합**: 패턴 쉐이핑을 OPC/ILT 플로우에 통합하는 방법론

## 알고리즘/수식
### 패턴 쉐이핑 기반 확률론적 노이즈 완화
```
확률론적 도전:
  피처 크기 축소 → 광자 수 감소
  → 확률론적 노이즈 증가
  P_fail ∝ exp(-NILS² × dose / (2σ_stoch²))

패턴 쉐이핑 전략:
  마스크 패턴 형상 변형:
    라인 끝단 → 둥근 끝단(rounded tip)
    코너 → 곡선형 코너
  목적: 웨이퍼 이미지 콘트라스트 향상
  → NILS 증가 → P_fail 감소

ILT/OPC 기반 패턴 쉐이핑:
  곡선형 ILT: 자연스럽게 최적 패턴 형상 생성
  OPC 패턴 쉐이핑: 규칙 기반 + 모델 기반 조합
```

### Intel 18A 확률론적 성능
```
패턴 쉐이핑 효과:
  ΔNILS = NILS_shaped - NILS_standard > 0
  ΔP_fail = P_fail_shaped - P_fail_standard < 0
  → 동일 도즈에서 더 낮은 결함률

수율 개선:
  수율 = exp(-D_stoch × A_chip)
  D_stoch 감소 → 수율 향상
  Intel 18A 타겟 수율 달성

설계 규칙 영향:
  패턴 쉐이핑 허용 → 곡선형 마스크 필요
  MBMW + MRC 준수 하에서 최적화
```

## OPC 툴 SMO 구현 관련성
- 패턴 쉐이핑 OPC: SKOPC OPC 엔진에서 확률론적 노이즈 완화용 패턴 쉐이핑 지원
- 확률론적 인식 ILT: EUV 확률론적 결함 최소화를 목표로 하는 ILT 최적화
- Intel 18A 벤치마크: 타이트 피치 EUV 패터닝 OPC 성능 기준 데이터
- 곡선형 마스크 연계: 패턴 쉐이핑이 필요로 하는 곡선형 마스크 OPC 플로우

## 태그
`EUV`, `Intel_18A`, `pattern_shaping`, `stochastic`, `OPC`, `ILT`, `curvilinear`, `yield`, `NILS`, `P_fail`, `SPIE`, `2024`
