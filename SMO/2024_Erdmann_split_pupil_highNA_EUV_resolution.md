# Resolution Enhancement for High-Numerical Aperture Extreme Ultraviolet Lithography by Split Pupil Exposures: A Modeling Perspective

## 메타데이터
- **저자**: Andreas Erdmann, Hazem Mesilhy, Peter Evanschitzky, Gerardo Bottiglieri, Tim Brunner, Eelco van Setten, Claire van Lare, Mark van de Kerkhof
- **연도**: 2024
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 24, Issue 1, 011002 (October 8, 2024)
- **DOI/URL**: https://doi.org/10.1117/1.JMM.24.1.011002

## 핵심 요약
High-NA EUV 리소그래피에서 3D 마스크 효과(M3D)로 인한 회절 효율 저하와 대비도 페이딩(contrast fading) 문제를 해결하기 위해 분할 동공(split pupil) 이중 노출 기법을 연구한다. 시뮬레이션을 통해 다양한 피치, 마스크 흡수층, 소스 충진(source filling)에서 분할 동공 노출의 적용 가능성을 체계적으로 분석한다.

## 주요 기여
1. **Split Pupil 기법 체계화**: 라인-스페이스 패턴 너머 접촉 배열까지 확장 가능성 입증
2. **M3D 효과 완화**: 분할 동공 노출로 이미지 블러 및 피치 간 최적 초점 이동 동시 보상
3. **Low-n/low-k 흡수층 최적 조합 발견**: 분할 동공 + 저굴절률 흡수층에서 최상의 이미징 성능
4. **명시야/암시야 마스크 비교**: 다양한 마스크 흡수층 옵션에서 분할 동공 효과 정량 분석

## 알고리즘/수식
### Split Pupil(이중 모노폴) 노출 원리
```
이미지 = 노출_1(동공 좌반부) + 노출_2(동공 우반부)

각 노출에서:
- 조명 소스는 동공의 절반만 활성화 (비대칭 조명)
- 마스크의 회절 차수가 각 노출에서 다른 방향으로 집광
- 두 이미지의 인코히런트 합산으로 최종 이미지 형성

장점:
- M3D에 의한 피치 의존적 best-focus 이동 보상
- 대비도 페이딩 완화
- 서로 다른 피치 간 동시 최적 초점 달성
```

### 성능 메트릭
- NILS(Normalized Image Log-Slope): 이미지 대비 척도
- Best Focus Shift: 피치 간 최적 초점 위치 차이
- Contrast Fading: M3D로 인한 이미지 대비 손실률

### 최적 조합
- Low-n/low-k 흡수층 + Split pupil: 단일 표준 흡수층 대비 성능 우수
- 명시야 마스크(light field mask)에서 특히 효과적

## OPC 툴 SMO 구현 관련성
- High-NA EUV(0.55NA) SMO에서 소스 분할 노출 전략 고려 필요
- 단일 소스 최적화가 아닌 이중 노출 소스 쌍(split pupil pair) 공동 최적화
- M3D 보상 목적의 SMO에서 동공 비대칭 소스 활용 가능성
- 비용 함수: 두 노출의 인코히런트 합산 이미지에 대한 EPE/CD 최적화

## 태그
`SMO`, `EUV`, `high_NA`, `split_pupil`, `dual_monopole`, `M3D`, `mask_3D_effects`, `0.55NA`, `resolution_enhancement`, `SPIE`
