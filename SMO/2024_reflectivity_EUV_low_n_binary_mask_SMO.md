# The Influence of Reflectivity on EUV Lithography Performance of Low-n and Binary Masks for Random Logic Via Implementation

## 메타데이터
- **저자**: (상세 저자 정보 SPIE 13216)
- **연도**: 2024
- **게재지**: Proc. SPIE 13216, International Conference on Extreme Ultraviolet Lithography 2024 (22 November 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3034348

## 핵심 요약
EUV 리소그래피 성능에 대한 마스크 흡수층 반사율의 영향을 저굴절률(low-n) 및 이진(binary) 마스크를 대상으로 랜덤 로직 비아 구현 관점에서 분석한다. 필름 두께, 굴절률, 소멸 계수 변화에 따른 성능을 SMO, OPC, SRAF를 포함한 해상도 향상 기술로 평가한다.

## 주요 기여
1. **반사율-성능 상관관계**: 마스크 반사율이 EUV 이미징 성능에 미치는 영향 정량화
2. **low-n vs binary 마스크 비교**: 저굴절률 대안 흡수층과 이진 마스크의 로직 비아 성능 비교
3. **SMO+OPC+SRAF 통합 분석**: 해상도 향상 기술 조합에서 마스크 재료 효과 평가
4. **흡수층 파라미터 공간 탐색**: 두께, n, k 변화에 따른 체계적 성능 맵핑

## 알고리즘/수식
### 마스크 성능 평가 프레임워크
```
평가 파라미터:
- 흡수층 두께 t: 30-80nm 범위
- 굴절률 n: low-n 재료 (n < 0.9 at 13.5nm)
- 소멸 계수 k: 흡수 특성 결정

평가 메트릭 (SMO + OPC + SRAF 포함):
- NILS(Normalized Image Log-Slope): 이미지 대비
- DOF(Depth of Focus): 초점 허용 범위
- EPE(Edge Placement Error): 엣지 배치 정확도
- MEEF(Mask Error Enhancement Factor): 마스크 오차 증배

EUV 마스크 반사율:
R_mask = R_ML × (1 - A_abs)²
여기서:
- R_ML: 다층 반사경 반사율 (~70%)
- A_abs: 흡수층 흡광도
```

### 타겟 패턴
- 랜덤 로직 비아 레이어
- 0.33NA EUV (현재 세대 스캐너)
- 고NA EUV(0.55NA) 예비 분석 포함

## OPC 툴 SMO 구현 관련성
- EUV 마스크 재료 데이터베이스: SMO에서 다양한 흡수층 옵션의 n, k 값 참조 필요
- SMO 비용 함수에 반사율 의존 M3D 효과 통합
- low-n 마스크의 SMO 최적 소스 형상: 기존 TaBN과 다름
- SKOPC에서 마스크 재료 파라미터를 SMO 입력으로 수용하는 인터페이스 설계 참조

## 태그
`SMO`, `OPC`, `EUV`, `mask_absorber`, `low_n_mask`, `binary_mask`, `reflectivity`, `SRAF`, `via_patterning`, `M3D`, `SPIE`
