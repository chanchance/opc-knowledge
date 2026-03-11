# Model-Based SRAF Solutions for Advanced Technology Nodes

## 메타데이터
- **저자**: Srividya Jayaram, Pat LaCour, James Word, Alexander Tritchkov
- **연도**: 2013
- **게재지**: Proc. SPIE 8886, 29th European Mask and Lithography Conference, 88860P
- **DOI/URL**: https://doi.org/10.1117/12.2031789
- **인용수**: ~35

## 핵심 요약
전체 칩에 대한 다양한 설계 구성에서 Rule-based SRAF 대비 Model-based SRAF 사용의 트레이드오프와 이점을 조사한다. 비용, 시간, 공정 윈도우, 성능에 대한 영향을 분석하며, 첨단 기술 노드(advanced technology nodes)에서 MB-SRAF가 언제, 어떻게 필요한지에 대한 실용적 가이드라인을 제공한다.

## 주요 기여
1. Rule-based vs. Model-based SRAF의 전체 칩 수준 트레이드오프 체계적 분석
2. 비용·시간·공정 윈도우·성능 4개 차원에서의 정량적 비교
3. 첨단 노드에서 MB-SRAF 필요성 판단 기준 및 실용적 적용 가이드
4. MB-SRAF 삽입 흐름의 산업 구현 사례

## Recipe/Process Flow 상세

### Rule-Based SRAF vs. Model-Based SRAF 비교
```
Rule-Based SRAF (RB-SRAF):
장점:
  - 빠른 실행 속도 (기하학적 연산)
  - 간단한 구현
  - 예측 가능한 결과
단점:
  - 복잡한 2D 패턴에서 최적성 부족
  - 규칙 개발에 상당한 엔지니어링 시간
  - 패턴 유형 변화에 적응 어려움

Model-Based SRAF (MB-SRAF):
장점:
  - 더 정확한 SRAF 위치/크기 (광학 모델 기반)
  - 복잡한 2D 패턴에서 우수한 공정 윈도우
  - 규칙 개발 없이 자동화
단점:
  - 높은 계산 비용 (리소그래피 시뮬레이션 필요)
  - 긴 런타임
  - 모델 캘리브레이션 필요
```

### Model-Based SRAF 삽입 흐름
```
1. 광학/레지스트 모델 준비
   - 캘리브레이션된 리소그래피 모델 확보
   - 광원 조건, NA, 레지스트 파라미터 설정

2. 전체 칩 레이아웃 처리
   - 레이아웃을 타일(tile)로 분할
   - 각 타일 독립적 병렬 처리

3. SRAF 후보 위치 탐색 (각 타일)
   a) 현재 마스크 레이아웃에서 SRAF 후보 영역 정의
      - 주 패턴으로부터의 최소/최대 이격 거리
      - 설계 규칙 기반 필터링
   b) 후보 SRAF 위치에서 리소그래피 시뮬레이션
      - SRAF 없는 기준 이미지 vs. SRAF 추가 이미지
   c) NILS (Normalized Image Log-Slope) 또는 공정 윈도우 계산
      - NILS 향상이 가장 큰 위치 선택

4. SRAF 크기 최적화
   - 최적 폭 탐색 (binary search 또는 gradient)
   - SRAF 인쇄 안전 확인 (인쇄 임계값 미달 보장)

5. DRC/MRC 후처리
   - 설계 규칙 위반 SRAF 제거
   - SRAF 간 충돌 해결
```

### 첨단 노드별 가이드라인
```
28nm 노드:
  - Dense gate 레이어: MB-SRAF 권장
  - Metal 레이어: RB-SRAF로 충분
  - Contact/Via: MB-SRAF 필요 (2D 구조)

20nm 이하:
  - 대부분 레이어에서 MB-SRAF 필요
  - RB-SRAF는 초기 기준으로만 사용
  - 핫스팟은 MB-SRAF로 보수

트레이드오프 판단:
  공정 윈도우 개선 > 런타임 비용 → MB-SRAF 사용
  패턴이 단순 1D → RB-SRAF 충분
  설계 콘텐츠 다양성 높음 → MB-SRAF 필수
```

## OPC 툴 구현 관련성
- **SKOPC SRAF 전략 선택**: `skopc/modeling/sraf_generator.py`에 RB-SRAF/MB-SRAF 자동 선택 로직 구현 시 본 논문의 판단 기준 활용
- **레시피 파라미터**: SRAF 방법(rule-based/model-based)을 SKOPC YAML 레시피에서 레이어별 설정 가능
- **전체 칩 타일 처리**: 대용량 레이아웃 MB-SRAF를 위한 타일 분할 병렬 처리 아키텍처
- **Mentor Graphics**: Calibre WORKbench MB-SRAF의 이론적 기반

## 참고문헌
- Proc. SPIE 8886, 29th European Mask and Lithography Conference (2013)
- 저자 소속: Mentor Graphics Corp.
- 관련: SRAF rule extraction and insertion based on ILT (SPIE 10961, 2019)
- 관련: Model-based placement and optimization of SRAFs (SPIE 6154, 2006)

## 태그
`Recipe`, `SPIE`, `SRAF`, `ModelBasedSRAF`, `RuleBasedSRAF`, `AdvancedNode`, `Tradeoff`, `ProcessWindow`, `FullChip`, `MentorGraphics`
