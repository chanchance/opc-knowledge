# EUV DRAM Patterning Historic Overview and Future Assumption

## 메타데이터
- **저자**: (SPIE 13425 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134250V (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3052340

## 핵심 요약
EUV 리소그래피를 이용한 DRAM 패터닝의 역사적 발전 과정을 개괄하고, BLP/SNLP 등 핵심 DRAM 레이어의 미래 가정을 제시한다. 금속성 레지스트와 전산 시뮬레이션을 활용한 EUV DRAM 패터닝의 최신 발전 사항을 정리한다.

## 주요 기여
1. **EUV DRAM 패터닝 역사 정리**: 세대별 EUV DRAM 기술 발전 과정 체계화
2. **BLP/SNLP 패터닝 발전**: 비트라인 주변부와 스토리지 노드 착지패드 EUV 패터닝
3. **금속성 레지스트 적용**: metallic resist를 활용한 DRAM EUV 패터닝 발전
4. **미래 로드맵 예측**: 향후 DRAM 노드 스케일링을 위한 EUV 패터닝 방향성

## 알고리즘/수식
### DRAM EUV 패터닝 발전 단계
```
DRAM EUV 패터닝 역사:
  1세대: ArF → EUV 전환 (첫 EUV DRAM 레이어 도입)
  2세대: EUV 단일 패터닝 BLP/SNLP (이중 패터닝 대체)
  3세대: 고NA EUV DRAM (0.55NA, 더 미세 피치)
  미래: 하이퍼NA EUV 또는 SADP+EUV 결합

주요 DRAM 레이어:
  BLP (Bit-Line Periphery): 비트라인 주변부 패턴
  SNLP (Storage-Node Landing Pad): 스토리지 노드 착지패드
  → 두 레이어 모두 높은 2D 패턴 복잡도

SMO/OPC 역할:
  단일 마스크 EUV 패터닝 실현 → SMO 필수
  BLP/SNLP 동시 최적화 → 공정 창 확보
```

### 미래 패터닝 가정
```
1x nm 이하 노드:
  0.33NA EUV 한계 → 고NA EUV or SADP 필요
  SMO 강화 + 금속성 레지스트 + 곡선형 마스크 결합

금속성 레지스트 이점:
  도즈 감도 향상 → 처리량 증가
  확률론적 특성 개선 → LCDU 감소
  → EUV DRAM 스케일링 핵심 기술
```

## OPC 툴 SMO 구현 관련성
- DRAM BLP/SNLP SMO: SKOPC SMO 모듈에서 DRAM 특화 레이어 최적화
- 역사적 SMO 발전: DRAM EUV 패터닝에서 SMO 역할 변화 이해
- 금속성 레지스트 OPC: 새로운 레지스트 타입에 맞는 OPC 모델 업데이트
- 미래 로드맵: 고NA EUV DRAM을 위한 SMO/OPC 발전 방향

## 태그
`EUV`, `DRAM`, `BLP`, `SNLP`, `history`, `roadmap`, `metallic_resist`, `SMO`, `OPC`, `DTCO`, `SPIE`, `2025`
