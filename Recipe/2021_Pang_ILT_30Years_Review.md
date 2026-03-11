# Inverse Lithography Technology: 30 Years from Concept to Practical, Full-Chip Reality

## 메타데이터
- **저자**: Linyong Pang
- **연도**: 2021
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 20, Issue 3, 030901
- **DOI/URL**: https://doi.org/10.1117/1.JMM.20.3.030901
- **인용수**: ~80

## 핵심 요약
ILT(Inverse Lithography Technology)의 30년 역사를 개념 제안(1991년경)부터 2021년 실용적 풀칩 양산까지 체계적으로 정리한 종합 리뷰 논문이다. ILT의 수학적 원리, 풀칩 상용화를 가로막았던 기술 장벽(계산 비용, 마스크 제조 가능성), 세 가지 주요 상용화 접근법(레벨셋 방법, 픽셀화 ILT, GPU 가속)의 발전 과정, 그리고 커브형(curvilinear) ILT와 VSB 마스크 기록기의 통합을 망라한다.

## 주요 기여
1. ILT 30년 발전사의 포괄적 체계적 정리
2. 풀칩 ILT 상용화 경로: 레벨셋(Luminescent), 픽셀화(Intel), GPU 가속(Gauda/D2S)
3. 커브형 ILT와 VSB/MBMW 마스크 기록기 통합 기술 현황
4. EUV 및 High-NA EUV를 위한 ILT 미래 방향

## Recipe/Process Flow 상세

### ILT의 수학적 원리
```
Forward 문제 (표준 OPC):
  주어진: 마스크 M
  계산: 웨이퍼 이미지 I(M)
  목표: I(M) ≈ I_target (비선형 최적화로 M 수정)

Inverse 문제 (ILT):
  주어진: 목표 이미지 I_target
  계산: 최적 마스크 M_opt
  수식: M_opt = argmin_{M} ||I(M) - I_target||² + λ R(M)
    R(M): 마스크 정규화 (마스크 복잡도 제어)
    λ: 정규화 강도

ILT와 MB-OPC 차이:
  MB-OPC: 기존 Manhattan 마스크 형상을 이동/조정
  ILT: 제약 없이 최적 마스크 형상을 탐색 (픽셀 단위)
  결과: ILT가 더 넓은 공정 윈도우 달성 가능
       (특히 2D 패턴, 라인-엔드, 코너에서)
```

### 30년 역사와 기술 장벽
```
1991-2000 (개념 제안 및 초기 연구):
  - 역 리소그래피 수학적 프레임워크 제안
  - 단일 패턴/작은 클립에서 개념 실증
  - 주요 장벽: 계산 비용 너무 높음 (풀칩 불가)

2000-2008 (알고리즘 발전):
  - 그래디언트 기반 최적화 알고리즘 개선
  - CTM(Continuous Transmission Mask) 도입
  - SRAF 생성에 ILT 선택적 적용 시작
  - 주요 장벽: 마스크 제조 가능성 (MRC 위반 형상)

2008-2015 (풀칩 접근):
  - Luminescent: 레벨셋 방법 기반 풀칩 ILT
  - Intel: 픽셀화 ILT 개발, 특정 레이어 적용
  - Gauda (D2S): GPU 가속으로 속도 문제 해결
  - Manhattanization 알고리즘: ILT 결과를 직교 형상으로 변환
  주요 장벽: 여전히 높은 런타임, 일부 레이어만 적용

2015-2021 (양산 적용):
  - 커브형 ILT: Manhattanization 포기, 직접 커브 마스크
  - MBMW(Multi-Beam Mask Writer): 커브형 마스크 제작 가능
  - GPU 클러스터: 풀칩 런타임 수용 가능 수준
  - 메모리/로직 선진 노드 전반에 ILT 적용 확대
```

### 세 가지 상용화 접근법
```
1. 레벨셋 방법 (Luminescent, 후 ASML 인수):
   마스크 경계를 레벨셋 함수로 기술
   장점: 위상 변화 자연 처리, 수학적 우아함
   적용: 풀칩 SMO까지 확장 (SPIE 7520, 2009)

2. 픽셀화 ILT (Intel):
   마스크를 픽셀 격자로 표현, 각 픽셀 0 또는 1
   장점: 단순한 파라미터화, 병렬화 용이
   제약: 픽셀 크기로 해상도 제한

3. GPU 가속 ILT (Gauda, 현 D2S):
   기존 ILT 알고리즘을 GPU에서 고속 실행
   장점: 기존 알고리즘 + 대규모 병렬화
   결과: 수일 → 수시간으로 런타임 단축
   cuLitho와 결합하여 수십 배 추가 가속
```

### 커브형 ILT와 VSB/MBMW 통합
```
기존 Manhattan ILT:
  ILT 최적 해 (연속 형상) → Manhattanization → VSB 마스크 기록
  문제: Manhattanization 단계에서 OPC 성능 손실

커브형 ILT:
  ILT 최적 해 (커브형) → MBMW로 직접 기록
  MBMW: 픽셀 기반 마스크 기록기 (커브형 지원)
  성능: Manhattan ILT 대비 공정 윈도우 추가 향상
  2021 현재: 일부 선진 노드에서 커브형 ILT 양산 적용

VSB 마스크 기록기 호환:
  커브형 형상을 VSB용 단순화 방법 연구 중
  Piecewise linear 근사 + VSB 기록 최적화
```

## OPC 툴 구현 관련성
- **SKOPC openilt_adapter**: `skopc/modeling/openilt_adapter.py` OpenILT 기반 ILT 흐름 참조
- **ILT 역사적 맥락**: 레벨셋 vs. 픽셀화 vs. GPU 가속 세 접근법 비교로 SKOPC ILT 전략 수립
- **커브형 ILT 연동**: ILT 결과를 Manhattan 변환 없이 커브형 마스크로 직접 출력하는 파이프라인
- **GPU 가속**: TorchLitho 기반 GPU ILT를 cuLitho 패턴으로 확장 참조

## 참고문헌
- J. Micro/Nanopatterning, Materials, and Metrology 20(3), 030901 (2021)
- 저자 소속: ASML (Linyong Pang, 전 Luminescent Technologies 창업자)
- 관련: SMO at full chip scale using ILT level set methods (SPIE 7520, 2009)
- 관련: Advancing the curvilinear ILT and OPC ecosystem (SPIE 12954, 2024)
- 관련: GPU-Accelerated ILT towards high quality curvy mask generation (arXiv, 2024)

## 태그
`Recipe`, `SPIE`, `JM3`, `ILT`, `InverseLithography`, `Review`, `LevelSet`, `PixelizedILT`, `GPU`, `Curvilinear`, `MBMW`, `30Years`, `2021`
