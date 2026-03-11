# Source Optimization for DRAM Critical Layer with Minimum Optical Proximity Correction

## 메타데이터
- **저자**: Min-Woo Kim, Da-Kyung Yu, Yu-Jin Chae, Hee-Chang Ko, Ji-Won Kang, Michael Yeung, Seung-Woo Son, Hye-Keun Oh
- **소속**: Hanyang University (한국), Fastlitho Inc. (미국)
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 134241N (22 April 2025)
- **DOI/URL**: https://doi.org/10.1117/12.3054260

## 핵심 요약
DRAM 핵심 레이어에서 최소한의 OPC를 적용하면서 소스 최적화만으로 최대 패터닝 성능을 달성하는 방법을 연구한다. 공격적인 OPC 없이도 소스 최적화로 충분한 공정 창을 확보할 수 있음을 보이며, OPC 복잡도와 소스 최적화 간의 트레이드오프를 정량화한다.

## 주요 기여
1. **최소 OPC 소스 최적화**: OPC 의존도를 줄이면서 소스 최적화로 공정 창 확보
2. **DRAM 레이어 특화**: DRAM 핵심 레이어의 소스 최적화 전략 제시
3. **OPC-소스 트레이드오프 분석**: OPC 복잡도 vs 소스 자유도 간 균형 정량화
4. **실용적 SMO 접근**: 마스크 합성 부담을 줄이는 소스 중심 최적화 전략

## 알고리즘/수식
### 최소 OPC 소스 최적화 프레임워크
```
목표: OPC 복잡도 최소화하면서 공정 창 최대화

최적화 문제:
max_{J} PW(J) subject to:
  EPE_OPC(J, M_simple) ≤ EPE_budget
  NILS(J) ≥ NILS_min
  Σ J(f_m) = P_total

여기서:
- J: 소스 강도 분포 (최적화 변수)
- M_simple: 최소 OPC 마스크 (고정 또는 단순 바이어스만)
- PW: 공정 창 (DOF × EL)
- EPE_OPC: OPC 후 남은 엣지 배치 오차
```

### 핵심 아이디어
```
기존 SMO 접근:
  소스 최적화 + 복잡한 OPC (SRAF + 모델 기반 OPC)
  → 높은 마스크 복잡도, 긴 TAT

최소 OPC 소스 최적화:
  강화된 소스 최적화 + 단순 OPC (기본 바이어스만)
  → 낮은 마스크 복잡도, 짧은 TAT, 유사한 공정 창
  트레이드오프: 소스 자유도 ↑, OPC 복잡도 ↓
```

### 타겟
- DRAM 핵심 레이어 (BLP, SNLP 등)
- EUV 리소그래피 조건

## OPC 툴 SMO 구현 관련성
- 소스 최적화와 OPC의 책임 분리: 소스 중심 최적화로 마스크 합성 부담 경감
- DRAM 레이어용 소스 최적화 전략: SKOPC의 DRAM 모드에서 참조
- 최소 OPC 모드: 빠른 TAT가 필요한 응용에서 소스 최적화 우선 전략
- 소스 최적화 비용 함수: OPC 복잡도 패널티 항 통합 가능성

## 태그
`source_optimization`, `DRAM`, `minimum_OPC`, `EUV`, `process_window`, `NILS`, `Hanyang`, `Fastlitho`, `SPIE`
