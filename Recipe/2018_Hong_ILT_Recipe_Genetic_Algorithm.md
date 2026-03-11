# Inverse Lithography Recipe Optimization Using Genetic Algorithm

## 메타데이터
- **저자**: Le Hong, Fan Jiang, Alexander Tritchkov, James Word, Dan Zhang
- **연도**: 2018
- **게재지**: Proc. SPIE 10587, Optical Microlithography XXXI, 105871H
- **DOI/URL**: https://doi.org/10.1117/12.2297141
- **인용수**: ~20

## 핵심 요약
역리소그래피 기술(ILT)의 레시피 최적화에 유전 알고리즘(GA)을 적용한 연구. 세 가지 실제 테스트 케이스로 검증하며, 합리적인 TAT(Turn-Around Time)와 향상된 ILT 솔루션을 달성함을 입증한다. OPC와 달리 ILT는 픽셀 기반 최적화로 더 넓은 파라미터 공간을 다루어야 하며, GA가 이 탐색에 효과적임을 보인다.

## 주요 기여
1. ILT 레시피 파라미터 최적화를 위한 수정된 GA 엔진
2. 세 가지 실제 산업 테스트 케이스에서 방법론 검증
3. ILT 솔루션 품질(EPE, 마스크 복잡도) 개선 정량화
4. 합리적 TAT를 유지하면서 ILT 레시피 자동 최적화

## Recipe/Process Flow 상세

### ILT 레시피 파라미터 공간
```
픽셀화 파라미터:
- 픽셀 크기 (pixel size): 마스크 해상도 결정
- 초기화 전략: 이진/연속 마스크 초기값

정규화 파라미터:
- 마스크 복잡도 페널티 계수 (α)
- EPE 가중치 함수
- Edge/Area 정규화 강도

수렴 파라미터:
- 최대 최적화 이터레이션
- 수렴 임계값 (EPE 목표)
- Step size for gradient update

출력 포맷:
- Manhattan 근사화 파라미터
- 마스크 이진화 임계값
```

### GA 기반 ILT 레시피 최적화 흐름
```
1. ILT 파라미터 공간 정의
   - 각 파라미터의 탐색 범위 설정
   - 연속/이산 혼합 변수 처리

2. 초기 집단 생성
   - 기존 경험 기반 레시피를 시드로 사용
   - 주변 무작위 변동으로 다양성 확보

3. 적합도 평가 (각 개체)
   - ILT 최적화 실행
   - EPE RMS 측정
   - 마스크 복잡도(MRC 위반, 곡률) 측정
   - 복합 목적함수: F = w1·EPE + w2·MaskComplexity + w3·Runtime

4. GA 연산 (선택/교배/돌연변이)
   - 비례 선택 또는 엘리트 보존
   - BLX-α 교배 (연속 파라미터)
   - 가우시안 돌연변이

5. 수렴 및 최적 레시피 추출
   - Pareto front 분석 (EPE vs. MaskComplexity)
   - 최적 레시피 선택 및 검증
```

### 3개 테스트 케이스 결과
- 케이스 1: 표준 1D 라인-스페이스 패턴
- 케이스 2: 2D contact/via 레이어
- 케이스 3: 혼합 1D/2D 복잡 레이아웃
- 공통 결과: 합리적 TAT 내에서 EPE 개선 및 마스크 복잡도 제어

## OPC 툴 구현 관련성
- **SKOPC ILT/SMO**: `skopc/smo/` 내 역리소그래피 최적화의 레시피 파라미터 자동 튜닝에 직접 적용
- **OpenILT 통합**: `skopc/modeling/openilt_adapter.py`의 ILT 파라미터 최적화 루프로 활용
- **다목적 최적화**: EPE와 마스크 복잡도의 Pareto front는 NSGA-II 기반 PWO와 유사
- **산업 검증**: Mentor Graphics 기반 실제 테스트 케이스로 산업 적용성 검증됨

## 참고문헌
- Proc. SPIE 10587, Optical Microlithography XXXI (2018)
- 관련: OPC recipe optimization using genetic algorithm (SPIE 9780, 2016)
- 관련: Inverse lithography OPC correction with multiple patterning (SPIE 10587, 2018)

## 태그
`Recipe`, `SPIE`, `ILT`, `GeneticAlgorithm`, `InverseLithography`, `RecipeOptimization`, `MaskComplexity`, `EPE`, `MentorGraphics`
