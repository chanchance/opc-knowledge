# Optimizing EUV OPC Runtime and Pattern Fidelity in DRAM Manufacturing

## 메타데이터
- **저자**: Shu De Gong, Sheng Tse Chen, Chun Cheng Liao, Teng Yen Huang, Renyang Meng, Kiho Yang, Werner Gillijns, Hsin-jung Lin, Shou-yuan Ma, JenHsiang Tsai, Ling Chieh Lin, Ryan Chou, Andrew Burbine, Alex Pearson, Xima Zhang
- **연도**: 2025
- **게재지**: Proc. SPIE 13427, Novel Patterning Technologies 2025
- **DOI/URL**: https://doi.org/10.1117/12.3051007

## 핵심 요약
DRAM 제조 환경에서 EUV OPC의 런타임을 85% 이상 단축하면서 패턴 피델리티를 유지하는 혁신적 메모리 최적화 OPC 플로우를 제시한다. Slit-Aware Memory OPC 방식을 도입해 메모리의 반복적 특성을 활용하고, EUV 특유의 슬릿(thru-slit) 효과와 플레어(flare)를 효과적으로 보정한다. 실험 결과 런타임 85% 이상 단축, 마스크 일관성 향상, 슬릿 효과의 정확한 보정 달성을 확인했다.

## 주요 기여
1. **Slit-Aware Memory OPC**: DRAM 반복 구조를 활용한 연산 최적화 OPC 플로우
2. EUV 슬릿(thru-slit) 효과의 정확한 보정 방법론
3. 플레어(flare) 보정을 포함한 DRAM 특화 EUV OPC 시뮬레이션
4. **런타임 85% 이상 단축** 달성하면서 패턴 피델리티 유지
5. 마스크 일관성(mask consistency) 향상 검증
6. 미래 DRAM 제조를 위한 강건하고 효율적인 OPC 기반 플로우 제시

## 검증 방법론
- **대상**: EUV DRAM 레이어 (반복 패턴 구조)
- **비교 기준**: 기존 OPC 플로우 대비 런타임 및 패턴 정확도
- **EUV 특유 효과**: Thru-slit 효과, 플레어 효과 보정 결과 검증
- **핵심 지표**: 런타임 감소율 (>85%), 마스크 일관성, 슬릿 효과 보정 정확도
- **산업 파트너**: 삼성 + Siemens EDA 협력 연구

## OPC 툴 구현 관련성
- DRAM 메모리 레이어의 반복 구조를 OPC 연산에 활용하는 계층적 최적화 전략
- EUV 슬릿-평균 조명 불균일성(slit-averaged vs slit-aware) OPC의 차이와 구현 방법
- EUV 플레어 보정을 OPC 플로우에 통합하는 방법
- 풀칩 OPC 런타임 최적화의 실증적 사례 (85% 단축)
- 메모리 반도체 EUV OPC 검증 기준 논문

## 태그
`Verification`, `EUV`, `OPCRuntime`, `DRAM`, `Memory`, `SlitEffect`, `Flare`, `PatternFidelity`, `Manufacturing`, `SPIE`, `2025`
