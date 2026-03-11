# Optical Proximity Correction (OPC) Under Immersion Lithography

## 메타데이터
- **저자**: Awad et al. (IntechOpen Chapter)
- **연도**: 2018
- **게재지/학회**: IntechOpen - Advanced Lithography 챕터
- **DOI/URL**: https://www.intechopen.com/chapters/58480
- **유형**: 교과서 챕터 / 종합 리뷰

## 핵심 요약
본 챕터는 193nm 침지 리소그래피(Immersion Lithography)에서의 OPC 기술을 체계적으로 다루는 종합 리뷰다. 서브 16nm 이하 기술 노드에서 차세대 리소그래피(NGL)가 아직 성숙하지 않은 시점에서 193nm 침지 리소그래피와 OPC의 중요성을 강조하며, MB-OPC(모델 기반 OPC)의 전체 플로우를 단계별로 설명한다. SRAF, 세리프(serif), 해머헤드(hammerhead) 등 보조 패턴 기술도 포함한다.

## 주요 기여
- **MB-OPC 플로우 종합 설명**: 모델 데이터 수집부터 사후 OPC 검증까지 단계별 가이드
- **침지 리소그래피 OPC 도전과제**: 서브 16nm에서의 특수 OPC 요구사항 정리
- **최신 OPC 알고리즘 비교**: 다양한 OPC 알고리즘의 성능 및 제조 가능성 비교
- **공정 변이 인식 OPC**: 공정 변이를 반영한 강건한 OPC 방법론

## Recipe/Process Flow 상세

### MB-OPC 표준 플로우 (산업 표준)

```
1단계: RET(해상도 향상 기술) 선택
  ─ OAI(오프-액시스 조명), PSM, SRAF 등 선택
  ─ 노드별 최적 RET 조합 결정

2단계: 설계 규칙 선택
  ─ CDmin, 간격, 오버레이 허용치 설정
  ─ DRC 규칙 확정

3단계: OPC 모델 구축
  ──────────────────────────────────────
  [모델 데이터 수집]
  ─ 테스트 마스크 제작
  ─ 웨이퍼 인쇄 및 CD-SEM 측정
  ─ 수천~수만 개 게이지(gauge) 패턴 수집
    (1D 패턴: 라인-스페이스, 격리 라인)
    (2D 패턴: 라인엔드, 코너, 좁은 간격)
  ──────────────────────────────────────
  [모델 설정 및 캘리브레이션]
  ─ 광학 모델 파라미터 설정:
    NA, σ(부분 간섭도), 수차 계수(Zernike)
  ─ 레지스트 모델 파라미터 설정:
    임계 에너지, 확산 계수, Dill 파라미터
  ─ 에치 모델 (선택적): 에치 바이어스 보정
  ─ 최소 RMS 오차로 파라미터 최적화:
    min Σ|CD_measured - CD_simulated|²
  ──────────────────────────────────────

4단계: 레시피 설정 (Recipe Setup)
  ─ 레이어별 OPC 파라미터 설정:
    ├── 세그먼테이션: 최소/최대 세그먼트 길이
    ├── 이동 한계: 내부/외부 최대 이동 거리
    ├── 반복 횟수: 최대 OPC 반복 수
    ├── 수렴 기준: EPE 허용 오차
    └── 특수 규칙: 라인엔드, 코너 처리
  ─ SRAF 규칙 설정:
    ├── SRAF 배치 간격 테이블
    ├── SRAF 크기 (폭, 길이)
    └── SRAF 최대 개수
  ─ 보조 패턴 규칙:
    세리프(Serif), 해머헤드(Hammerhead)

5단계: OPC 보정
  ──────────────────────────────────────
  [MB-OPC 반복 루프]
  a) 레이아웃 폴리곤 세그먼트 분할
  b) 마스크 이미지 생성
  c) 리소그래피 시뮬레이션 (공중 이미지 → 레지스트 윤곽)
  d) 설계 타겟과 시뮬레이션 윤곽 비교 → EPE 계산
  e) EPE 감소 방향으로 각 세그먼트 이동
  f) 수렴 기준 충족까지 a~e 반복
  ──────────────────────────────────────
  ─ 보조 패턴 추가:
    SRAF, 세리프, 해머헤드 자동 삽입

6단계: 사후 OPC 검증 (Post-OPC Verify)
  ─ 풀칩 모델 기반 검증
  ─ 목적: 잠재적 취약점(weak points) 예측
  ─ 출력: 핫스팟 목록, EPE 분포
  ─ 피드백: 레시피 조정 → OPC 재실행
```

### 침지 리소그래피 OPC 특수 고려사항
193nm 침지 리소그래피에서의 추가 도전:
- **편광 효과**: 높은 NA에서 편광이 OPC에 미치는 영향
- **플레어(Flare)**: 장거리 산란광에 의한 CD 변동
- **워터 렌즈 효과**: 침지 매질(물)의 굴절률 변화
- **수직 OPC**: 초점 심도(DoF) 내에서의 수직 벽 형성

### 보조 패턴 상세
| 패턴 유형 | 목적 | 위치 | 크기 |
|---------|------|------|------|
| SRAF | 공정 윈도우 향상 | 메인 피처 옆 | 해상도 이하 |
| 세리프(Serif) | 코너 보정 | 폴리곤 코너 | nm 스케일 |
| 해머헤드(Hammerhead) | 라인엔드 보정 | 라인 끝 | nm 스케일 |

### 주요 OPC 알고리즘 비교
- **규칙 기반 OPC (RBOPC)**: 빠르지만 90nm 이하 부적합
- **모델 기반 OPC (MBOPC)**: 정확하지만 계산 집약적
- **ILT**: 최고 품질, 최고 계산 비용
- **최신 빠른 OPC**: MBOPC와 ILT의 절충안

## OPC 툴 구현 관련성
이 챕터는 SKOPC의 핵심 OPC 플로우 설계의 표준 참조:
- **표준 플로우 준수**: SKOPC의 6단계 OPC 플로우가 이 산업 표준과 일치
- **레시피 파라미터**: SKOPC YAML 레시피의 세그먼테이션/이동 한계 파라미터 정의
- **모델 캘리브레이션**: `skopc/modeling/calibration.py`의 CD 데이터 기반 파라미터 최적화
- **사후 OPC 검증**: OPC 완료 후 LithoHoD/Unitho 기반 핫스팟 검출 통합

## 참고문헌 (핵심)
- Levenson, "Improving resolution in photolithography with a phase-shifting mask" (1982)
- Cobb, "Fast pixel-based mask optimization for inverse lithography" (JM3 2006)
- Torres et al., "Integration of sub-resolution assist features" (SPIE 2003)
- Ma et al., "OPC by modeling" (2010 textbook)

## 태그
`Model-based OPC`, `Immersion Lithography`, `OPC Flow`, `Recipe Setup`, `Model Calibration`, `SRAF`, `Serif`, `Hammerhead`, `193nm`, `Post-OPC Verification`, `IntechOpen`, `2018`, `Industry Standard`
