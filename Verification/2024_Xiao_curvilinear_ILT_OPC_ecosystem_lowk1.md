# Advancing the Curvilinear ILT and OPC Ecosystem for Low-k1 DUV and EUV Lithography

## 메타데이터
- **저자**: Guangming Xiao, Kevin Hooker, Yunqiang Zhang, Ji Li, Thuc Dam, Yu-Po Tang, Linghui Wu, WooJoo Sim, Kevin Lucas
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 1295413
- **DOI/URL**: https://doi.org/10.1117/12.3014637

## 핵심 요약
저-k1 DUV 및 EUV 리소그래피 환경에서 커비리니어 마스크를 위한 ILT/OPC 생태계 전반의 발전 현황을 종합 보고한 논문. ILT 기반 커비리니어 마스크/타겟 생성, 곡선 기반 ILT/OPC 통합, MRC/MEC(Mask Edge Check), etch 보정, 데이터 볼륨 감소 등 커비리니어 생태계 전 영역의 최신 발전을 체계적으로 정리하였다.

## 주요 기여
1. **커비리니어 ILT/OPC 스펙트럼 솔루션**: 다양한 응용 영역(메모리, 로직, 포토닉스)의 품질 및 계산 비용 요구사항을 충족하는 다양한 커비리니어 솔루션 제시
2. **곡선 기반 통합 ILT/OPC 플로우**: 커비리니어 타겟과 마스크를 동시에 최적화하는 통합 최적화 방법론
3. **MRC/MEC 발전**: 커비리니어 형상 전용 마스크 규칙 및 엣지 검사(mask edge check) 알고리즘 최신화
4. **데이터 볼륨 감소**: 커비리니어 마스크 데이터의 대용량 문제 해결을 위한 압축/표현 방법 개선
5. **DUV-EUV 통합 적용**: 193nm DUV와 EUV 양쪽 리소그래피 환경에서의 커비리니어 OPC 적용 가이드라인

## 검증 방법론
- 여러 기술 노드(DUV 저-k1, EUV)에서 커비리니어 OPC와 맨해튼 OPC의 웨이퍼 프린터빌리티 비교
- 통합 ILT/OPC 플로우 적용 후 EPE, LCDU, 공정 윈도우 면적 비교
- MRC/MEC 규칙 기반 검증 커버리지 분석
- 데이터 볼륨 감소율 및 마스크 충실도(fidelity) 비교 정량화

## OPC 툴 구현 관련성
- SKOPC의 커비리니어 ILT/OPC 모듈 로드맵 수립 시 전체 생태계 조망 문헌으로 핵심 참조
- `2024_Wang_integrated_verification_flow_curvilinear_mask.md`와 함께 커비리니어 OPC-검증 통합 파이프라인의 쌍두 문헌
- MRC/MEC 모듈, etch 보정, 데이터 볼륨 관리까지 커비리니어 생태계 전 계층 커버
- `2025_Yi_Bspline_curvilinear_mask_ILT_optimization.md`(기수집)의 선행 생태계 정리 논문

## 태그
`Verification`, `SPIE`, `Curvilinear`, `ILT`, `OPC`, `Low-k1`, `DUV`, `EUV`, `MRC`, `MEC`, `Ecosystem`
