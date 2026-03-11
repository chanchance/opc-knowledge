# Resist Toploss Modeling for OPC Applications

## 메타데이터
- **저자**: Christian Zuniga, Yunfei Deng
- **연도**: 2014
- **게재지**: Proc. SPIE 9052, Optical Microlithography XXVII, 905227
- **DOI/URL**: https://doi.org/10.1117/12.2048124

## 핵심 요약
32nm 노드 이하에서 레지스트 손실(toploss)이 증가하여 패턴이 에칭 실패에 취약해지는 문제를 OPC 모델로 다룬다. Calibre CM1 레지스트 모델을 활용하여 광학 이미지 평면 선택으로 레지스트 손실을 결정하고, 풀칩에서 toploss 핫스팟을 식별·보정한다.

## 주요 기여
1. 레지스트 높이(Z) 방향 손실(toploss)을 OPC 컴팩트 모델로 처리하는 방법론
2. Calibre CM1 모델의 광학 이미지 평면 선택으로 레지스트 손실 결정 기법
3. 풀칩 스케일에서 toploss 핫스팟 식별 방법
4. 레지스트 손실 패턴의 OPC 보정 가능성 시연
5. 2D 컨투어만 다루는 기존 OPC 모델의 한계를 3D 프로파일로 확장

## 모델 수식/아키텍처
- **Toploss 모델**: 레지스트 높이 H(x,y) 분포를 CM1 모델로 예측
  - 여러 Z 평면에서 공중 이미지 I(x,y,z) 계산
  - 각 Z에서 CD 컨투어 추출 → 3D 레지스트 프로파일 재구성
  - Toploss = H_nominal - H_simulated
- CM1 파라미터: σ_X, σ_Y (가로/세로 확산), n (대비), t_r (임계값)
- 풀칩 적용: 레지스트 두께 마진이 작은 핫스팟 패턴 자동 탐지

## 모델 유형
- [x] 광학
- [x] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC 레지스트 모델에 Z방향 toploss 계산 기능 추가 시 직접 참조
- OPC 검증(verification) 단계에서 toploss 핫스팟 감지 규칙 구현에 활용
- 에치 후 패턴 실패와 레지스트 toploss의 상관관계 모델링
- `2014_Zavyalova_CombiningLithoEtch_OPC.md`와 함께 3D OPC 모델 시리즈

## 태그
`Model`, `Resist`, `Toploss`, `3D`, `OPC`, `Hotspot`, `Calibre`, `CM1`, `SPIE`
