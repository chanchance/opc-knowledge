# Exploring Alternative EUV Mask Absorber for iN5 Self-Aligned Block and Contact Layers

## 메타데이터
- **저자**: Rajiv Sejpal, Vicky Philipsen, Ana Armeanu, Chih-I Wei, Werner Gillijns, Neal Lafferty, Germain Fenger, Eric Hendrickx
- **소속**: imec (벨기에)
- **연도**: 2019
- **게재지**: Proc. SPIE 11148, Photomask Technology 2019, 111481B (26 September 2019)
- **DOI/URL**: https://doi.org/10.1117/12.2536892

## 핵심 요약
EUV 마스크 3D 효과를 완화하는 대안적 마스크 흡수층(High-k absorber, AttPSM) 두 후보를 기존 Ta 기반 TaBN 흡수층과 비교 평가한다. Mentor의 pxSMO 툴과 ASML NXE3400B 설정을 사용한 리소그래피 소스-마스크 최적화(SMO)를 통해 메모리 및 로직 레이어에서의 광학 성능을 정량화한다.

## 주요 기여
1. **High-k 흡수층 SMO 성능**: 메모리 케이스에서 High-k 흡수층이 기존 TaBN 대비 더 높은 cDOF, 낮은 EPE 달성
2. **AttPSM 흡수층 NILS 향상**: AttPSM 흡수층에서 정규화 이미지 대수 기울기(NILS) 유의미한 개선
3. **iN5 레이어 특화 분석**: 자기 정렬 블록(SAB) 및 콘택 레이어에서 대안 흡수층 평가
4. **SMO 기반 흡수층 선택 방법론**: SMO를 활용한 마스크 재료 선택의 정량적 기준 제시

## 알고리즘/수식
### SMO 기반 마스크 흡수층 비교 프레임워크
```
비교 대상:
1. 기준선: TaBN (60nm, 기존 표준)
   - n, k 값: 표준 Ta 기반
   - M3D 효과: 강함

2. High-k 흡수층:
   - 높은 EUV 소멸 계수 k → 얇은 흡수층 가능
   - M3D 효과 감소
   - SMO 결과: 더 높은 cDOF, 낮은 EPE

3. AttPSM (감쇠 위상 이동 마스크):
   - 부분 반사 + 위상 이동 효과 활용
   - SMO 결과: 높은 NILS 향상

평가 메트릭:
- cDOF: 공통 심도 (포커스 허용 범위)
- EPE: 엣지 배치 오차
- NILS: 정규화 이미지 대수 기울기 (대비도 척도)
- MEEF: 마스크 오차 증강 인수
```

### 조명 최적화 (pxSMO)
```
SMO 설정:
- 툴: Mentor pxSMO (픽셀화 SMO)
- 스캐너: ASML NXE3400B (0.33NA EUV)
- 소스: 픽셀화 조명 최적화
- 마스크: 각 흡수층 재료에 최적화

비용 함수:
min_{J, M} Σ_p ||CD_p - CD_target||² + λ₁·MEEF + λ₂·EPE_max
subject to: NILS ≥ NILS_min, cDOF ≥ DOF_min
```

## OPC 툴 SMO 구현 관련성
- EUV SMO에서 마스크 흡수층 재료가 성능에 미치는 영향 정량화
- 마스크 재료 선택을 SMO 비용 함수의 파라미터로 통합하는 접근법
- 픽셀화 SMO(pxSMO)의 구체적 구현 및 메트릭 기준 제시
- SKOPC SMO 모듈에서 다양한 EUV 마스크 타입(binary, attPSM, high-k) 지원 필요성

## 태그
`SMO`, `EUV`, `mask_absorber`, `High_k`, `AttPSM`, `TaBN`, `M3D`, `iN5`, `NILS`, `cDOF`, `pxSMO`, `SPIE`
