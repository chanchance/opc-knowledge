# ILT Optimization of EUV Masks for Sub-7nm Lithography

## 메타데이터
- **저자**: Kevin Hooker, Bernd Kuechler, Aram Kazarian, Guangming Xiao, Kevin Lucas
- **연도**: 2017
- **게재지**: Proc. SPIE 10446, 33rd European Mask and Lithography Conference (28 September 2017)
- **DOI/URL**: https://doi.org/10.1117/12.2279912

## 핵심 요약
ILT(Inverse Lithography Technology)를 EUV 리소그래피에 최초로 적용한 연구. 기존 EUV OPC/RET 방법 대비 ILT의 장점을 특성화하고, 0.33NA EUV에서 16nm L/S 완전 랜덤 로직 메탈 패턴과 40nm 피치 랜덤 로직 직사각형 콘택트 패터닝에서 ILT가 공정 창 개선, 2D CD 제어 향상, 해상도 향상, DPT 도입 지연에 기여함을 시연한다.

## 주요 기여
1. **EUV ILT 최초 적용**: ILT를 EUV 리소그래피에 처음으로 적용하여 기존 EUV OPC/RET 대비 정량적 이득 시연
2. **해상도 향상**: 단일 노출 디바이스 레이어 해상도를 ~10% 타이트하게 개선 (DPT 회피 가능)
3. **2D CD 제어 향상**: 복잡한 2D 패턴에서 ILT의 공정 창 및 CD 균일성 개선
4. **비용 절감 잠재력**: DPT 없이 단일 노출로 해결 가능해 공정 복잡도 및 비용 절감

## 알고리즘/수식
### EUV ILT 프레임워크
```
목적함수 최소화:
min_{M} ||I_sim(M, S) - I_target||² + λ·R(M)

여기서:
- M: 마스크 패턴 (EUV 반사형 마스크)
- S: EUV 조명 소스
- I_sim: EUV 이미징 시뮬레이션 (M3D 효과 포함)
- I_target: 목표 웨이퍼 이미지
- R(M): 마스크 제조 가능성 정규화항
```

### EUV ILT 특수 고려사항
- 반사형 마스크: 투과형 193i와 달리 EUV는 반사식 → 그림자 효과(shadowing) 처리 필요
- M3D(Mask 3D) 효과: EUV 마스크의 3D 전자기 효과를 ILT 비용 함수에 통합
- 곡선형(curvilinear) 마스크 패턴: e-beam 마스크 라이팅을 활용한 비-맨해튼 패턴 허용

### 타겟 패턴
- 16nm L/S 완전 랜덤 로직 메탈
- 40nm 피치 랜덤 로직 직사각형 콘택트
- 0.33NA EUV 조건

## OPC 툴 SMO 구현 관련성
- EUV OPC 모듈에서 ILT로의 전환 필요성과 근거 제공
- SMO와 ILT의 결합: 소스 최적화 + 역 리소그래피 마스크 합성 통합 방향
- 곡선형 마스크 지원: SKOPC 마스크 합성 모듈의 비-맨해튼 패턴 지원 필요성
- EUV M3D 효과를 ILT 비용 함수에 포함하는 방법론 제시

## 태그
`ILT`, `EUV`, `OPC`, `RET`, `curvilinear_mask`, `sub7nm`, `0.33NA`, `process_window`, `DPT`, `SPIE`
