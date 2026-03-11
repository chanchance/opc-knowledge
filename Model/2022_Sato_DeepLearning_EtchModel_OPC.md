# OPC Accuracy Improvement Through Deep-Learning Based Etch Model

## 메타데이터
- **저자**: Sato, T. et al. (Synopsys / TSMC)
- **연도**: 2022
- **게재지**: Proc. SPIE 12056, DTCO and Computational Patterning I
- **DOI/URL**: https://doi.org/10.1117/12.2613926
- **인용수**: ~18

## 핵심 요약
DUV 리소그래피-에칭 공정에서 딥러닝 기반 에칭 모델을 활용하여 OPC 정확도를 향상시키는 방법을 제시한다. 대규모 SEM 메트롤로지 데이터와 자동화 메트롤로지 소프트웨어를 통해 고품질 게이지를 수집하고, Newron 에칭 모델이 기존 항(term) 기반 에칭 모델 대비 캘리브레이션 정확도를 50% 이상 개선함을 실증한다.

## 주요 기여
1. 딥러닝(Newron) 에칭 모델의 OPC 플로우 통합 방법론
2. 대규모 SEM 자동 메트롤로지 데이터 수집 → 에칭 게이지 추출
3. Newron 에칭 모델: 테스트 패턴 50%, 실제 칩 패턴 35% 정확도 향상
4. 기존 항 기반 에칭 모델 vs. DL 에칭 모델 정량 비교
5. 전체 OPC 플로우에서 리소-에칭 연계 모델의 실제 적용 사례

## 모델 수식/아키텍처

**기존 항 기반 에칭 모델:**
```
CD_etch = CD_litho + Σ_k c_k · f_k(CD_litho, density, pitch, ...)
```
c_k = 캘리브레이션 계수, f_k = 공정 의존 특성 함수

**딥러닝 에칭 모델 (Newron):**
```
CD_etch = DNN(CD_litho, layout_context_features)
```
입력: 리소 CD + 주변 레이아웃 컨텍스트 (local density, pitch, orientation 등)
출력: 에칭 후 CD 예측

**레이아웃 컨텍스트 특성 추출:**
```
context_features = {density_map(r), pitch_histogram, CD_neighbors, orientation_map}
```
r = 수십~수백 nm 범위의 영역별 밀도 맵

**통합 OPC 모델 (리소 + 에칭):**
```
CD_final = Etch_Model(Litho_Model(mask_pattern, optical_params), layout_context)
OPC_target: CD_final → CD_target
```

**정확도 메트릭:**
```
RMS_improvement = (RMS_term_etch - RMS_DL_etch) / RMS_term_etch × 100%
```

## 모델 유형
- [ ] 광학 모델
- [ ] 레지스트 모델
- [x] ML/DL (딥러닝 에칭 모델)
- [x] 하이브리드 (물리 리소 모델 + DL 에칭 모델)

## OPC 툴 구현 관련성
- 최신 OPC 플로우는 리소 모델 + 에칭 모델 연계가 표준화 추세
- skopc/modeling/etch_model/ 구현 시 딥러닝 에칭 모델 옵션 추가 고려
- 에칭 모델 캘리브레이션: 리소 후 + 에칭 후 CD-SEM 모두 필요
- 레이아웃 컨텍스트(주변 패턴 밀도) 계산이 핵심 전처리 단계
- Newron: Synopsys Proteus OPC 툴의 ML 에칭 모델 컴포넌트

## 참고문헌
- Sturtevant, J. et al., "Roadmap to sub-nanometer OPC model accuracy" (2012)
- Zuniga, C. et al., "CM1 standard process model" (2007)
- Synopsys Proteus OPC documentation

## 태그
`Model`, `SPIE`, `EtchModel`, `DeepLearning`, `OPC`, `Calibration`, `Hybrid`, `DUV`, `2022`
