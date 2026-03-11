# Etch Proximity Correction by Integrated Model-Based Retargeting and OPC Flow

## 메타데이터
- **저자**: Shumay Shang, Yuri Granik, Martin Niehoff
- **연도**: 2007
- **게재지**: Proc. SPIE 6730, Photomask Technology 2007, 67302G
- **DOI/URL**: https://doi.org/10.1117/12.746773

## 핵심 요약
기존 model-based OPC는 광학 및 레지스트 proximity 효과만 보정하고 etch proximity 효과는 별도로 처리하거나 무시한다. 본 논문은 etch와 optical/resist 공정 효과를 모델 캘리브레이션과 레이아웃 보정 양쪽에서 분리하는 통합 플로우를 제안한다. 이 이중 분리(double separation)로 etch 및 resist 타겟 제어가 용이해지고 OPC 런타임이 대폭 감소한다.

## 주요 기여
1. **이중 분리 원칙**: etch 효과와 optical/resist 효과를 (1) 모델 캘리브레이션과 (2) 레이아웃 보정 양쪽에서 동시 분리
2. **통합 Retargeting-OPC 플로우**: etch proximity 보정을 retargeting 단계로, optical 보정을 OPC 단계로 분리
3. **OPC 런타임 감소**: etch 효과 분리로 OPC 모델 복잡도 감소 → 수렴 속도 향상
4. **이중 레벨 검증**: resist 레벨 및 etch 레벨 양쪽에서 post-OPC 검증 가능
5. **etch 타겟 제어**: etch 공정 변동에 독립적인 정밀 타겟 설정 가능

## Recipe/Flow 상세
- **통합 Etch-OPC 플로우**:
  1. **모델 캘리브레이션 분리**:
     - Optical/Resist 모델: 광학 이미지 → 레지스트 윤곽 매핑
     - Etch 모델: 레지스트 윤곽 → 최종 etch 윤곽 매핑 (독립 캘리브레이션)
  2. **레이아웃 보정 분리**:
     - **Step 1 – Etch Retargeting**: 설계 타겟에 etch 바이어스 적용
       → 레지스트 타겟 = 설계 타겟 + etch_bias(local_density, CD, pattern_type)
     - **Step 2 – OPC**: retargeting된 레지스트 타겟을 기반으로 optical/resist OPC 수행
  3. **이중 레벨 Post-OPC 검증**:
     - Resist 레벨 검증: optical/resist 모델로 시뮬레이션
     - Etch 레벨 검증: etch 모델 추가 적용하여 최종 CD 검증
- **Etch 모델 파라미터**: 국소 패턴 밀도, CD, 형상 타입(line, contact, corner)
- **대상 레이어**: critical 레이어 전반 (gate, metal, contact)
- **런타임 효과**: etch 효과 분리로 OPC 모델 단순화 → 런타임 대폭 감소

## OPC 툴 구현 관련성
- SKOPC 모델링 모듈의 etch 모델 분리 구조 직접 참고 가능
- `etch_model.py`: 독립 etch proximity 모델 캘리브레이션
- OPC 플로우에 retargeting 단계(etch bias pre-correction) 삽입 방법
- 이중 레벨 검증: `opc_verify.py`에 etch 레벨 검증 레이어 추가

## 태그
`EtchProximity`, `Retargeting`, `OPC`, `ModelBased`, `EtchModel`, `DoubleSeparation`, `SPIE`, `2007`
