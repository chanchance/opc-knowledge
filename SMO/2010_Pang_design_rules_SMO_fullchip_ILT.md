# Optimization from Design Rules, Source and Mask, to Full Chip with a Single Computational Lithography Framework: Level-Set-Methods-Based Inverse Lithography Technology (ILT)

## 메타데이터
- **저자**: Linyong Pang, Guangming Xiao, Vikram Tolani, Peter Hu, Danping Peng, Dongxue Chen, Tom Cecil, Lin He, Thuc Dam, Ki-Ho Baik, Bob Gleason
- **연도**: 2010
- **게재지/학회**: Proc. SPIE 7640, Optical Microlithography XXIII, 76400O
- **DOI/URL**: https://doi.org/10.1117/12.848145
- **인용수**: 다수

## 핵심 요약
설계 규칙부터 소스-마스크 최적화, 풀칩까지 단일 계산 리소그래피 프레임워크로 처리하는 레벨셋 기반 ILT 방법론을 제시한다. 설계 규칙 탐색, SMO, 풀칩 ILT OPC를 동일한 레벨셋 프레임워크 내에서 통합하여 처음부터 끝까지 일관된 최적화를 가능하게 한다. Luminescent Technologies.

## 주요 기여
- 설계 규칙 → SMO → 풀칩 ILT OPC 단일 프레임워크 통합
- 레벨셋 기반 ILT 방법론의 전체 흐름 통합 구현
- 설계 규칙 탐색과 SMO의 연계 최적화
- 풀칩 적용 가능한 계산 효율적 레벨셋 ILT 프레임워크

## 알고리즘/수식
**통합 최적화 프레임워크:**
```
1단계: 설계 규칙 탐색
   - 레벨셋 ILT로 다양한 설계 규칙 클립 최적화
   - 최적 CD, 피치, OPC 규칙 식별

2단계: SMO
   - 설계 규칙 클립 + 임계 패턴으로 소스-마스크 공동 최적화
   - 레벨셋 마스크 + 그래디언트 소스 최적화

3단계: 풀칩 ILT OPC
   - 최적화된 소스로 풀칩 레벨셋 ILT 마스크 합성
```

**레벨셋 ILT 비용함수 (통합):**
$$F_{unified}(\phi, \boldsymbol{\sigma}) = \sum_j EPE_j^2 + \lambda_{PW} F_{PW} + \lambda_{MEEF} F_{MEEF} + \lambda_{DRC} C_{DRC}(\phi)$$

**설계 규칙 최적화:**
$$\{CD^*, pitch^*, space^*\} = \arg\min_{CD, pitch, space} F_{unified}(\phi^*(CD, pitch, space), \boldsymbol{\sigma}^*)$$

**풀칩 ILT 마스크 합성 (최적 소스 고정):**
$$\phi_{fullchip}^*(x) = \arg\min_\phi \sum_j EPE_j^2(\phi(x), \boldsymbol{\sigma}^*)$$

## OPC 툴 SMO 구현 관련성
- SKOPC 레벨셋 ILT 기반 통합 최적화 프레임워크 구현 시 참고
- `skopc/smo/unified_ilt_smo.py`에 설계 규칙-SMO-풀칩 통합 프레임워크 구현
- `skopc/modeling/fullchip_ilt_opc.py`에 최적 소스 고정 풀칩 ILT OPC 구현
- Pang et al. 2009 풀칩 ILT SMO의 후속 확장 연구로 함께 참고

## 참고문헌 (핵심)
- Pang et al., \"Full chip ILT SMO level set,\" SPIE 2009
- Tolani et al., \"SMO level set methods,\" SPIE 2009
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011

## 태그
`SMO`, `ILT`, `SPIE`, `level-set`, `full-chip`, `design-rules`, `unified-framework`, `Luminescent-Technologies`, `inverse-lithography`, `OPC`, `mask-synthesis`, `computational-lithography`
