# High Accuracy OPC Modeling for New EUV Low-K1 Mask Technology Options

## 메타데이터
- **저자**: (SPIE Photomask Technology / EUV Lithography 2023)
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, SPIE Photomask Technology + EUV Lithography 2023, 124950P
- **DOI/URL**: https://doi.org/10.1117/12.2658720
- **인용수**: ~15

## 핵심 요약
차세대 EUV 리소그래피를 위한 저굴절률(low-n) 및 고소광계수(high-k) 대안 마스크 흡수체 재료 도입 시 OPC 모델링 과제와 해결 방법을 다룬다. 기존 TaN 기반 흡수체에서 low-n(n≈1 근접) 흡수체로의 전환은 마스크 3D 효과를 감소시키지만 새로운 OPC 모델 과제를 유발한다. 다양한 n, k 값의 흡수체 재료에 대해 EUV OPC 컴팩트 모델의 정확도를 유지하는 방법을 제시한다.

## 주요 기여
1. Low-n/high-k 대안 EUV 마스크 흡수체에 대한 OPC 모델링 과제 분석
2. 다양한 흡수체 재료 (n, k 값 변화)에 대한 OPC 모델 정확도 검증
3. 저n 흡수체의 M3D 효과 감소 효과와 OPC 모델링 영향 정량화
4. EUV 저K1 마스크 기술 옵션에 맞춤 OPC 컴팩트 모델 방법 제시

## Recipe/Process Flow 상세

### EUV 마스크 흡수체 재료 배경
```
현재 표준 EUV 마스크 흡수체:
  재료: TaN (탄탈륨 질화물)
  두께: ~60-70nm
  n (굴절률): n > 1 (EUV 파장 13.5nm에서)
  k (소광계수): 중간

TaN 흡수체 한계:
  두꺼운 흡수체 → 강한 마스크 3D (M3D) 효과:
    - 쉐도잉: 경사 입사광으로 인한 비텔레센트리시티
    - 포커스 시프트: 최적 포커스 패턴 의존
    - 대비 저하: M3D로 인한 이미지 콘트라스트 감소
  → OPC 모델 복잡성 증가
```

### 대안 흡수체 재료 분류
```
Low-n 흡수체 (n ≈ 1):
  원리: EUV 파장에서 n≈1 → 굴절 없음 → M3D 감소
  재료 후보:
    - Ru (루테늄): n≈0.89, k 중간
    - Mo 화합물: n≈0.92-0.95
    - 고엔트로피 합금: 다성분 최적화
  장점: M3D 대폭 감소, 이미지 콘트라스트 향상
  단점: 흡수 낮음 → 더 두꺼운 막 필요 or 투과율 증가

High-k 흡수체:
  원리: k 증가 → 얇은 두께에도 높은 흡수 달성
  재료 후보:
    - NiN (니켈 질화물): 높은 k
    - Ta-B-N 합금: 최적화된 n, k
  장점: 얇은 흡수체 → M3D 감소
  단점: 이미지 콘트라스트 vs 흡수 트레이드오프

Low-n + High-k 결합:
  최적 재료: 낮은 n + 높은 k 동시 달성
  목표: 얇은 두께 + 낮은 M3D + 높은 콘트라스트
  IBM/imec 탐색: 다양한 조성 매개변수 탐색
```

### OPC 모델링 과제
```
기존 OPC 컴팩트 모델 (TaN 기반):
  M3D 항 파라미터: TaN 흡수체에 맞게 캘리브레이션
  비텔레센트리시티 보정: TaN-특정 계수

Low-n 흡수체 OPC 과제:
  M3D 효과 변화:
    - 비텔레센트리시티: n≈1 → 굴절 없음 → 쉐도잉 다름
    - 포커스 시프트: 두께/n 변화 → 다른 포커스 의존성
    - 콘트라스트 변화: 더 높은 이미지 콘트라스트 → 다른 OPC 필요
  컴팩트 모델 재캘리브레이션:
    - M3D 항: 새 흡수체에 맞게 업데이트
    - NILS (Normalized Image Log Slope): 변화
    - CD-비선형성: 흡수체 의존 비선형 CD 응답

High-k 흡수체 OPC 과제:
  얇은 흡수체 M3D: 다른 쉐도잉 패턴
  패턴 의존 흡수: k 변화 → CD 변동
  마스크 제조 편차: 두께 균일성 → OPC 오차
```

### OPC 모델 정확도 평가
```
시뮬레이션 방법:
  엄밀 전자기 시뮬 (FDTD/RCWA):
    - 다양한 n, k, 두께 조합
    - 완전한 M3D 효과 포함 기준값
  컴팩트 모델:
    - TCC + M3D 보정항
    - 새 흡수체 재료에 재캘리브레이션

평가 메트릭:
  EPE RMS: 다양한 흡수체 조합 비교
  Nils 예측 오차: 이미지 콘트라스트 예측 정확도
  포커스 민감도: M3D 포커스 시프트 예측
  SMO 영향: OPC 모델 정확도 → SMO 결과 영향

결과:
  Low-n: M3D 감소 확인 → OPC 모델 단순화 가능
  High-k: 얇은 흡수체 → M3D 부분 감소
  재캘리브레이션: 새 흡수체에 맞는 OPC 컴팩트 모델 가능
  정확도: 재캘리브레이션 후 기존 TaN과 동등 수준
```

### High-NA EUV 적용
```
Low-n 흡수체 + High-NA:
  필요성: High-NA → M3D 더 심해짐 → low-n 필요성 증가
  아나모픽 효과: 4×/8× 비대칭 → 흡수체 방향 의존 M3D
  두께 최적화: 웨이브프론트 최적화 → 최소 두께 달성
  도즈 이득: low-n 얇은 흡수체 → 20-30% 도즈 감소 가능

OPC 모델 로드맵:
  현재 0.33NA: TaN OPC 모델 성숙
  High-NA 전환: Low-n 흡수체 + 아나모픽 OPC 모델 필요
  → 새로운 OPC 모델 개발 필수
```

## OPC 툴 구현 관련성
- **SKOPC EUV 모델**: low-n/high-k 흡수체 재료별 M3D 컴팩트 모델 파라미터 지원
- **재캘리브레이션 프레임워크**: 새 흡수체 도입 시 OPC 모델 빠른 재캘리브레이션 워크플로우
- **EUV SMO 확장**: 흡수체 재료에 따른 OPC/SMO 파라미터 최적화 세트 관리
- **High-NA 준비**: low-n 흡수체 + 아나모픽 OPC 통합 경로 설계

## 참고문헌
- Proc. SPIE 12495, SPIE Photomask Technology + EUV Lithography 2023, 124950P
- DOI: https://doi.org/10.1117/12.2658720
- 관련: Low-n absorber EUV mask manufacturing (IBM Research, SPIE 2024)
- 관련: Novel high-k mask absorber (SPIE 12292, 2022)
- 관련: High-k near n≈1 EUV mask (EUV Litho Workshop 2023)
- 관련: EUV stochastic OPC (Vaglio Pret, SPIE 2019)

## 태그
`Recipe`, `SPIE`, `EUV`, `MaskAbsorber`, `LowN`, `HighK`, `M3DEffects`, `OPCModel`, `CompactModel`, `ModelCalibration`, `HighNA`, `TaN`, `Ruthenium`, `2023`
