# An Integrated Verification Flow for Curvilinear Mask

## 메타데이터
- **저자**: Shuling Wang, Shumay Shang, Sagar Saxena, Xima Zhang, George Lippincott, Le Hong, John L. Sturtevant
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 1295415
- **DOI/URL**: https://doi.org/10.1117/12.3010925

## 핵심 요약
멀티빔 마스크 라이터(MBMW) 발전으로 커비리니어 마스크 양산이 현실화된 시점에서, 커비리니어 OPC 마스크에 대한 완전 통합 검증 플로우를 제안한 논문. 복잡한 마스크 형상과 대용량 데이터라는 두 가지 핵심 도전을 해결하기 위해 MRC(Mask Rule Check) 규칙 체계와 검증 자동화 파이프라인을 제시하였다.

## 주요 기여
1. **완전 통합 커비리니어 검증 플로우**: OPC 출력에서 마스크 제조까지 End-to-End 검증 파이프라인 구성
2. **커비리니어 전용 MRC 규칙 체계**: 맨해튼 MRC와 구분되는 커비리니어 고유 마스크 규칙 정의 및 분류
3. **3가지 핵심 OPC 개선 사항 통합**:
   - 노치(notch) 제거 및 덜 공격적인 코너 세리프 조정 기반 마스크 충실도 인식 OPC 리타게팅 전략
   - ABBA형 비대칭 L/S 어레이의 패턴 붕괴 완화를 위한 Pitch Walking 방법
   - T2T(Tip-to-Tip) 패턴 강인성 개선을 위한 특화 리타게팅 방법
4. **대용량 데이터 처리 효율화**: 커비리니어 데이터의 용량 문제를 고려한 검증 알고리즘 최적화
5. **MBMW 시대 산업 표준 검증 플로우**: 양산 환경에 적용 가능한 실용적 커비리니어 마스크 검증 워크플로우

## 검증 방법론
- 커비리니어 OPC 출력물에 대한 MRC 규칙 위반 감지 정확도 및 처리 시간 측정
- 맨해튼 MRC 대비 커비리니어 전용 MRC의 false positive/negative 비율 비교
- 3가지 개선 전략 적용 전후 웨이퍼 프린터빌리티(printability) 메트릭 비교
- Pitch Walking 보정 효과: ABBA 패턴 CD 균일도(LCDU) 개선 정량화
- T2T 패턴 EPE 분포 개선량 정량 비교

## OPC 툴 구현 관련성
- SKOPC의 ILT/커비리니어 OPC 후처리 및 마스크 검증 모듈 설계의 핵심 참조
- `2023_Kato_verification_methods_curvilinear_geometries.md`의 실용화 버전으로, SKOPC 구현 단계에서 우선 참조
- `2025_Yi_Bspline_curvilinear_mask_ILT_optimization.md`과 연계하여 ILT→검증 통합 파이프라인 구성
- SKOPC MDP(Mask Data Preparation) 모듈의 커비리니어 지원 추가 시 MRC 규칙 기준으로 활용
- Pitch Walking 보정 알고리즘은 SKOPC Rule OPC 모듈의 ABBA 패턴 처리에 참조 가능

## 태그
`Verification`, `SPIE`, `Curvilinear`, `MRC`, `ILT`, `OPC`, `MBMW`, `Mask Data`, `Pitch Walking`, `T2T`
