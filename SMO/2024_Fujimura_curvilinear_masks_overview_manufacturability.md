# Curvilinear Masks Overview: Manufacturable Mask Shapes Are More Reliably Manufacturable

## 메타데이터
- **저자**: Aki Fujimura, Yohan Choi, Abhishek Shendre
- **연도**: 2024
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology (JMM), Vol. 23, Issue 4, 041502 (24 August 2024)
- **DOI/URL**: https://doi.org/10.1117/1.JMM.23.4.041502

## 핵심 요약
곡선형 마스크의 기술적 배경, 동기, 실용적 응용을 종합적으로 개요한다. 다중 빔 및 가변 형상 빔 마스크 라이터로 작성된 곡선형 ILT 마스크가 더 신뢰성 있게 제조 가능함을 논증한다. 곡선형 타겟을 허용하면 설계를 더 제조 가능하고 웨이퍼 제조 변동에 탄력적으로 만들면서, 전력 절감, 클럭 속도 향상, 설계 소형화를 동시에 달성할 수 있음을 제시한다.

## 주요 기여
1. **곡선형 마스크 종합 개요**: 기술 배경부터 실제 응용까지 체계적 정리
2. **제조 가능성 우수성 논증**: 곡선형 형상이 맨해튼보다 오히려 더 안정적으로 제조 가능
3. **MBMW/VSB 라이터 지원**: 두 유형의 마스크 라이터에서 곡선형 ILT 마스크 작성
4. **설계-마스크-제조 공동 이점**: 소비 전력, 성능, 면적의 동시 개선

## 알고리즘/수식
### 곡선형 마스크 제조 가능성 분석
```
직관적 오해: 곡선형 형상 = 제조 어려움
실제: 날카로운 맨해튼 코너 > 완만한 곡선 (제조 관점)

맨해튼 OPC 제약:
  - 날카로운 90° 코너: e-beam 근접 효과 강함
  - MRC 위반 위험: 최소 간격/피처 크기 제약 많음
  - 코너 라운딩 불가피 → 의도치 않은 곡선화

곡선형 ILT 마스크:
  - 연속 곡률: e-beam 근접 효과 분산
  - MRC 제약 완화: 곡률 반경 기반 설계 자유도 증가
  - 의도적 곡선화로 예측 가능한 제조 오차

제조 변동 내성:
  σ_CD_curvilinear < σ_CD_manhattan (동일 피처)
  → 웨이퍼 CD 균일성 향상
```

### 성능 향상 분석
```
PPA (Power, Performance, Area) 이점:
  곡선형 OPC: 더 정밀한 엣지 배치
  → EPE 감소 → 게이트 길이 균일성 향상 → 성능 향상
  → 설계 밀도 증가 → 면적 감소
  → 누설 전류 감소 → 소비 전력 감소
```

## OPC 툴 SMO 구현 관련성
- 곡선형 OPC 설계 근거: SKOPC 곡선형 OPC 채택의 기술적/비즈니스 근거
- 제조 가능성 설계: MRC 제약을 최소화하면서 곡선형 이점 극대화
- MBMW/VSB 지원: 두 마스크 라이터 타입에 맞는 곡선형 OPC 출력 형식
- SMO + 곡선형 마스크: 소스 최적화와 곡선형 마스크의 시너지 효과

## 태그
`curvilinear`, `ILT`, `EUV`, `manufacturability`, `MBMW`, `VSB`, `OPC`, `design`, `PPA`, `JMM`, `2024`
