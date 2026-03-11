# Patterning Optimization for Single Exposure BLP and SNLP DRAM Layers with 0.33NA and 0.55NA EUV Lithography

## 메타데이터
- **저자**: Van Tuong Pham, et al. (imec, 벨기에)
- **연도**: 2025
- **게재지**: Proc. SPIE 13428, Advances in Patterning Materials and Processes XLII, 134280T (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051494

## 핵심 요약
0.33NA와 0.55NA EUV 리소그래피를 비교하여 DRAM BLP/SNLP 레이어의 단일 노출 패터닝을 최적화한다. 0.33NA 34nm 피치에서 기존 대비 도즈 20% 감소, 28~32nm 피치에서 30~50% 도즈 감소를 달성하며, 0.55NA에서 28nm HEX-pillar 구조에서 DOF ~80nm를 시연한다.

## 주요 기여
1. **0.33NA vs 0.55NA 비교**: 두 NA 조건에서 DRAM 패터닝 성능 체계적 비교
2. **도즈 감소**: 0.33NA에서 20~50% 도즈 감소 달성 (기존 대비)
3. **고NA 초기 결과**: 0.55NA에서 28nm HEX-pillar DOF ~80nm 시연
4. **이전 연구 연속성**: 2023, 2024년 동일 그룹의 DRAM SMO 연구 시리즈의 최신작

## 알고리즘/수식
### 0.33NA vs 0.55NA EUV 비교
```
0.33NA EUV:
  피치 34nm: 도즈 20% 감소 (기존 대비)
  피치 28-32nm: 도즈 30-50% 감소
  방법: SMO + 레지스트 모델 OPC 최적화

0.55NA EUV (고NA):
  피치 28nm HEX-pillar: DOF ~80nm
  장점: 더 낮은 k1 → 해상도 향상
  도전: 새로운 렌즈 수차, 마스크 이슈
```

### 성능 지표
- **도즈-to-size**: 타겟 CD를 인쇄하는 최소 도즈
- **DOF**: 공정 허용 초점 범위
- **EL**: 도즈 허용 범위

## OPC 툴 SMO 구현 관련성
- 0.33NA → 0.55NA 마이그레이션에서 SMO 재최적화 필요성 확인
- DRAM BLP/SNLP 레이어의 연도별 SMO 플로우 개선 추적 가능
- 고NA EUV에서 DOF ~80nm는 SMO 비용 함수의 DOF 목표 설정 참조값

## 태그
`SMO`, `OPC`, `EUV`, `DRAM`, `BLP`, `SNLP`, `0.33NA`, `0.55NA`, `high_NA`, `dose_reduction`, `imec`, `SPIE`
