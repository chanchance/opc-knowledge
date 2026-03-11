# Multi-Beam Mask Writing Opens Up New Fields of Application, Including Curvilinear Mask Pattern for High Numerical Aperture Extreme Ultraviolet Lithography

## 메타데이터
- **저자**: (JMM 저자 정보)
- **연도**: 2024
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology (JMM), Vol. 23, Issue 1, 011205
- **DOI/URL**: https://doi.org/10.1117/1.JMM.23.1.011205

## 핵심 요약
다중 빔 마스크 라이터(MBMW)가 고NA EUV 리소그래피용 곡선형 마스크 패턴을 포함한 새로운 응용 분야를 열어가는 방법을 검토한다. MBMW-301이 2nm 노드 이하 고NA EUV 마스크 생산을 목표로 하며, ILT/OPC를 통한 곡선형 마스크 패턴의 고정밀 라이팅을 가능하게 한다.

## 주요 기여
1. **MBMW 세대별 발전**: MBMW-201 → MBMW-261 → MBMW-301 기술 진보 정리
2. **고NA EUV 마스크 라이팅**: 0.55NA EUV용 마스크의 고해상도/고정밀 라이팅
3. **곡선형 ILT 마스크 지원**: MBMW로 가능해진 자유형 곡선형 ILT 마스크 생산
4. **데이터 볼륨 처리**: 곡선형 마스크의 대규모 데이터 볼륨 관리 방법

## 알고리즘/수식
### MBMW 기술 사양 (MBMW-301)
```
MBMW-301 목표 사양:
  빔 수: 수백만 개 동시 빔
  해상도: < 2nm (마스크 상) = < 0.5nm (웨이퍼 상, 4x 배율)
  오버레이: < 0.3nm (마스크 상)
  처리량: 전체 칩 마스크 라이팅 < 12시간

곡선형 마스크 라이팅:
  MBMW: 픽셀 기반 라이팅 → 임의 형상 표현 가능
  VSB (Variable Shaped Beam): 사각형 기반 → 곡선형 어려움

  곡선형 ILT 마스크:
    Bezier/B-spline 제어점 → MBMW 픽셀 변환
    → 고정밀 곡선형 패턴 실현
```

### 데이터 흐름
```
OPC/ILT 출력 → 곡선형 데이터 포맷 변환 → MBMW 라이팅

데이터 볼륨:
  맨해튼 OPC → 곡선형 OPC: 데이터 5~10x 증가
  MBMW 픽셀 데이터: 추가 데이터 처리 필요
  → 효율적 압축/변환 알고리즘 필수
```

## OPC 툴 SMO 구현 관련성
- OPC/ILT → MBMW 플로우: SKOPC 곡선형 OPC 출력이 MBMW 입력으로 연결
- 데이터 포맷 통합: 곡선형 OPC 결과를 MBMW 호환 포맷으로 변환
- 고NA EUV 마스크: MBMW-301 지원 0.55NA EUV 마스크 OPC/ILT 플로우
- MRC → MBMW: 곡선형 MRC 통과 후 MBMW 라이팅으로 이어지는 통합 플로우

## 태그
`MBMW`, `multi_beam_mask_writer`, `curvilinear`, `ILT`, `EUV`, `high_NA`, `mask_writing`, `data_volume`, `OPC`, `JMM`, `2024`
