# Enabling Scalable AI Computational Lithography with Physics-Inspired Models

## 메타데이터
- **저자**: Haoyu Yang, Haoxing Ren (NVIDIA Corp.)
- **연도**: 2023
- **게재지/학회**: 28th Asia and South Pacific Design Automation Conference (ASP-DAC 2023); also SPIE Advanced Lithography + Patterning 2023
- **DOI/URL**: https://dl.acm.org/doi/10.1145/3566097.3568361
- **인용수**: 미확인

## 핵심 요약
컴퓨테이셔널 리소그래피를 위한 확장 가능한 AI 프레임워크를 제안한다. 기존 CNN 기반 솔루션의 한계를 극복하기 위해 신경망 설계에 리소그래피 편향(lithography bias)을 도입하여 더 효율적인 모델 설계와 성능 향상을 달성한다. 두 가지 핵심 문제—리소그래피 모델링(마스크에서 웨이퍼 형상 예측)과 마스크 최적화(역 리소그래피)—를 물리 영감 신경망 모델로 해결한다. NVIDIA의 컴퓨테이셔널 리소그래피 연구 방향성을 대표하는 핵심 논문으로, cuLitho로 이어지는 NVIDIA의 AI 리소그래피 연구 계보에 해당한다.

## 주요 기여
- **물리 영감 신경망 설계**: 리소그래피 물리 편향을 신경망 아키텍처에 직접 내장
- **확장 가능한 AI 리소그래피**: 전체 칩 규모에서 적용 가능한 확장 가능한 모델 설계
- **리소그래피 모델링 + 역 리소그래피 통합**: 두 핵심 태스크를 물리 영감 접근으로 동시 해결
- **CNN 기반 한계 극복**: 기존 순수 데이터 기반 CNN의 물리적 비정합성 문제 해결
- **성능 효율 동시 향상**: 기존 방법 대비 모델 효율성과 성능 모두 향상

## 검증 방법론
- **리소그래피 시뮬레이션 정확도**: 물리 영감 모델과 수치 시뮬레이터의 웨이퍼 컨투어 예측 비교
- **마스크 최적화 품질**: EPE 및 PVB 기준 역 리소그래피 결과 평가
- **확장성 검증**: 작은 패턴에서 전체 칩 스케일까지의 성능 확장성 측정
- **기존 CNN 비교**: 리소그래피 편향 없는 순수 CNN 대비 성능 비교
- **속도 효율**: 수치 시뮬레이터 대비 추론 속도 비교

## 검증 지표
- **EPE 허용 범위**: 마스크 최적화 결과의 웨이퍼 시뮬레이션 EPE
- **PVB (Process Variation Band)**: 공정 변동에 대한 최적화 마스크 견고성
- **L2 오차**: 리소그래피 시뮬레이션 예측의 픽셀 오차
- **사용 시뮬레이터**: 수치 리소그래피 시뮬레이터 (ICCAD/SPIE 벤치마크)
- **검증 커버리지**: ICCAD 벤치마크 + SPIE 2023 발표 산업 데이터

## OPC 툴 구현 관련성
SKOPC의 리소그래피 시뮬레이션 및 OPC 최적화 엔진에 다음과 같이 활용 가능:
1. **물리 영감 OPC 모델**: SKOPC의 모델 OPC에 리소그래피 물리 편향을 가진 신경망 모델 통합
2. **확장 가능한 전체 칩 OPC**: 물리 영감 모델의 확장성으로 전체 칩 OPC 검증 지원
3. **NVIDIA cuLitho 연계**: cuLitho로 이어지는 NVIDIA 연구 계보로 cuLitho 통합 방향성 참고
4. **리소그래피 시뮬레이터 가속**: 물리 영감 신경망으로 수치 시뮬레이터를 빠르게 근사
5. **물리-AI 하이브리드**: 물리 모델 정확도와 AI 속도를 결합한 하이브리드 리소그래피 엔진

## 참고문헌 (핵심)
- Yang et al. (2022) - CFNO: 대규모 마스크 최적화 (후속 연구)
- Yang & Ren (2024) - ILILT, GPU-ILT (후속 연구)
- Mukhopadhyay et al. (2026) - cuLitho (후속 산업 연구)
- Hopkins 이미징 모델 관련 리소그래피 기초 참고문헌
- ICCAD 2012/2019 벤치마크 데이터셋

## 태그
`Verification`, `OPC`, `Physics-Inspired`, `Scalable AI`, `Computational Lithography`, `Lithography Modeling`, `Mask Optimization`, `ASP-DAC`, `SPIE`, `2023`, `NVIDIA`, `CNN`, `Deep Learning`, `ILT`
