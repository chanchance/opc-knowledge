# Model-Based CMP Proximity Correction for Mitigating Systematic Process Variations

## 메타데이터
- **저자**: Yongchan Ban, Yongseok Kang, Woohyun Paik
- **연도**: 2015 (IEEE ISOCC 2015, published 2016)
- **게재지**: IEEE International SoC Design Conference (ISOCC) 2015
- **DOI/URL**: https://ieeexplore.ieee.org/document/7401685/

## 핵심 요약
sub-28nm SoC 설계에서 CMP(Chemical-Mechanical Polishing) 공정에 의한 체계적 공정 변동(systematic process variation)을 완화하기 위한 모델 기반 CMP proximity 보정 방법을 제안한다. 기존 metal fill 방식에 추가적인 마스크 합성 단계로 편입될 수 있는 접근법으로, 배선 폭 변동에 의한 RC 특성 변화를 최소화한다.

## 주요 기여
1. **CMP-aware 마스크 보정**: OPC와 유사한 방식으로 CMP 기인 CD 변동을 사전 보정
2. **Metal fill 보완**: 기존 dummy fill 방법 대비 패턴 의존적 CMP 변동까지 보정
3. **Sub-28nm 적용**: 28nm 이하 노드에서 BEOL 배선 CMP 변동의 심각성 및 보정 필요성 입증
4. **마스크 합성 통합**: 기존 OPC 플로우 후단에 CMP 보정 단계 삽입 가능한 구조

## Recipe/Flow 상세
- **CMP proximity 보정 플로우**:
  1. **CMP 모델 캘리브레이션**: 패턴 밀도, 피처 크기, 주변 환경 대비 CMP 연마율 모델 구축
  2. **CMP 시뮬레이션**: 레이아웃에서 CMP 후 예상 토폴로지/CD 계산
  3. **보정 바이어스 계산**: CMP 기인 CD 변동을 상쇄하는 마스크 바이어스 산출
  4. **보정 적용**: OPC 후 또는 OPC와 동시에 CMP 보정 바이어스 적용
  5. **검증**: 보정 전/후 CD 변동 및 RC 특성 비교
- **대상 레이어**: BEOL 금속 배선 레이어 (M1, M2 등)
- **모델 파라미터**: 패턴 밀도, 피처 종횡비, 주변 구조 밀도
- **평가 지표**: 배선 CD 균일도, RC 변동량, 타이밍 closure 여유

## OPC 툴 구현 관련성
- OPC 플로우에 CMP 보정 단계 추가 시 모델 구조 참고
- 패턴 밀도 기반 보정 바이어스 테이블 구현 방법
- Metal fill과 CMP 보정의 상호작용 처리 로직
- `cmp_proximity_correction.py`: density map 생성 → CMP 모델 → 바이어스 보정 파이프라인

## 태그
`CMP`, `ProximityCorrection`, `ModelBased`, `BEOL`, `MetalLayer`, `SystematicVariation`, `IEEE`, `2015`
