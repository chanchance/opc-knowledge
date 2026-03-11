# Correction for Etch Proximity: New Models and Applications

## 메타데이터
- **저자**: Yuri Granik
- **연도**: 2001
- **게재지**: Proc. SPIE 4346, Optical Microlithography XIV
- **DOI/URL**: https://doi.org/10.1117/12.435649

## 핵심 요약
에치 근접 보정(EPC)을 위한 새로운 모델과 응용을 제시한다. 모델 기반 보정으로 폴리 및 메탈 레이어의 iso/dense 바이어스와 inverse-iso/dense 바이어스를 보상하여 CD 균일도를 개선하고, 복잡한 2D 근접 효과도 포착한다.

## 주요 기여
1. 에치 근접 보정(EPC)을 위한 새로운 물리 기반 모델 제안
2. 폴리 및 메탈 레이어의 iso/dense CD 바이어스 보상 방법
3. Inverse iso/dense 바이어스 처리 모델
4. 2D 에치 근접 효과 포착 능력 입증
5. 모델 기반 EPC의 CD 균일도 향상 효과 정량화 (초기 선구적 연구)

## 모델 수식/아키텍처
- **에치 근접 모델**:
  - 1D 바이어스: B_etch = B_iso + (B_dense - B_iso) · f(pitch, CD)
  - Iso/dense 전환 함수: f(pitch) = 1 - exp(-pitch/λ_etch)
  - 2D 효과: 국소 패턴 밀도 커널 합산 B_2D = Σ K_etch * m(x,y)
- 보정 흐름: CD_target → B_etch(environment) → 마스크 CD 조정
- 응용: 폴리 게이트, 금속 배선 레이어의 iso/dense 바이어스 보상

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [ ] ML/DL
- [x] 하이브리드 (물리 기반 에치 컴팩트 모델)

## OPC 툴 구현 관련성
- SKOPC EPC 모듈의 역사적 기반 — 에치 근접 보정 모델의 원형
- Granik의 에치 모델은 후속 컴팩트 EPC 모델(커널 기반)의 시작점
- `2005_Beale_EtchModel_FullChip_PPC.md` 등 후속 연구의 선행 논문
- `2020_Granik_ResistShrinkageCompactModel_OPC.md`와 같은 저자의 초기 연구

## 태그
`Model`, `Etch`, `EPC`, `IsoDense`, `ProximityCorrection`, `CompactModel`, `Granik`, `SPIE`
