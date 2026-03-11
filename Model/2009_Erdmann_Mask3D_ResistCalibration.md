# Impact of Mask Three-Dimensional Effects on Resist-Model Calibration

## 메타데이터
- **저자**: Erdmann, A. et al. (Fraunhofer IISB)
- **연도**: 2009
- **게재지**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 8, No. 3
- **DOI/URL**: https://doi.org/10.1117/1.3158356
- **인용수**: ~60

## 핵심 요약
마스크 3D 효과(thick-mask EMF 효과)가 레지스트 모델 캘리브레이션에 미치는 영향을 정량적으로 분석한다. Kirchhoff(박막) 근사와 엄밀 EMF(전자기장) 시뮬레이션을 PROLITH 및 S-Litho 레지스트 모델과 결합하여 캘리브레이션 결과를 비교한다. 마스크 3D 효과를 무시하고 캘리브레이션된 레지스트 파라미터가 실제 공정과 다른 조건에서 예측 정확도를 저하시킴을 실증한다.

## 주요 기여
1. 마스크 3D(M3D) 효과와 레지스트 모델 캘리브레이션의 상호작용 체계적 분석
2. Kirchhoff 근사 vs. 엄밀 EMF 계산 비교 (PROLITH 10.2 / S-Litho)
3. Bossung 곡선(CD vs. focus/dose) 기반 캘리브레이션 프레임워크
4. 조명 조건 변화 시 캘리브레이션 이식성(portability) 평가
5. M3D 보정 없이 캘리브레이션된 모델의 예측 오차 정량화

## 모델 수식/아키텍처

**Kirchhoff 근사 (박막 마스크):**
```
t(x,y) = { 1  (transparent region)
          { 0  (opaque region)
```

**엄밀 EMF (RCWA/FDTD 기반):**
```
∇ × E = iωμH
∇ × H = -iωεE
```
마스크 크롬층(두께 ~70 nm) 및 MoSi 다층막의 3D 회절 효과 포함

**Bossung 캘리브레이션 오차 메트릭:**
```
RMS_error = sqrt( (1/N) Σ_i (CD_sim,i - CD_meas,i)² )
```

**M3D 보정 (Best Focus Shift):**
```
ΔBF(pitch, orientation) = f(mask_stack, NA, σ, wavelength)
```
피치·방향·조명 조건의 함수로 Best Focus 이동 예측

## 모델 유형
- [x] 광학 모델 (M3D EMF)
- [x] 레지스트 모델 (PROLITH/S-Litho 캘리브레이션)
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- OPC 모델 캘리브레이션 시 마스크 3D 효과를 반드시 고려해야 함
- skopc 컴팩트 M3D 모델 구현 시 Best Focus 이동 보정 항 필요
- 193nm 이하 노드(특히 EUV)에서 M3D 효과는 OPC 정확도에 수 nm 오차 유발
- 캘리브레이션 패턴: 다양한 피치·방향·조명 조건 포함 필수

## 참고문헌
- Mack, C.A., "PROLITH: A Comprehensive Optical Lithography Model" (1985)
- Rosenbluth, A.E. et al., "Fast TCC algorithm" (2005)
- Erdmann, A. et al., Fraunhofer IISB lithography simulation papers

## 태그
`Model`, `SPIE-JMM`, `Mask3D`, `EMF`, `ResistCalibration`, `PROLITH`, `SLitho`, `Kirchhoff`, `2009`
