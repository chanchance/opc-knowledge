# Resolution Improvement and Dose Reduction in Logic and Memory Applications from Low NA to High NA

## 메타데이터
- **저자**: Shubhankar Das, Victor Blanco, Van Tuong Pham, Shruti Jambaldinni, Anuja De Silva, Joern-Holger Franke, Marcus Newman, Ali Haider, Matt Gallagher, Jeonghoon Lee, Kaushik Sah, Zhijin Chen, Bobo Cheng, Chenwei Gong, Vidya Ramanathan, Andrew Cross, Werner Gillijns, Hyo Seon Suh, Philippe Foubert, John Petersen, Pieter Vanelderen, Geert Vandenberghe, Kurt Ronse, Sandip Halder, Philippe Leray
- **소속**: imec (벨기에) 및 협력 기관
- **연도**: 2025
- **게재지**: Proc. SPIE 13424, Optical and EUV Nanolithography XXXVIII, 1342413 (22 April 2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051512

## 핵심 요약
0.33NA(저NA)에서 0.55NA(고NA) EUV로의 마이그레이션에서 로직 및 메모리 응용의 해상도 향상과 도즈 감소를 체계적으로 비교한다. 고NA 단일 노출이 복잡한 다중 패터닝 기술을 대체할 잠재력을 보이며, DRAM BLP/SNLP에서 도즈를 ~40% 감소시킨다.

## 주요 기여
1. **저NA→고NA 마이그레이션 종합 비교**: 로직 메탈 PnR 및 DRAM BLP/SNLP에서 0.33NA vs 0.55NA 체계적 비교
2. **도즈 40% 감소**: 0.55NA에서 28nm 피치 DRAM 단일 노출, 0.33NA 34nm 피치 대비 ~40% 도즈 감소
3. **다중 패터닝 대체 가능성**: 고NA 단일 노출이 복잡한 MPT 대체 가능함을 시연
4. **드라이 레지스트 활용**: 드라이 레지스트 사용으로 고NA 패터닝 성능 향상

## 알고리즘/수식
### 저NA→고NA 성능 지표 비교
```
0.33NA (저NA) 기준:
  DRAM BLP/SNLP: 피치 34nm, 도즈 D₀

0.55NA (고NA) 결과:
  DRAM BLP/SNLP: 피치 28nm, 도즈 ~0.6×D₀ (~40% 감소)

해상도 향상:
  k1 = CD × NA / λ
  0.33NA: k1 ≥ 0.33 (해상도 한계)
  0.55NA: 동일 CD에서 k1 더 큰 여유 또는 더 작은 CD 달성

단일 노출 가능 조건:
  0.55NA 단일 노출 ↔ 0.33NA + MPT
```

### 타겟 사용 사례
1. **로직**: Aligned T2T(Track-to-Track) 구조, 메탈 PnR(Place and Route)
2. **메모리**: DRAM BLP/SNLP (피치 28nm, 드라이 레지스트)

### 핵심 결과
- DRAM 28nm 피치: DOF 및 EL 공정 창 확보
- 도즈 감소: ~40% (0.33NA P34nm 단일 노출 대비)
- MPT 회피: 고NA 단일 노출로 복잡한 다중 패터닝 불필요

## OPC 툴 SMO 구현 관련성
- 0.33NA→0.55NA 마이그레이션 시 SMO 완전 재설계 필요
- 고NA에서 도즈 감소는 SMO 비용 함수의 새로운 목표 추가 가능
- 드라이 레지스트 모델: SMO 레지스트 모델 업데이트 필요
- MPT 회피를 위한 고NA SMO 설계 기준 (k1, DOF, EL 목표값)

## 태그
`SMO`, `EUV`, `high_NA`, `0.55NA`, `0.33NA`, `DRAM`, `logic`, `dose_reduction`, `resolution`, `dry_resist`, `MPT`, `imec`, `SPIE`
