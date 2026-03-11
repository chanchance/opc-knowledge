# Lithography Hotspot Correction on Post-OPC Layout Using Generative Adversarial Networks

## 메타데이터
- **저자**: Weilun Ciou, Tony Hu, Fz Cheng, Y. Y. Tsai, Terry Hsuan, Elvis Yang, T. H. Yang, K. C. Chen
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124951Y
- **DOI/URL**: https://doi.org/10.1117/12.2654456

## 핵심 요약
Post-OPC 레이아웃에서 리소그래피 hotspot을 GAN(Generative Adversarial Network)으로 직접 보정하는 방법론을 제안한 논문. GAN이 hotspot 패턴의 형상을 수정하는 마스크 레이아웃 변환을 학습함으로써, OPC 재실행 없이 hotspot을 직접 교정하고 리소그래픽 인쇄 품질을 개선하였다.

## 주요 기여
1. **GAN 기반 Post-OPC Hotspot 보정**: GAN이 hotspot 패턴 형상을 직접 수정하는 레이아웃 변환을 학습하여 OPC 재실행 없이 hotspot 교정
2. **레이아웃 형상 자동 수정**: hotspot 영역의 마스크 레이아웃 형상을 GAN이 자동으로 재생성(generate)하여 교정 패턴 제안
3. **리소그래픽 인쇄 개선**: GAN 보정 후 웨이퍼 인쇄 시뮬레이션 결과로 hotspot 해소 및 EPE 개선 확인
4. **OPC 엔지니어링 효율화**: 전체 OPC 재실행 대신 GAN 기반 hotspot 국소 보정으로 처리 시간 단축
5. **End-to-End 학습**: hotspot 입력 패턴에서 보정 패턴 출력까지 end-to-end 학습 방식

## 검증 방법론
- GAN 훈련 데이터: 알려진 hotspot 패턴과 수동/자동 보정 패턴 쌍(pair)
- GAN 보정 패턴을 리소그래피 시뮬레이터로 재시뮬레이션하여 hotspot 해소 여부 확인
- EPE 분포 비교: GAN 보정 전후
- 처리 시간 비교: GAN 보정 vs. 전통적 OPC 재실행

## OPC 툴 구현 관련성
- SKOPC의 post-OPC hotspot 자동 보정 기능에서 GAN 기반 접근법 도입 시 참조
- `2020_Falch_hotspot_library_manufacturing_OPC_flow.md`의 레시피 기반 hotspot 보정과 비교하여 GAN 방식의 장단점 평가
- `2022_Lin_OPC_optimization_hotspot_pattern_diffing.md`과 결합하면 pattern diffing으로 신규 hotspot 발견 → GAN으로 자동 보정하는 통합 파이프라인 구성 가능
- SKOPC의 hotspot auto-fix 모듈 설계에서 규칙 기반, 라이브러리 기반, GAN 기반 방식의 비교 기준

## 태그
`Verification`, `SPIE`, `GAN`, `Hotspot`, `Post-OPC`, `Deep Learning`, `Layout Correction`, `EPE`, `OPC`
