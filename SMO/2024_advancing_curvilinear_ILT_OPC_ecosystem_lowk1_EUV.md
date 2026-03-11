# Advancing the Curvilinear ILT and OPC Ecosystem for Low-k1 DUV and EUV Lithography

## 메타데이터
- **저자**: (SPIE 12954 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 1295413 (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3014637

## 핵심 요약
저-k1 DUV 및 EUV 리소그래피를 위한 곡선형 ILT 및 OPC 생태계의 발전을 다룬다. 다양한 레이어와 리소그래피 응용에서 곡선형 마스크의 품질 요구사항과 비용 제약을 다루며, ILT와 통합 곡선형 기반 ILT/OPC의 발전 사항을 공유한다.

## 주요 기여
1. **곡선형 ILT/OPC 생태계 진보**: DUV/EUV 다중 레이어 응용을 위한 통합 곡선형 플로우
2. **레이어별 품질-비용 균형**: 레이어 유형에 따른 곡선형 마스크 수준 차별화
3. **통합 ILT+OPC**: ILT와 곡선형 OPC의 통합된 단일 플로우
4. **저-k1 DUV 적용**: EUV 외에 저-k1 ArFi DUV에도 곡선형 마스크 확대 적용

## 알고리즘/수식
### 곡선형 ILT/OPC 통합 플로우
```
레이어 유형별 전략:
  Critical 레이어 (EUV 로직 메탈/비아):
    Full ILT → 최적 곡선형 마스크
    런타임: 길지만 최고 품질

  Semi-critical 레이어:
    하이브리드 ILT + 곡선형 OPC
    런타임: 중간 수준, 충분한 품질

  Less-critical 레이어 (ArFi DUV):
    곡선형 OPC만 (ILT 없음)
    런타임: 빠름, 기본적 품질 향상

통합 곡선형 ILT/OPC:
  ILT 단계: 전역 최적화 → 초기 곡선형 마스크
  OPC 단계: 로컬 보정 → 최종 곡선형 마스크 세밀 조정
  → 단일 플로우에서 ILT와 OPC의 장점 결합
```

### 품질-비용 트레이드오프
```
곡선형 마스크 비용 요소:
  런타임: ILT > 하이브리드 > 곡선형 OPC
  데이터 볼륨: ILT > 하이브리드 > 곡선형 OPC
  마스크 제조: MRC 복잡도에 따라 다름

품질 메트릭:
  EPE, DOF, EL, NILS
  → 레이어 요구사항에 맞는 최소 품질 달성
```

## OPC 툴 SMO 구현 관련성
- 레이어별 곡선형 전략: SKOPC에서 레이어 유형별 ILT/OPC 수준 자동 선택
- 통합 ILT+OPC: ML ILT + 곡선형 OPC를 단일 플로우로 통합 설계
- DUV/EUV 통합 플로우: ArFi와 EUV를 동일 플랫폼에서 처리하는 곡선형 OPC
- SMO 연계: 곡선형 마스크에 최적화된 소스 형상 도출

## 태그
`ILT`, `curvilinear`, `OPC`, `EUV`, `DUV`, `low_k1`, `ecosystem`, `hybrid_ILT`, `DTCO`, `SPIE`, `2024`
