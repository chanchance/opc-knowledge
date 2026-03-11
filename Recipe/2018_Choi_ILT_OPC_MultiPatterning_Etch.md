# Inverse Lithography OPC Correction with Multiple Patterning and Etch Awareness

## 메타데이터
- **저자**: Heon Choi, Ayman Hamouda
- **소속**: (SPIE Optical Microlithography XXXI 게재)
- **연도**: 2018
- **게재지**: Proc. SPIE 10587, Optical Microlithography XXXI, 105870O
- **DOI/URL**: https://doi.org/10.1117/12.2297368

## 핵심 요약
ILT(Inverse Lithography Technique)를 다중 패터닝(multiple patterning)과 식각(etch) 효과를 동시에 고려하는 방향으로 확장한다. 기존 ILT는 단일 리소그래피 공정만 고려하지만, 이 연구는 LELE 등 다중 패터닝 시나리오에서의 마스크 간 상호작용과 리소그래피 후 etch proximity 효과를 ILT 최적화 루프에 통합한다.

## 주요 기여
1. **Multi-patterning aware ILT**: LELE 분해된 두 마스크의 리소그래피 상호작용을 ILT 최적화에 통합
2. **Etch awareness**: 리소그래피 후 식각 공정의 proximity 효과를 ILT 목적함수에 포함
3. **통합 최적화**: 리소그래피 + etch를 연속 공정으로 모델링하여 최종 웨이퍼 패턴 목표에 직접 최적화
4. **실용적 플로우**: 산업적 다중 패터닝 플로우에 ILT 적용 가능성 검증
5. **공정 마진 개선**: etch 효과 무시 시 발생하는 체계적 오차 제거

## Recipe/Flow 상세
```
[Multi-Patterning + Etch-Aware ILT Flow]
1. 레이아웃 분해 (Multiple Patterning Decomposition):
   - 원본 레이아웃 → Mask A + Mask B (conflict-free LELE 분리)
2. Etch 모델 구축:
   - 리소그래피 후 식각 공정의 proximity 효과 모델링
   - Etch bias = f(pattern density, geometry, process conditions)
3. ILT 최적화 루프:
   a. Mask A, B 픽셀/형상 초기화
   b. 리소그래피 시뮬레이션 (Mask A + Mask B 상호작용 포함)
   c. Etch 시뮬레이션 적용 → 최종 웨이퍼 패턴 예측
   d. 최종 패턴 vs. 타겟 EPE 계산
   e. Gradient 역전파로 Mask A, B 동시 업데이트
   f. 수렴 판정
4. MRC 검사 및 최종 마스크 출력
5. Multi-patterning ORC (각 mask 개별 + 전체 overlay 포함)
```

### 핵심 파라미터
- **다중 패터닝 방식**: LELE (Litho-Etch-Litho-Etch) 주 대상
- **Etch 모델**: pattern density 및 geometry 기반 proximity etch bias
- **최적화 목표**: 최종 웨이퍼 패턴(리소+etch 후) vs. 타겟 EPE 최소화
- **ILT 방법**: pixel-based 또는 level-set 기반

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: multi-patterning + etch 통합 OPC/ILT 플로우 설계 참고
- **Etch 모델 통합**: SKOPC의 리소그래피 시뮬레이션 뒤에 etch 공정 시뮬레이션 추가하는 파이프라인 구축 참고
- `skopc/pwo/`: 다중 패터닝 공정 윈도우 최적화 시 etch 효과 포함하는 확장 방향
- `recipes/example_arfimm.yaml`: multi-patterning recipe에 `etch_aware: true`, `multi_patterning: LELE` 파라미터 추가 참고

## 태그
`Recipe`, `SPIE`, `ILT`, `Multiple Patterning`, `LELE`, `Etch Awareness`, `EPC`, `OPC`, `Multi-Patterning OPC`, `2018`
