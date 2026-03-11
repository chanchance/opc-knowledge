# Curvilinear Mask Handling in OPC Flow

## 메타데이터
- **저자**: (JMM 저자 정보)
- **연도**: 2024
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology (JMM), Vol. 23, Issue 1, 011203
- **DOI/URL**: https://doi.org/10.1117/1.JMM.23.1.011203

## 핵심 요약
OPC 플로우에서 곡선형 마스크를 처리하는 방법론을 체계적으로 정리한다. 기존 맨해튼 OPC와 ILT(역 리소그래피) 방식은 서로 다른 알고리즘 기반이어서 경험이 쉽게 전환되지 않는다. 곡선형 OPC는 마스크 형상에 대한 MRC 제한을 완화하여 맨해튼 OPC 대비 패터닝 성능을 향상시킨다.

## 주요 기여
1. **곡선형 OPC 플로우 체계화**: ILT/ML ILT와 곡선형 OPC의 차이점 및 통합 방법
2. **맨해튼 vs 곡선형 비교**: OPC 플로우에서 두 방식의 장단점 분석
3. **MRC 제한 완화**: 곡선형 OPC가 맨해튼 OPC의 마스크 형상 제한을 극복하는 방법
4. **임계 패턴 분석**: 곡선형 OPC가 특히 유리한 패턴 유형 식별

## 알고리즘/수식
### 곡선형 OPC vs 맨해튼 OPC
```
맨해튼 OPC:
  마스크 엣지: 직각(90°) 세그먼트로 구성
  MRC 제약: 최소 세그먼트 길이, 최소 피처 크기 (맨해튼 기준)
  한계: 2D 코너/엔드 피처에서 MRC 제약으로 OPC 자유도 제한

곡선형 OPC:
  마스크 엣지: 연속 곡선 (Bezier, B-spline 등)
  MRC 제약: 곡률 반경, 최소 피처 크기 (곡선 기준)
  장점: 코너-투-코너(CTC), 엔드-투-엔드(ETE) 패턴에서 더 자유로운 최적화

ILT vs 곡선형 OPC:
  ILT: 픽셀 기반 전체 최적화 → 곡선형 후처리
  곡선형 OPC: 엣지 세그먼트 직접 곡선형 표현 → OPC 최적화
```

### 임계 패턴 성능 비교
```
CTC (Corner-To-Corner) 패턴:
  맨해튼 OPC: MRC 제한으로 최적화 제약
  곡선형 OPC: 곡률 자유도로 추가 OPC 보정 가능
  → EPE 개선, 공정 창 향상

ETE (End-To-End) 패턴:
  곡선형 OPC: 팁 형상 최적화로 tip-to-tip EPE 감소
```

## OPC 툴 SMO 구현 관련성
- 곡선형 OPC 플로우 설계: SKOPC 곡선형 OPC 모듈의 핵심 참조
- ILT-OPC 통합: ML ILT 출력 + 곡선형 OPC 파인튜닝 통합 플로우
- MRC 인식 OPC 최적화: 곡선형 MRC 제약을 OPC 최적화 내에 통합
- 임계 패턴 처리: CTC/ETE 패턴에 곡선형 OPC 우선 적용 전략

## 태그
`curvilinear`, `OPC`, `ILT`, `EUV`, `Manhattan`, `MRC`, `CTC`, `ETE`, `mask_shape`, `JMM`, `2024`
