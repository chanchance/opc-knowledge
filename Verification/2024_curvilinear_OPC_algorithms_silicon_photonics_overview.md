# An Overview of Curvilinear OPC Algorithms for Silicon Photonics Applications

## 메타데이터
- **저자**: Mohamed Gheith
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540P (2024년 4월 10일)
- **DOI/URL**: https://doi.org/10.1117/12.3025295

## 핵심 요약
실리콘 포토닉스 기술이 고볼륨 제조(HVM)를 향해 발전함에 따라, 기존 CMOS 설계와 차별화된 곡선형 구조에 대한 OPC 및 에치 보정 과제가 새롭게 부각된다. 이 논문은 실리콘 포토닉스 응용을 위한 곡선형 OPC 알고리즘의 현황을 포괄적으로 검토하고, 고볼륨 제조 환경에서의 도전 과제와 해결 방향을 제시한다.

## 주요 기여
1. **실리콘 포토닉스 전용 OPC 과제 정의**: 기존 CMOS vs. 포토닉스 설계의 OPC/에치 보정 차이점 체계적 분석
2. **곡선형 OPC 알고리즘 비교**: 다양한 곡선형 OPC 접근법(베지어 기반, 포인트 기반, 세그먼트 기반 등)의 실리콘 포토닉스 적용 시 성능 비교
3. **고볼륨 제조 요건 분석**: HVM 환경에서의 런타임, 정확도, 재현성 요건 분석
4. **에치 보정 통합**: 포토닉스 디바이스의 복잡한 형상에 대한 에치 모델 통합 방안 제시

## 검증 방법론
- 다양한 곡선형 OPC 알고리즘에서의 EPE 및 CD 정확도 비교
- 실리콘 포토닉스 핵심 구조(waveguide, coupler, ring resonator 등)에서의 OPC 성능 평가
- 알고리즘별 런타임 및 수렴성 분석

## OPC 툴 구현 관련성
- `skopc/modeling/` 내 OPC 모듈을 실리콘 포토닉스(곡선형 구조)로 확장할 때 핵심 참고 자료
- 현재 `skopc`의 직선(맨해튼) 위주 OPC 알고리즘을 곡선형으로 확장하는 로드맵 수립에 활용
- 에치 보정 모듈과 곡선형 OPC의 통합 설계 전략으로 참고
- 포토닉스 레이아웃 에디터 지원 기능 개발 시 곡선형 구조 처리 방식으로 활용

## 태그
`Verification`, `SPIE`, `Curvilinear`, `OPC`, `Silicon_Photonics`, `HVM`, `Algorithms`, `2024`
