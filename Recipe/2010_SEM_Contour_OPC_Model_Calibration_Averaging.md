# Alignment and Averaging of SEM Image Contours for OPC Modeling Purposes

## 메타데이터
- **저자**: (JM3 2010 - Journal of Micro/Nanolithography)
- **연도**: 2010
- **게재지**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 9, Issue 4, 041302
- **DOI/URL**: https://doi.org/10.1117/1.3514704
- **인용수**: ~35

## 핵심 요약
OPC 모델 캘리브레이션을 위한 SEM(Scanning Electron Microscope) 이미지 기반 윤곽선(contour) 추출 및 정렬/평균화 방법론을 제시한다. 기존 1D CD-SEM 측정만으로는 서브-65nm 이하 노드의 복잡한 2D 패턴 OPC 모델 캘리브레이션에 충분하지 않다는 점에서, SEM 이미지 전체 윤곽선 정보를 OPC 모델 캘리브레이션에 활용하는 체계적 방법을 개발한다. 정렬/평균화를 통해 SEM 노이즈를 줄이고 신뢰성 있는 2D 윤곽선 데이터를 확보한다.

## 주요 기여
1. SEM 이미지 윤곽선 추출 및 다중 이미지 정렬/평균화 알고리즘
2. 1D CD-SEM 측정의 한계를 극복하는 2D 윤곽선 기반 OPC 모델 캘리브레이션
3. 임의 2D 구조(수평+수직 엣지 혼합)에 대한 확장된 정렬 기법
4. Calibre Workbench OPC 모델 캘리브레이션 흐름에 통합

## Recipe/Process Flow 상세

### SEM 윤곽선 기반 OPC 캘리브레이션의 동기
```
기존 1D CD-SEM 측정의 한계:
  측정 데이터: 단일 위치에서 선폭(CD) 값만
  → OPC 모델: 1D 선/공간에 최적화
  → 2D 패턴(코너, 끝단, T-junction): 정확도 부족

2D 패턴의 중요성:
  65nm 이하 노드: 2D 효과(코너 라운딩, 끝단 단축) 증가
  회로 성능에 직접 영향:
    코너 라운딩 → PMOS/NMOS 전류 비대칭
    끝단 단축 → 컨택 오버랩 감소

SEM 윤곽선의 장점:
  - 전체 패턴 형상 정보 포함 (2D)
  - 코너, 끝단, 복잡한 구조 캘리브레이션 가능
  - 동일 SEM 데이터에서 다수 캘리브레이션 포인트 추출
```

### SEM 이미지 윤곽선 추출 및 처리
```
1단계: SEM 이미지 취득
  - 동일 패턴의 다수 SEM 이미지 수집 (노이즈 평균화)
  - 대표 패턴: 1D 선/공간 + 2D 코너 + 끝단

2단계: 윤곽선 추출 (Contouring)
  - SEM 이미지에서 레지스트 경계 윤곽선 추출
  - 방법: 임계값(threshold) 기반 엣지 감지
  - 결과: 픽셀 단위 경계선 좌표 집합

3단계: 정렬 (Alignment)
  문제: 다수 SEM 이미지 간 패턴 위치/방향 미세 차이
  해결:
    - 기준 이미지(reference) 선택
    - 각 이미지의 윤곽선을 기준에 정렬
    - 1D 구조: 단순 평행 이동 정렬
    - 2D 구조(수평+수직 엣지 혼합):
        Fine SEM Edge (FSE) 방법: 각 엣지 방향별 분리 정렬

4단계: 평균화 (Averaging)
  - 정렬된 N개 윤곽선 평균 계산
  - 픽셀별 좌표 평균 → SEM 노이즈 감소 (√N 분의 1)
  - 결과: 신뢰도 높은 평균 윤곽선
```

### OPC 모델 캘리브레이션 통합
```
윤곽선 기반 캘리브레이션 데이터:
  전통 1D: (패턴, CD 값) 쌍 → 캘리브레이션 포인트
  윤곽선 기반: (패턴, 2D 윤곽선) → 수십~수백 포인트/패턴

캘리브레이션 과정:
  1. OPC 모델 시뮬레이션 → 예측 2D 윤곽선
  2. 예측 윤곽선 vs. SEM 평균 윤곽선 비교
  3. 법선 방향 거리(EPE) 계산
  4. 모델 파라미터 최적화: RMS EPE 최소화

장점:
  - 2D 패턴 모델 정확도 향상 (코너, 끝단)
  - 더 많은 캘리브레이션 데이터 포인트 (동일 측정 비용)
  - 공정 윈도우 전반에 걸친 모델 검증 가능

Calibre Workbench 통합:
  - 산업계 표준 OPC 모델 캘리브레이션 도구
  - 윤곽선 데이터 입력 형식 표준화
  - 정렬/평균화 기능 내장
```

### 1D CD-SEM vs. 윤곽선 캘리브레이션 비교
```
데이터 품질:
  1D CD-SEM: 빠른 측정, 국소 CD만
  윤곽선: 더 많은 정보, 처리 필요

모델 정확도 (2D 패턴):
  1D CD-SEM만: RMS EPE 높음 (2D 효과 미반영)
  윤곽선 포함: RMS EPE 감소 (특히 코너/끝단)

적합 상황:
  1D 위주 설계: 1D CD-SEM 충분
  2D 패턴 많은 설계 (28nm 이하): 윤곽선 필수
```

## OPC 툴 구현 관련성
- **SKOPC 캘리브레이션 모듈**: `skopc/modeling/` SEM 윤곽선 데이터를 OPC 모델 캘리브레이션 입력으로 처리
- **2D 윤곽선 처리**: 외부 SEM 윤곽선 파일(CSV/JSON) → 캘리브레이션 게이지 자동 변환
- **EPE 계산 확장**: 기존 1D EPE에서 2D 윤곽선 기반 법선 EPE로 확장
- **모델 정확도 진단**: 1D vs. 2D 패턴별 모델 오차 분리 보고 도구

## 참고문헌
- J. Micro/Nanolith. MEMS MOEMS 9(4), 041302 (2010)
- 관련: SEM image contouring for OPC model calibration and verification (SPIE 6520, 2007)
- 관련: SEM-contour-based OPC model calibration through the process window (SPIE 6518, 2007)
- 관련: Automated sample plan selection for OPC modeling (SPIE 9052, 2014)

## 태그
`Recipe`, `SPIE`, `JM3`, `SEMContour`, `OPC-ModelCalibration`, `ImageContour`, `2D-Calibration`, `Alignment`, `Averaging`, `CalibreWorkbench`, `2010`
