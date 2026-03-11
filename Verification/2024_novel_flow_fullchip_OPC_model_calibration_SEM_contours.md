# A Novel Flow of Full-Chip OPC Model Calibration and Verification by Utilizing SEM Image Contours

## 메타데이터
- **저자**: (저자명 미확인 - SPIE 12954 수록)
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III
- **DOI/URL**: https://doi.org/10.1117/12.3010034

## 핵심 요약
기존 CD(Critical Dimension) 기반 모델 캘리브레이션의 한계를 극복하기 위해 SEM 이미지 컨투어(contour)를 활용한 새로운 풀칩 OPC 모델 캘리브레이션 및 검증 플로우를 제안한다. 컨투어 기반 접근법은 CD 측정값보다 훨씬 많은 엣지 정보를 활용해 모델 정확도를 크게 향상시킨다.

## 주요 기여
1. **컨투어 기반 캘리브레이션 플로우**: SEM 이미지에서 추출한 컨투어를 OPC 모델 캘리브레이션 게이지로 직접 활용하는 혁신적인 플로우 제안
2. **고밀도 게이지 적용**: 10K 이상의 컨투어 기반 엣지 배치 게이지(edge placement gauge)를 사용해 오버피팅 문제 해결
3. **모델 정확도 향상**: 전통적인 CD 기반 방법 대비 >47% 향상된 모델 정확도를 1,400개 이상의 검증 게이지에서 확인
4. **풀칩 검증 통합**: 캘리브레이션과 검증을 단일 플로우로 통합하여 사이클 타임 단축

## 검증 방법론
- SEM 이미지 컨투어 추출 후 CD-SEM 측정값 대비 검증
- 컨투어-to-컨투어 정렬 및 EPE(Edge Placement Error) 측정
- 1,400개 이상의 독립 검증 게이지로 모델 정확도 평가
- 기존 CD 기반 방법과 정량적 비교 (>47% 정확도 향상 확인)

## OPC 툴 구현 관련성
- OPC 모델 캘리브레이션 엔진에서 컨투어 기반 입력 처리 기능 필요
- SEM 컨투어 추출 및 정렬 알고리즘을 모델링 모듈에 통합 가능
- EPE 계산 루틴을 컨투어 형식으로 확장하면 검증 정확도 향상
- `skopc/modeling/` 내 모델 캘리브레이션 파이프라인과 직접 연관

## 태그
`Verification`, `SPIE`, `OPC_Model_Calibration`, `SEM_Contour`, `Full_Chip`, `EPE`, `2024`
