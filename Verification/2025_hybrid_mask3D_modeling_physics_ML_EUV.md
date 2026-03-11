# Hybrid Mask 3D Modeling Driven by Both Physical Solution and Machine Learning

## 메타데이터
- **저자**: Rongzhang Chen 등
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV (SPIE Advanced Lithography + Patterning 2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051827

## 핵심 요약
EUV 리소그래피 확산에 따라 마스크 3D(M3D) 모델링의 정확도와 런타임 요구가 동시에 높아지고 있다. 물리 기반 모델링은 안정성은 우수하지만 복잡하고 조밀한 패턴에서 런타임 페널티와 정확도 저하가 발생한다. 머신러닝 기반 방법은 높은 정확도와 빠른 계산이 가능하지만 오버피팅 위험이 있다. 이 논문은 두 방식의 장점을 결합한 하이브리드 M3D 모델을 제안한다.

## 주요 기여
1. **하이브리드 M3D 아키텍처**: 물리 기반 솔루션과 머신러닝을 결합하여 안정성과 정확도를 동시에 확보
2. **0.55NA 및 0.33NA EUV 적용**: 두 가지 EUV NA 조건에서 모두 정확도 향상 및 런타임 단축 결과 제시
3. **오버피팅 방지**: 물리 제약을 통해 ML 모델의 일반화 성능 향상
4. **풀칩 적용 가능성**: 실용적인 런타임 내에서 풀칩 M3D 효과 시뮬레이션 가능

## 검증 방법론
- 0.55NA EUV 및 0.33NA EUV 사용 사례에서 모델 정확도 및 런타임 평가
- RCWA 등 rigorous EM 시뮬레이션 결과를 기준으로 하이브리드 모델 결과 검증
- 기존 순수 물리 모델 및 순수 ML 모델 대비 정량적 비교

## OPC 툴 구현 관련성
- EUV OPC 엔진에서 M3D 효과 처리 시 하이브리드 접근 방식 채택 고려
- `skopc/modeling/` 내 LithoEngine에서 마스크 3D 효과 모델 컴포넌트로 통합 가능
- 물리 제약 기반 ML 아키텍처는 GNN-OPC 등 신경망 OPC 모델에도 응용 가능
- 0.55NA EUV 대응 모델링 확장 시 핵심 참고 자료

## 태그
`Verification`, `SPIE`, `EUV`, `Mask3D`, `Machine_Learning`, `Physics_Informed`, `High_NA`, `Modeling`, `2025`
