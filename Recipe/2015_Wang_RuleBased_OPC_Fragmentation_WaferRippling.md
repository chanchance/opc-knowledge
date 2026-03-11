# Optimization of Rule-Based OPC Fragmentation to Improve Wafer Image Rippling

## 메타데이터
- **저자**: Jingyu Wang, Alexander Wei, Piyush Verma, William Wilkinson
- **소속**: GLOBALFOUNDRIES Inc., Mentor Graphics Corp.
- **연도**: 2015
- **게재지**: Proc. SPIE 9661, 31st European Mask and Lithography Conference, 96610D
- **DOI/URL**: https://doi.org/10.1117/12.2194755

## 핵심 요약
Rule-based OPC의 fragmentation 규칙을 model-based resist 이미지를 기준으로 설계하여 웨이퍼 이미지 rippling 효과를 억제하는 방법론을 제시한다. 핵심 기여는 OPC 엔진 실행 전 coarse 시뮬레이션을 통해 rippling의 사인파 성분을 미리 추출하고, 이를 fragmentation 규칙 설계에 반영하는 feedback 루프다.

## 주요 기여
1. **Ripple pre-analysis**: OPC 실행 전 default 엔진 설정으로 coarse 시뮬레이션 → 특징적 geometry별 ripple 사인파 성분 추출
2. **Rule-based fragmentation 최적화**: resist 이미지 기반으로 fragment 위치·크기를 결정하는 versatile fragmentation 규칙 설계
3. **수렴성 향상**: target convergence 개선, 특히 불리한 치수 방향(unfavorable dimension)에서의 성능 개선
4. **Trial-and-error 최소화**: 기존 방식 대비 OPC recipe 구축 시 경험적 시행착오를 체계적 방법론으로 대체

## Recipe/Flow 상세
```
[Flow]
1. Default 설정으로 coarse OPC 시뮬레이션 실행
2. 특징 geometry별 ripple 사인파 성분 분석 및 추출
3. Ripple 특성(주기, 진폭)에 기반한 fragmentation 규칙 설계
   - Fragment 위치: resist 이미지 변화가 큰 위치 우선
   - Fragment 크기: ripple 주기의 절반 이하로 설정
4. 최적화된 fragmentation 규칙으로 model-based OPC 실행
5. ORC(Optical Rule Check)로 ripple 억제 결과 검증
```

### 핵심 파라미터
- **Fragment 배치 기준**: model-based resist image의 gradient 분포
- **Ripple 억제 기준**: 사인파 진폭 < specification threshold
- **적용 대상**: 모든 치수 방향 (특히 unfavorable dimension)

## OPC 툴 구현 관련성
- `skopc/modeling/rule_opc.py`: rule-based OPC에서 fragmentation 단계 개선에 직접 적용 가능
- `skopc/modeling/model_opc.py`: coarse simulation 기반 ripple 사전 분석 루프 추가 고려
- **Fragmentation 전략**: SKOPC의 edge segment fragmentation 알고리즘에서 resist 이미지 기반 adaptive fragmentation 구현 참고
- **Recipe 파라미터**: `fragment_min_length`, `fragment_max_length` 설정 시 ripple 주기 분석 결과 활용

## 태그
`Recipe`, `SPIE`, `Rule-Based OPC`, `Fragmentation`, `Edge Segment`, `Wafer Rippling`, `OPC Recipe`, `Convergence`
