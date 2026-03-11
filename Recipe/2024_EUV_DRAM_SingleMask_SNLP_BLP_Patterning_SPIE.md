# Patterning Optimization for Single Mask Bit-Line-Periphery and Storage-Node-Landing-Pad DRAM Layers Using 0.33NA EUV Lithography at the Resolution Limit

## 메타데이터
- **저자**: (imec 협력팀, SPIE 2024)
- **연도**: 2024
- **게재지**: Proc. SPIE 12957, Advances in Patterning Materials and Processes XLI, 129570V (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010934
- **인용수**: ~10

## 핵심 요약
0.33NA EUV 리소그래피를 활용한 차세대 DRAM의 비트라인 주변부(BLP)와 스토리지 노드 랜딩 패드(SNLP) 레이어를 단일 마스크로 패터닝하는 최적화 방법을 제시한다. 피치 34nm DRAM 레이어에서 CD 공정 윈도우, 결함, 균일성을 최적화하여 DOF 119nm, EL 25%의 대형 공정 윈도우를 달성하고, low-n 마스크로 피치 32nm SNLP/BLP 달성을 보여주며 0.33NA EUV 리소그래피의 해상도 한계를 탐색한다.

## 주요 기여
1. 피치 34nm DRAM BLP-SNLP 단일 마스크 EUV 패터닝 최적화 방법
2. 스핀온 금속 산화물 레지스트 + 다크 필드 바이너리 마스크 조합
3. DOF 119nm, EL 25% 대형 공정 윈도우 달성
4. Low-n 마스크로 피치 32nm SNLP/BLP 해상도 한계 탐색

## Recipe/Process Flow 상세

### DRAM 패터닝 배경
```
DRAM 스케일링 트렌드:
  메모리 셀 반피치:
    1x → 1y → 1z → 1α → 1β → 1γ 노드
    각 세대: 약 10-15% 피치 축소

  BLP (Bit-Line-Periphery):
    기능: 비트라인 접촉 패드 영역
    패턴: 조밀한 접촉홀 배열
    과제: 고밀도, 균일한 CD, 낮은 오버레이 오차

  SNLP (Storage-Node-Landing-Pad):
    기능: 커패시터 스토리지 노드 랜딩 패드
    패턴: 매우 조밀한 패드 배열
    과제: 소면적, 고종횡비, 피치 < 36nm

단일 마스크 전략:
  전통: BLP + SNLP 별도 마스크 → 더블/멀티 패터닝
  EUV 단일: 0.33NA EUV 고해상도 → 단일 마스크 가능
  장점: 마스크 비용 절감, 오버레이 오차 감소, 공정 단순화
```

### 패터닝 최적화 방법
```
마스크 설계:
  마스크 유형: 다크 필드 바이너리 마스크 (CoA, Chrome-on-Absorber)
  마스크 소재: 표준 TaN 또는 low-n 흡수체
  RET 기법:
    - OPC: 모델 기반 OPC, 근접 효과 보정
    - SMO: 소스-마스크 최적화로 공정 윈도우 극대화
    - SRAF: 서브해상도 보조 피처 추가

레지스트:
  재료: 스핀온 금속 산화물 레지스트 (CAR 대비 고해상도)
  특성:
    - 높은 EUV 흡수 → 더 낮은 도즈 필요
    - 낮은 LWR (라인 폭 거칠기)
    - 우수한 에칭 선택비

리소그래피 최적화:
  노광 조건:
    - 도즈-투-사이즈(DTS): 89.4 mJ/cm²
    - 조명: 최적화된 SMO 소스
  공정 윈도우 평가:
    - DOF: 초점 범위 최적화
    - EL (노광 위도): 도즈 허용 범위
    - OPIC (겹치는 공정 윈도우): BLP + SNLP 동시 만족
```

### OPC 공정 흐름
```
1. 레이아웃 준비:
   설계 규칙 검증
   BLP + SNLP 레이어 합성

2. 리소그래피 시뮬레이션:
   EUV 0.33NA 광학 모델
   레지스트 모델 (금속 산화물 레지스트 캘리브레이션)
   예측: CD, 공정 윈도우, 핫스팟

3. SMO (소스-마스크 최적화):
   DRAM 반복 패턴에 최적화된 광원 형상
   동시 마스크 OPC: 접촉홀 어시스트 피처 최적화

4. OPC:
   모델 기반 OPC: CD 균일성 최적화
   2D 보정: 코너, 끝단 효과 보정
   SRAF: 인쇄 마진 향상 보조 피처

5. 검증:
   시뮬 기반: EPE, PV Band, 핫스팟 검출
   실제 인쇄: SEM 계측, CD 측정, 결함 검사

6. 결과:
   피치 34nm: DOF 119nm, EL 25%
   Low-n 마스크: 피치 32nm 달성 (해상도 한계)
```

### 성능 결과
```
피치 34nm (표준 TaN 마스크):
  DOF: 119nm (대형 공정 윈도우)
  EL: 25% (충분한 도즈 여유)
  결함: 도즈 20mJ/cm² 범위에서 무결함
  DTS: 89.4 mJ/cm²

피치 32nm (Low-n 마스크):
  해상도 한계 탐색
  단일 마스크 SNLP/BLP 달성
  0.33NA 현재 한계 확인

0.33NA EUV 해상도 한계:
  실용적 한계: ~34-36nm 피치 (표준 마스크)
  Low-n 마스크 활용: ~32nm 피치까지 연장
  High-NA EUV 전환 포인트: 피치 <32nm
```

## OPC 툴 구현 관련성
- **SKOPC 메모리 OPC**: DRAM 접촉홀/랜딩패드 패턴 OPC 레시피 개발 참고
- **EUV 컴팩트 모델**: 금속 산화물 레지스트 캘리브레이션 방법 참고
- **SMO 목표**: 반복 DRAM 패턴에 최적화된 SMO 소스 형상 설계
- **해상도 한계**: 0.33NA EUV OPC 적용 가능 최소 피치 기준 수립

## 참고문헌
- Proc. SPIE 12957, Advances in Patterning Materials and Processes XLI, 129570V (2024)
- 관련: Single mask BLP-SNLP 0.33NA EUV (SPIE 12292, 2022; SPIE 12495, 2023)
- 관련: EUV DRAM multi-patterning (SPIE 2022)
- 관련: High-NA EUV DRAM patterning (imec, IEDM 2024)
- 관련: Low-n absorber EUV mask OPC (SPIE 12495, 2023)

## 태그
`Recipe`, `SPIE`, `DRAM`, `EUV`, `SingleMask`, `BLP`, `SNLP`, `Patterning`, `0.33NA`, `ProcessWindow`, `ResolutionLimit`, `MetalOxideResist`, `LowN`, `Memory`, `2024`
