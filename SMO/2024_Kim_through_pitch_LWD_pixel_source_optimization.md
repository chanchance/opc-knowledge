# Through Pitch Line Width Difference Minimization by Pixel Source Optimization

## 메타데이터
- **저자**: Min-Woo Kim, Da-Kyung Yu, Yu-Jin Chae, Hee-Chang Ko, Ji-Won Kang, Michael Yeung, Seung-Woo Son, Hye-Keun Oh
- **소속**: Hanyang University (한국), Fastlitho Inc. (미국)
- **연도**: 2024
- **게재지**: Proc. SPIE 13216, Photomask Technology 2024, 132162L (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3037354

## 핵심 요약
픽셀화 소스 최적화를 통해 다양한 피치(through-pitch) 조건에서 선폭 차이(Line Width Difference, LWD)를 최소화하는 방법을 연구한다. 0.33NA 및 0.55NA 조건에서 low-n 흡수층 재료를 사용하여 웨이퍼 상의 선폭 변동을 줄이고 OPC 부담을 경감한다.

## 주요 기여
1. **Through-pitch LWD 최소화**: 다양한 피치 범위에서 일관된 선폭 달성을 위한 소스 최적화
2. **0.33NA/0.55NA 동시 검토**: 두 NA 조건에서 동일 방법론 적용
3. **low-n 흡수층 호환**: 저굴절률 마스크 흡수층과 픽셀 소스 최적화 결합
4. **OPC 부담 경감**: 소스 최적화로 피치 간 CD 균일성 확보 → OPC 복잡도 감소

## 알고리즘/수식
### Through-pitch LWD 최소화 소스 최적화
```
비용 함수:
min_{J} Σ_{p} (LW(pitch_p) - LW_target)²
       + λ · Σ_{p≠q} (LW(pitch_p) - LW(pitch_q))²

여기서:
- J: 픽셀화 소스 강도 분포
- LW(pitch_p): p번째 피치에서의 선폭
- LW_target: 타겟 선폭
- 두 번째 항: 피치 간 선폭 차이 패널티

제약:
  0 ≤ J(f_m) ≤ J_max
  Σ_m J(f_m) = P_total
  NILS(pitch_p) ≥ NILS_min ∀p (모든 피치에서 충분한 대비)
```

### Through-pitch CD 균일성 메트릭
```
LWD = max_{p,q} |LW(pitch_p) - LW(pitch_q)|

최적화 목표: LWD 최소화
            피치 범위: 해당 레이어의 주요 피치 집합
```

### 조건
- NA: 0.33 / 0.55 (두 조건 모두)
- 마스크: low-n 흡수층 재료

## OPC 툴 SMO 구현 관련성
- Through-pitch 선폭 균일성: SMO 비용 함수에 피치 간 CD 차이 패널티 항 추가
- 픽셀화 소스 최적화로 OPC 복잡도 경감: 소스 최적화와 OPC의 역할 분담
- 0.55NA 고NA 마이그레이션 시 소스 재최적화 필요성 확인
- SKOPC SMO 모듈에서 through-pitch CD 균일성 비용 함수 설계 참조

## 태그
`source_optimization`, `through_pitch`, `LWD`, `CD_uniformity`, `EUV`, `high_NA`, `0.55NA`, `low_n_mask`, `pixel_source`, `SPIE`
