# Hybrid OPC Modeling with SEM Contour Technique for 10nm Node Process

## 메타데이터
- **저자**: Keiichiro Hitomi, Scott Halle, Marshal Miller, Ioana Graur, Nicole Saulnier, Derren Dunn, Nobuhiro Okai, Shoji Hotta, Atsuko Yamaguchi, Hitoshi Komuro, Toru Ishimoto, Shunsuke Koshihara, Yutaka Hojo
- **연도**: 2014
- **게재지**: Proc. SPIE 9052, Optical Microlithography XXVII
- **DOI/URL**: https://doi.org/10.1117/12.2047678
- **인용수**: ~40

## 핵심 요약
10nm 노드 공정을 위한 하이브리드 OPC 모델 캘리브레이션 방법을 제시한다. 1D/단순 2D 구조에서 CD를 측정하는 전통 방법과, 복잡한 2D 구조에서 CD-SEM 컨투어를 추출하는 방법을 결합하여 OPC 모델 정확도를 향상시킨다. 컨택 레이어에서 23%, 메탈 레이어에서 18% RMS EPE 개선을 달성하며, 컨투어 수축(shrink) 보정이 모델의 정확도와 안정성을 크게 높인다.

## 주요 기여
1. 1D CD + 2D SEM 컨투어를 결합한 하이브리드 OPC 모델 캘리브레이션
2. 컨택 레이어 23%, 메탈 레이어 18% RMS EPE 개선
3. SEM 컨투어 수축 보정(shrink correction)으로 모델 정확도 및 안정성 향상
4. 10nm 노드 복잡한 2D 패턴을 위한 SEM 컨투어 기반 캘리브레이션 방법론 확립

## Recipe/Process Flow 상세

### 하이브리드 캘리브레이션의 필요성
```
전통적 OPC 모델 캘리브레이션:
  데이터: 1D 게이지 (라인/공간) + 간단한 2D 게이지 (코너, 엔드캡)
  측정: CD-SEM으로 선폭(CD) 측정 (단일 수치)
  한계:
    10nm 이하 노드에서 2D 근접 효과 심화
    단일 CD로 복잡한 2D 패턴 형상 정보 불충분
    컨택, 비아 레이어: 2D 형상이 CD보다 중요

SEM 컨투어 기반 캘리브레이션:
  데이터: 복잡한 2D 구조의 SEM 이미지 → 컨투어 추출
  측정: 전체 2D 윤곽선 정보 (수십~수백 계측점/패턴)
  장점: 2D 형상 완전 포착 → 복잡한 2D 근접 효과 학습

하이브리드 접근:
  1D/단순 2D: 전통 CD 계측 (빠름, 많은 게이지)
  복잡한 2D: SEM 컨투어 계측 (느림, 소수 게이지)
  결합: 보완적 정보로 모델 정확도 최대화
```

### SEM 컨투어 추출 및 처리
```
SEM 이미지 취득:
  고해상도 CD-SEM (임계 치수 계측 목적)
  복잡한 2D 패턴: 컨택 홀 어레이, 메탈 배선 2D 조합

컨투어 추출 알고리즘:
  방법: 임계값 기반 윤곽선 추출 (SEM 그레이레벨 → 이진 경계)
  결과: 패턴 경계의 (x,y) 좌표 리스트

SEM 수축(Shrink) 보정:
  문제: CD-SEM 전자빔 조사 → SEM 수축(shrink) 현상
    레지스트/패턴이 전자빔으로 수축 → CD 과소 측정
    복잡한 2D 컨투어에서 특히 심각
  수축 보정:
    반복 SEM 측정으로 수축량 정량화
    컨투어 좌표에 수축 보정 오프셋 적용
  효과:
    수축 보정 후: 모델 정확도 + 안정성 향상
    다수 캘리브레이션 런 간 편차 감소
```

### 하이브리드 모델 캘리브레이션 흐름
```
1단계: 게이지 수집
  A. 1D/2D 전통 게이지:
     라인/공간/피치 배열 (다양한 CD, pitch)
     단순 2D (고립 끝단, 코너, 코너-코너)
     측정: CD-SEM으로 단일 CD 수치
  B. 복잡한 2D 컨투어 게이지:
     컨택 홀 어레이, 복잡한 메탈 배선 패턴
     측정: SEM 이미지 → 컨투어 추출 → 수축 보정

2단계: 모델 파라미터 최적화
  Hopkins 광학 모델 + 레지스트 모델
  비용 함수:
    C = Σ_1D (CD_sim - CD_meas)² + λ × Σ_2D ||contour_sim - contour_meas||²
  최적화: 경사하강법 또는 Levenberg-Marquardt

3단계: 검증
  훈련 세트: 위 하이브리드 게이지
  검증 세트: 독립 패턴 (훈련에 미사용)
  지표: RMS EPE (시뮬 CD/컨투어 vs. 실측)
```

### 성능 결과
```
RMS EPE 개선 (전통 방법 대비):
  컨택 레이어: 23% RMS EPE 감소
  메탈 레이어: 18% RMS EPE 감소

모델 안정성:
  8회 독립 캘리브레이션 런 편차:
    수축 보정 미적용: 런마다 EPE 편차 큼
    수축 보정 적용: 편차 크게 감소 → 안정적 모델

패턴 타입별 개선:
  복잡한 2D 컨택/비아 패턴: 가장 큰 개선
  단순 1D 패턴: 개선 미미 (이미 정확)
  2D 코너/엔드캡: 중간 수준 개선
```

## OPC 툴 구현 관련성
- **SKOPC SEM 컨투어 캘리브레이션**: `skopc/modeling/` SEM 컨투어 기반 2D OPC 모델 캘리브레이션
- **컨투어 처리**: SEM 이미지 → 컨투어 추출 → 수축 보정 파이프라인
- **하이브리드 비용 함수**: 1D CD + 2D 컨투어 혼합 최적화 목적함수
- **모델 안정성 검증**: 다수 캘리브레이션 런 편차 분석으로 모델 품질 평가

## 참고문헌
- Proc. SPIE 9052, Optical Microlithography XXVII (2014)
- 저자 소속: IBM + GlobalFoundries
- 관련: SEM contour-based OPC calibration through PW (SPIE 6518, 2007)
- 관련: Weighting for SEM contour OPC model quality (SPIE 8326, 2012)
- 관련: Accurate etch modeling with massive metrology (SPIE 11327, 2020)

## 태그
`Recipe`, `SPIE`, `OPC-ModelCalibration`, `SEMContour`, `HybridCalibration`, `2DPattern`, `ShrinkCorrection`, `IBM`, `10nm`, `ContactLayer`, `MetalLayer`, `2014`
