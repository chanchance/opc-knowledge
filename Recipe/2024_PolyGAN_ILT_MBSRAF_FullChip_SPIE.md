# Synthesizing ILT MB-SRAF Using Machine Learning (POLY-GAN)

## 메타데이터
- **저자**: Ferhat Turker Celepcikay, Chun-Cheng Liao, Teng-Yen Huang, Szu-Ping Chen, Chi Neng Lin, Alan Zhu, Hung Yu Lin
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129540H
- **DOI/URL**: https://doi.org/10.1117/12.3010902
- **인용수**: ~10

## 핵심 요약
ILT 기반 Model-Based SRAF(MB-SRAF)를 전체 칩으로 확장하기 위해 POLY-GAN이라는 새로운 GAN 아키텍처를 제안한다. POLY-GAN은 pix2pix 조건부 GAN을 기반으로 하되 SRAF의 다각형 형상을 학습에 특화한 구조로, 빠르고 정확하며 문맥 인식적(in-context) ILT MB-SRAF 합성이 가능하다. 기존 Rule-based SRAF와 Model-based SRAF의 속도/정확도 트레이드오프를 해결하며, ILT 수준의 SRAF 품질을 전체 칩 수준에서 실용적인 TAT로 제공한다.

## 주요 기여
1. POLY-GAN: 다각형 형상 학습에 특화된 ILT MB-SRAF 합성 GAN
2. 전체 칩 ILT MB-SRAF 생성의 end-to-end 흐름 구현
3. ILT 품질의 SRAF를 전체 칩 실용적 런타임으로 제공
4. 문맥 인식(in-context) SRAF: 주변 패턴 밀도와 2D 환경 반영

## Recipe/Process Flow 상세

### ILT MB-SRAF의 필요성과 한계
```
SRAF 방법 비교:
  RB-SRAF (Rule-based):
    방법: Space-Width 테이블 → SRAF 크기/위치 결정
    장점: 빠름 (수 분/전체 칩)
    단점: 2D 패턴, 복잡한 밀도 변화 처리 한계

  MB-SRAF (Model-based):
    방법: 리소그래피 시뮬로 최적 SRAF 위치 계산
    장점: 정확도, 공정 윈도우 최대화
    단점: 느림 (수 시간/전체 칩)

  ILT MB-SRAF:
    방법: ILT 수치 최적화로 SRAF 포함 마스크 최적화
    장점: 최고 공정 윈도우 성능
    단점: 매우 느림 (수십 시간/전체 칩)

POLY-GAN 목표:
  ILT MB-SRAF 품질 + RB-SRAF 수준 속도
```

### POLY-GAN 아키텍처
```
기반: pix2pix 조건부 GAN

POLY-GAN 특화 설계:
  입력: 타겟 레이아웃 패턴 이미지 (주 패턴)
  출력: ILT MB-SRAF 배치 이미지

생성기(G) 특화:
  U-Net 기반 + 다각형 인식 컨볼루션
  SRAF 다각형의 직선 경계, 코너 형상 보존
  다중 스케일 처리: 전체 패턴 문맥 + 로컬 SRAF 형상

판별기(D):
  PatchGAN: 로컬 SRAF 품질 판별
  글로벌 판별기: 전체 SRAF 배치 일관성
  진짜: ILT 솔버로 생성된 MB-SRAF 배치

손실 함수:
  L_total = L_adv + λ_L1 × L_L1 + λ_litho × L_litho + λ_poly × L_poly
  L_poly: SRAF 다각형 경계 품질 손실 (POLY-GAN 특화)
  L_litho: 리소그래피 시뮬 기반 공정 윈도우 손실
```

### 전체 칩 적용 흐름
```
훈련 단계:
  1. 대표 레이아웃 패턴 수집 (다양한 CD/pitch/density)
  2. 각 패턴에 ILT 솔버 적용 → Ground Truth ILT MB-SRAF
  3. (레이아웃, ILT SRAF) 쌍으로 POLY-GAN 훈련

추론 단계 (전체 칩):
  타겟 레이아웃 → POLY-GAN 추론 → SRAF 배치 이미지
  추론: ms/클립 → 전체 칩 수 분

후처리:
  SRAF 이미지 → 다각형 벡터화
  MRC(마스크 규칙 검사) 준수 확인 및 보정
  ILT 솔버 소수 이터레이션으로 미세 조정 (선택)
```

### 성능 결과
```
SRAF 품질 비교 (공정 윈도우):
  ILT MB-SRAF (기준): DOF × EL = 100%
  POLY-GAN SRAF:       ILT 대비 동등하거나 근접 (95%+)
  RB-SRAF:             ILT 대비 낮음

런타임 비교:
  ILT 솔버: 수십 시간 (전체 칩)
  POLY-GAN 추론: 수 분 (전체 칩)
  속도 향상: 수백 배

문맥 인식 SRAF:
  고밀도/저밀도 전환 영역: 자동 SRAF 밀도 조정
  2D 코너, 엔드-캡 패턴: ILT와 유사한 SRAF 형상
```

## OPC 툴 구현 관련성
- **SKOPC POLY-GAN SRAF**: `skopc/modeling/sraf_generator.py`에 POLY-GAN 백엔드 추가
- **ILT 훈련 데이터**: OpenILT로 Ground Truth ILT SRAF 생성 → POLY-GAN 훈련
- **다각형 손실**: SRAF 다각형 경계 품질 손실 L_poly 구현
- **전체 칩 파이프라인**: POLY-GAN 추론으로 전체 칩 SRAF 삽입 TAT 단축

## 참고문헌
- Proc. SPIE 12954, DTCO and Computational Patterning III (April 2024)
- 관련: GAN SRAF placement (Ciou, SPIE 11613, 2021)
- 관련: ML-assisted SRAF full chip (Wang, SPIE 10451, 2017)
- 관련: Neural-ILT (ICCAD 2020 / TCAD 2022)
- 관련: ILT natural solution for MB-SRAF (Pang, SPIE 6607, 2007)

## 태그
`Recipe`, `SPIE`, `SRAF`, `ILT`, `GAN`, `POLY-GAN`, `MB-SRAF`, `FullChip`, `MachineLeaning`, `ProcessWindow`, `2024`
