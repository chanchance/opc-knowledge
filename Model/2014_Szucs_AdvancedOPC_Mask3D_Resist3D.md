# Advanced OPC Mask-3D and Resist-3D Modeling

## 메타데이터
- **저자**: Szucs, A., Planchot, J., Farys, V., Yesilada, E., Depre, L., Kapasi, S., Gourgon, C., Besacier, M., Mouraille, O., Driessen, F.
- **연도**: 2014
- **게재지**: Proc. SPIE 9052, Optical Microlithography XXVII
- **DOI/URL**: https://doi.org/10.1117/12.2047281
- **인용수**: ~40

## 핵심 요약
28nm 메탈 레이어의 복잡한 2D 레이아웃 구조 제어를 위해 신뢰성 있는 Mask-3D(M3D)와 Resist-3D(R3D) 모델을 구축하는 방법을 제시한다. 3D 모델링이 공정 변동 예측 정확도를 향상시키고 공정 윈도우 한계 구조에 대한 OPC 제어를 개선함을 실증한다. immersion 및 EUV 리소그래피 모두에 적용 가능한 통합 3D OPC 모델링 프레임워크를 제안한다.

## 주요 기여
1. M3D(마스크 3D)와 R3D(레지스트 3D)를 통합한 OPC 모델 구축 방법론
2. 28nm 메탈 레이어에서 2D 복잡 구조 공정 윈도우 예측 정확도 향상
3. 컴팩트 M3D 모델의 안정적 캘리브레이션 절차
4. R3D 모델: 레지스트 상부 손실(top-loss) 및 프로파일 효과 포함
5. 실제 양산 환경에서의 적용 가능성 검증

## 모델 수식/아키텍처

**컴팩트 M3D 모델 (Hopkins 섭동 이론 기반):**
```
E_M3D(f,g) = E_Kirchhoff(f,g) · [1 + Σ_k α_k · P_k(f,g)]
```
α_k = M3D 보정 계수, P_k = 피치/방향 의존 기저함수

**Best Focus 이동 (M3D 유발):**
```
ΔBF(pitch, azimuth) = Σ_k β_k · cos(k·azimuth) · h_k(pitch)
```
β_k = 조명/마스크 스택 의존 계수

**Resist-3D 모델 (레지스트 프로파일 포함):**
```
CD_bottom = CD_aerial_image(I, threshold_bottom)
CD_top = CD_aerial_image(I, threshold_top)
CD_eff = w_b · CD_bottom + w_t · CD_top   [가중 평균]
```
threshold_top > threshold_bottom: 레지스트 상부가 더 좁게 현상

**레지스트 상부 손실 모델:**
```
H_eff(x) = H_nominal - α_toploss · dose · exp(-β · CD)
```

**통합 3D OPC 모델 캘리브레이션:**
```
min_{α,β,w} Σ_patterns [w_i · (CD_M3D_R3D,i - CD_meas,i)²]
```
Focus-Exposure 매트릭스 전체 범위에서 캘리브레이션

## 모델 유형
- [x] 광학 모델 (M3D)
- [x] 레지스트 모델 (R3D)
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- 28nm 이하 노드에서 M3D + R3D 통합 모델이 OPC 정확도 핵심
- skopc/modeling/mask3d.py + resist3d.py 구현 참조
- 컴팩트 M3D: SOCS 커널에 피치/방향 의존 보정 항 추가로 구현
- R3D top-loss: OPC 모델의 유효 CD 정의에 가중 평균 방식 적용
- 캘리브레이션 데이터: Focus-Exposure 매트릭스 필수

## 참고문헌
- Erdmann, A. et al., "Mask 3D effects on resist model calibration" (2009)
- Sturtevant, J. et al., "Roadmap to sub-nanometer OPC model accuracy" (2012)
- Mentor/Synopsys M3D compact model documentation

## 태그
`Model`, `SPIE`, `Mask3D`, `Resist3D`, `CompactModel`, `OPCModel`, `Calibration`, `28nm`, `ProcessWindow`, `2014`
