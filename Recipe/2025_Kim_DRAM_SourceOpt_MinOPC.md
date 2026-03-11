# Source Optimization for DRAM Critical Layer with Minimum Optical Proximity Correction

## 메타데이터
- **저자**: Min-Woo Kim, Da-Kyung Yu, Yu-Jin Chae, Hee-Chang Ko, Ji-Won Kang, Michael Yeung, Seung-Woo Son, Hye-Keun Oh
- **소속**: Hanyang University (Korea), Fastlitho Inc. (USA)
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 134241N
- **DOI/URL**: https://doi.org/10.1117/12.3054260

## 핵심 요약
DRAM critical layer에서 SMO(Source Mask Optimization)를 통해 광원을 최적화하여 OPC 보정량을 최소화(minimum OPC)하는 전략을 제안한다. 광원이 충분히 최적화되면 패턴 왜곡이 줄어 OPC의 보정 부담이 감소하고, 마스크 복잡도 및 런타임이 개선된다. EUV DRAM critical layer(BLP, SNLP 등)를 대상으로 anamorphic 광학계와 arc-slit illumination의 특수성을 고려한다.

## 주요 기여
1. **Source-first 전략**: OPC 전에 광원을 충분히 최적화하여 OPC 보정량 자체를 최소화
2. **DRAM critical layer 특화**: BLP(Bit-Line Periphery), SNLP(Storage Node Landing Pad) 등 DRAM 핵심 레이어 적용
3. **EUV anamorphic 광학계 고려**: EUV의 비대칭 배율(anamorphic optics) 및 arc-slit illumination에서의 CD 불균일성 분석
4. **최소 OPC 접근**: 광원 최적화로 리소그래피 왜곡을 사전에 억제 → OPC는 잔류 오차만 보정
5. **Minimum OPC 정량화**: 충분한 광원 최적화 후 필요한 최소 OPC 보정량 및 마스크 단순화 효과 평가

## Recipe/Flow 상세
```
[Source-Optimized Minimum OPC Flow for DRAM]
1. DRAM Critical Layer 분석:
   - 대상: BLP, SNLP, Active layer 등
   - EUV 파라미터: λ=13.5nm, NA, anamorphic magnification (4x/8x)
   - Arc-slit illumination 비균일성 파악
2. Source Optimization (SMO):
   - 광원 pupil 최적화 (자유도: pupil 픽셀 강도값)
   - 목표: 전체 slit에서 CD 균일성 + 공정 윈도우 최대화
   - Constraint: 물리적으로 실현 가능한 광원 형상
3. 최소 OPC 필요량 평가:
   - 최적화된 광원으로 리소그래피 시뮬레이션
   - 잔류 EPE 분포 분석 → OPC 필요 위치/크기 결정
4. Minimum OPC 실행:
   - 잔류 오차만 타겟으로 model-based OPC 적용
   - 기존 full OPC 대비 보정량 및 mask complexity 비교
5. 검증:
   - CD uniformity (x/y 방향, slit 전체)
   - 공정 윈도우 (DOF-EL)
   - 마스크 EPE 및 MEEF
```

### 핵심 파라미터
- **적용 노드**: EUV (13.5nm) DRAM critical layer
- **광학계**: Anamorphic (4x/8x), arc-slit illumination
- **목표**: minimum OPC (광원 최적화 후 잔류 오차만 보정)
- **핵심 지표**: CD uniformity, 공정 윈도우, 마스크 복잡도 감소율

## OPC 툴 구현 관련성
- `skopc/modeling/model_opc.py`: SMO 후 minimum OPC 플로우 구현 참고
- `skopc/pwo/`: 광원 최적화(SMO)와 OPC를 연계하는 co-optimization 구조 참고
- `recipes/example_euv.yaml`: EUV DRAM 레시피에 `source_optimization: true`, `min_opc_mode: true` 파라미터 추가 참고
- **SMO-OPC 연계**: SKOPC SMO 모듈과 OPC 모듈 간 파라미터 전달 인터페이스 설계에 활용

## 태그
`Recipe`, `SPIE`, `DRAM`, `EUV`, `Source Optimization`, `SMO`, `Minimum OPC`, `Anamorphic`, `BLP`, `SNLP`, `2025`
