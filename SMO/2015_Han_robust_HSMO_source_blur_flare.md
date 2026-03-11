# Robust Hybrid Source and Mask Optimization to Lithography Source Blur and Flare

## 메타데이터
- **저자**: Chunying Han, Yanqiu Li, Xu Ma, Lihui Liu
- **연도**: 2015
- **게재지/학회**: Applied Optics, Vol. 54, No. 17, pp. 5291–5302
- **DOI/URL**: https://doi.org/10.1364/AO.54.005291
- **인용수**: 다수

## 핵심 요약
소스 블러(source blur)와 플레어(flare)가 SMO 결과로 얻은 최적 소스/마스크의 리소그래피 성능에 미치는 영향을 분석하고, 이 두 요소에 대한 에어리얼 이미지 민감도를 비용함수에 통합한 강인한 하이브리드 SMO(HSMO) 방법을 개발한다. 소스 블러·플레어 인식 HSMO로 패턴 충실도와 공정 마진을 향상시킨다.

## 주요 기여
- 소스 블러와 플레어의 민감도를 SMO 비용함수에 직접 통합
- 강인 HSMO(R-HSMO) 방법으로 소스 블러·플레어 영향 최소화
- 기존 HSMO 대비 패턴 충실도 및 공정 마진 향상 실증
- 실제 리소그래피 스캐너의 소스 비이상성을 고려한 현실적 SMO

## 알고리즘/수식
**소스 블러 모델:**
블러된 소스 $\sigma_{blur}$를 원래 소스 $\sigma$와 블러 커널 $b$의 컨볼루션으로 표현:
$$\sigma_{blur}(f,g) = \sigma(f,g) * b(f,g)$$
가우시안 블러 커널: $b(f,g) = \frac{1}{2\pi\sigma_b^2}\exp\left(-\frac{f^2+g^2}{2\sigma_b^2}\right)$

**플레어 모델:**
$$I_{flare}(x) = (1-F) \cdot I(x) + F \cdot \bar{I}$$
플레어 비율 $F$, 평균 강도 $\bar{I}$.

**강인 HSMO 비용함수:**
$$F_{robust} = F_{nominal} + \lambda_b F_{blur} + \lambda_f F_{flare}$$

**블러 민감도 항:**
$$F_{blur} = \sum_j \left(\frac{\partial I(x_j)}{\partial \sigma_b} \cdot \Delta\sigma_b\right)^2$$
소스 블러 변동 $\Delta\sigma_b$에 대한 이미지 민감도.

**플레어 민감도 항:**
$$F_{flare} = \sum_j \left(\frac{\partial I_{flare}(x_j)}{\partial F} \cdot \Delta F\right)^2 = \sum_j \left((\bar{I} - I(x_j)) \cdot \Delta F\right)^2$$

**하이브리드 HSMO 2단계:**
1. 개별 소스 최적화 (강인 비용함수 사용)
2. 동시 소스+마스크 최적화 (강인 비용함수 사용)

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 스캐너 소스 블러와 플레어 효과 통합 방법 참고
- `skopc/smo/blur_flare_robust_smo.py`에 소스 블러·플레어 인식 강인 SMO 구현
- 소스 블러 모델은 `skopc/litho/source_model.py`의 조명 시스템 모델링에 활용
- Ma et al. 2013 HSMO의 강인성 확장 버전으로 함께 참고

## 참고문헌 (핵심)
- Ma et al., "Hybrid SMO robust immersion," Applied Optics 2013
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Hashimoto et al., "Robust SMO HVM," SPIE 2013

## 태그
`SMO`, `Applied-Optics`, `robust-SMO`, `source-blur`, `flare`, `hybrid-SMO`, `HSMO`, `sensitivity`, `scanner-aberration`, `process-robustness`, `gradient-based`
