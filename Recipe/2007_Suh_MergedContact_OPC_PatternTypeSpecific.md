# Merged Contact OPC Using Pattern Type Specific Modeling and Correction

## 메타데이터
- **저자**: Sungsoo Suh, Sangwook Kim, Sukjoo Lee, Youngchang Kim, Junghyeon Lee, Changjin Kang
- **연도**: 2007
- **게재지**: Proc. SPIE 6607, Photomask and Next-Generation Lithography Mask Technology XIV, 66071O
- **DOI/URL**: https://doi.org/10.1117/12.728971

## 핵심 요약
Contact hole 레이어에서 인접한 contact 홀들이 병합(merge)되거나 서로 매우 근접한 "merged contact" 패턴은 일반적인 model-based OPC로 정확히 보정하기 어렵다. 본 논문은 패턴 타입별 특화 모델링과 보정을 사용하여 merged contact OPC의 정확도를 향상시키는 방법을 제시한다.

## 주요 기여
1. **패턴 타입 분류**: Merged contact, 고립 contact, 밀집 contact 등 타입별 분리 모델링
2. **타입별 특화 OPC 모델**: 각 패턴 타입에 최적화된 별도 OPC 모델 구축 및 적용
3. **Merged contact 처리**: 병합 contact 특유의 광학 근접 효과를 정확히 캡처
4. **OPC 정확도 향상**: 단일 모델 대비 패턴 타입별 모델의 CD 오차 감소
5. **실용적 플로우**: 패턴 타입 자동 분류 → 해당 모델 적용의 자동화 플로우

## Recipe/Flow 상세
- **Merged Contact 패턴 타입별 OPC 플로우**:
  1. **패턴 타입 분류**:
     - 고립 contact: 주변 contact과의 거리 > 임계값
     - 밀집 contact: 규칙적 배열의 contact array
     - Merged contact: 두 contact 홀이 병합되어 연장된 슬롯 형태
     - 반고립 contact: 중간 거리 범위
  2. **타입별 모델 캘리브레이션**:
     - 각 타입의 대표 패턴으로 별도 OPC 모델 학습
     - 병합 contact의 장축/단축 방향 광학 거동 개별 캘리브레이션
  3. **타입별 OPC 적용**:
     - 분류된 각 패턴에 해당 전문 모델로 OPC 수행
     - 타입 경계 영역은 블렌딩(blending) 처리
  4. **검증**: 각 타입별 CD 오차 및 공정 창 평가
- **Merged contact 특수 처리**:
  - 장축 방향: 라인 엔드 pullback 보정 중요
  - 단축 방향: CD 균일도 유지
  - 코너 처리: 광 산란에 의한 코너 라운딩 보정
- **적용 기술 노드**: 60~90nm급 logic contact 레이어

## OPC 툴 구현 관련성
- Contact/via 레이어 OPC에서 패턴 타입 분류 및 타입별 모델 적용 구조
- Merged contact 검출 알고리즘 구현 방법
- `contact_opc.py`: 패턴 타입 분류 → 타입별 모델 선택 → OPC 적용 파이프라인
- 슬롯 형상 contact의 장/단축 독립 보정 전략

## 태그
`Contact`, `OPC`, `PatternType`, `ModelBased`, `MergedContact`, `ContactHole`, `SPIE`, `2007`
