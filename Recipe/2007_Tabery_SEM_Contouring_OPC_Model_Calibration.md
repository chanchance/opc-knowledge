# SEM Image Contouring for OPC Model Calibration and Verification

## 메타데이터
- **저자**: Cyrus Tabery, Hidetoshi Morokuma, Ryoichi Matsuoka, Lorena Page, George E. Bailey, Ir Kusnadi, Thuy Do
- **연도**: 2007
- **게재지**: Proc. SPIE 6520, Optical Microlithography XX, 652019
- **DOI/URL**: https://doi.org/10.1117/12.714389
- **인용수**: ~80

## 핵심 요약
최첨단 OPC 및 설계 검증을 위한 리소그래피 모델은 전통적으로 CD-SEM의 1차원 측정값으로 캘리브레이션되어 왔다. 본 논문은 설계 기반 계측 시스템(design-based metrology) 내에서 대량의 SEM 이미지를 윤곽 추출(contouring)하여 2D 측정으로 활용하는 새로운 방법을 제시한다. 45nm 액침 리소그래피에서 전통적 1D 캘리브레이션과 하이브리드 1D+SEM 윤곽 캘리브레이션의 모델 정확도를 비교한다.

## 주요 기여
1. 대량 SEM 이미지 윤곽 추출을 통한 2D OPC 모델 캘리브레이션 방법론
2. Line-end, bar-to-bar, bar-to-line 등 2D 근접 피처 완전 특성화
3. 1D 캘리브레이션 vs. 하이브리드(1D+SEM 윤곽) 캘리브레이션 정확도 비교
4. 설계 기반 계측 시스템(design-based metrology)과 OPC 모델 캘리브레이션 통합

## Recipe/Process Flow 상세

### OPC 모델 캘리브레이션 흐름 (전통 vs. SEM 윤곽 기반)
```
전통적 1D 캘리브레이션:
1. 캘리브레이션 패턴 레이아웃 설계
   - 1D 라인-스페이스 (다양한 pitch, CD)
   - 측정 용이성 위주 패턴 선택
2. CD-SEM 측정
   - 각 패턴의 1D CD 측정 (선폭)
   - 수백~수천 측정 포인트
3. 모델 파라미터 최적화
   - 측정 CD vs. 모델 예측 CD 최소 자승 맞춤
   - 주로 1D 구조에서 우수한 정확도

한계: 2D 피처(line-end, corner, 2D 근접)의 부분적 특성화만 가능
```

```
SEM 윤곽 기반 2D 캘리브레이션:
1. 대량 SEM 이미지 획득
   - 설계 기반 계측으로 2D 패턴 SEM 이미지 자동 취득
   - Line-end, L-자형, bar-to-bar 등 2D 구조 포함
   - 동일 패턴 다수 이미지로 노이즈 평균화

2. SEM 이미지 윤곽 추출
   - 이진화 및 에지 검출로 인쇄 윤곽 추출
   - 서브픽셀 정확도 윤곽 위치 결정
   - 포지션 대응: 설계 레이아웃 ↔ SEM 윤곽

3. 2D 캘리브레이션 데이터 생성
   - 각 윤곽 포인트에서 (설계 위치, 인쇄 위치) 쌍
   - 수만 개의 2D 측정 포인트
   - 1D CD 측정보다 훨씬 풍부한 데이터

4. 하이브리드 모델 캘리브레이션
   - 1D 측정값 + 2D SEM 윤곽 데이터 결합
   - 2D 근접 효과 정확히 포착
   - RMS 오차 감소
```

### 45nm 액침 리소그래피 결과
```
비교 대상:
  A) 1D 캘리브레이션만 사용
  B) 하이브리드 (1D + SEM 윤곽 데이터)

결과:
  1D 패턴 정확도: A ≈ B (유사)
  2D 패턴 정확도: B >> A (SEM 윤곽이 결정적)
  전체 RMS EPE: B가 현저히 낮음
  Line-end 단축(pullback): B에서 훨씬 정확히 예측
```

## OPC 툴 구현 관련성
- **SKOPC 모델 캘리브레이션**: `skopc/modeling/` 내 OPC 모델 캘리브레이션 파이프라인에 SEM 윤곽 데이터 활용 참조
- **2D 측정 데이터**: SEM 윤곽 기반 EPE 측정은 `skopc/modeling/gnn/` GNN 훈련 데이터 생성에도 활용 가능
- **모델 정확도**: 2D 피처 포함 캘리브레이션으로 GAN-OPC, GNN-OPC 등 ML 모델의 학습 데이터 품질 향상
- **설계 기반 계측**: SegSEM(2026_Chen_SegSEM)과 같은 최신 SEM 윤곽 추출 기술의 이론적 배경

## 참고문헌
- Proc. SPIE 6520, Optical Microlithography XX (2007)
- 관련: Realizing more accurate OPC models by utilizing SEM contours (SPIE, 2020)
- 관련: Enabling SEM contour-based OPC models (JM3, 2015)
- 관련: SegSEM: Enabling SAM2 for SEM Contour Extraction (2026)

## 태그
`Recipe`, `SPIE`, `ModelCalibration`, `SEM-Contouring`, `2D-Calibration`, `OPC-Model`, `DesignBasedMetrology`, `45nm`, `ImmersionLithography`, `Hybrid`
