# Pattern Selection Strategy by Clustering for Logic EPE Monitoring

## 메타데이터
- **저자**: Roy Anunciado, Konstantin Nechaev, Reza Sahraeian, Jeroen Schouwenberg, Guillaume Schelcher, Shubhankar Das, Wei Peng, Stefan van der Sanden, Harm Dillen
- **연도**: 2024
- **게재지**: Proc. SPIE 13215, International Conference on Extreme Ultraviolet Lithography 2024, 1321508
- **DOI/URL**: https://doi.org/10.1117/12.3034649

## 핵심 요약
로직 EPE 모니터링을 위한 시뮬레이션 기반 패턴 클러스터링 방법론을 개발한 논문. 기하학적 설계와 패턴의 이미징 거동을 함께 고려하여 유사한 EPE 거동을 가진 피처들을 식별하고 분류하는 클러스터링 기법을 제시한다. EPE 모니터링을 위한 대표 패턴 선택 전략을 자동화하여 측정 효율성을 높이면서도 다양한 EPE 거동 모드를 포괄적으로 커버한다.

## 주요 기여
1. **시뮬레이션 기반 패턴 클러스터링**: 기하학적 + 이미징 거동을 함께 고려한 패턴 분류
2. 유사 EPE 거동 패턴 자동 식별 및 대표 패턴 선택 전략
3. 로직 레이어 EPE 모니터링을 위한 효율적 패턴 샘플링 방법
4. EUV 리소그래피 환경에서 인라인 EPE 모니터링 패턴 셋 최적화
5. 클러스터 기반 접근으로 측정 커버리지와 효율성의 균형 달성

## 검증 방법론
- **방법론**: 시뮬레이션 기반 패턴 클러스터링
- **클러스터링 기준**: 기하학적 설계 특성 + 이미징 거동 (EPE 민감도)
- **적용 대상**: 로직 레이어 EPE 모니터링 패턴 선택
- **EUV 환경**: EUV 리소그래피 컨텍스트
- **평가**: 클러스터별 대표 패턴 선택의 EPE 거동 커버리지 검증

## OPC 툴 구현 관련성
- OPC 모델 캘리브레이션 및 검증을 위한 패턴 샘플링 전략 자동화에 직접 적용 가능
- 대규모 로직 레이아웃에서 EPE 모니터링 게이지(gauge) 선택의 클러스터링 접근법
- OPC 검증 후 인라인 EPE 모니터링 패턴 셋 구성에 클러스터링 방법 통합 방법
- 기하학적 유사성과 이미징 유사성을 모두 반영한 OPC 테스트 패턴 선택 프레임워크

## 태그
`Verification`, `EPE`, `EPEMonitoring`, `PatternClustering`, `EUV`, `Logic`, `PatternSelection`, `InlineMonitoring`, `SPIE`, `EUVL`, `2024`
