# Fabrication-Aware Computational Design of Large-Area Diffractive Optical Elements

## 메타데이터
- **저자**: Wei et al. (Stanford / NVIDIA)
- **연도**: 2025
- **게재지/학회**: SIGGRAPH Asia 2025, arXiv:2505.22313
- **DOI/URL**: https://arxiv.org/abs/2505.22313
- **인용수**: 신규 논문 (2025)

## 핵심 요약
직접 쓰기(direct-write) 그레이스케일 리소그래피와 나노 임프린팅 복제로 제작되는 대면적 회절 광학 소자(DOE)의 제조 인식 설계 파이프라인을 제안한 논문. 초해상도 신경망 리소그래피 모델로 공정 변동을 시뮬레이션하고, 텐서 병렬 FFT로 32.16mm × 21.44mm 크기 설계를 처리한다. 기존 방법 대비 제조 정확도와 광학 성능을 동시에 향상시킨다.

## 주요 기여
- 대면적 DOE 제조를 위한 제조 인식 설계 파이프라인 구축
- 초해상도 신경망 리소그래피 모델로 그레이스케일 공정 변동 예측
- 텐서 병렬 FFT로 32.16mm × 21.44mm 초대형 설계 처리
- 나노 임프린팅 복제 공정의 형상 왜곡 보상
- 제조 후 광학 성능 저하 최소화

## 알고리즘/수식
- **제조 인식 최적화**:
  - 목적함수: min_{φ} L_optical(f(g(φ))) + λ·L_fabrication(g(φ))
  - φ: 이상적 DOE 위상 프로파일
  - g(φ): 리소그래피 공정 모델 (신경망)
  - f(·): 광학 전달 함수 (FFT 기반)

- **초해상도 신경망 리소그래피 모델**:
  - 입력: 설계 레이아웃 (그레이스케일 깊이 맵)
  - 출력: 제조 후 실제 형상 예측
  - 공정 변동: 근접 효과, 로딩 효과, 현상 불균일성

- **텐서 병렬 FFT**:
  - 설계 도메인: 32.16mm × 21.44mm (수억 픽셀)
  - 블록 분할 + 분산 FFT 연산
  - GPU 클러스터 병렬화로 메모리 한계 극복

- **나노 임프린팅 보상**:
  - 임프린팅 수축·변형 모델 → 역보상 맵 생성
  - 설계 단계에서 제조 오차 선제 보정

## OPC 툴 구현 관련성
SKOPC의 LithoEngine 및 SMO 모듈에 대면적 제조 인식 최적화 접근법 제공. 텐서 병렬 FFT는 SKOPC의 풀칩 OPC 처리에서 메모리 효율화에 참조 가능. 그레이스케일 리소그래피 모델은 연속 위상 마스크(CPM) 최적화에 응용 가능. 초해상도 공정 모델은 TorchResist와 유사한 접근으로 SKOPC calibration 모듈 고도화에 참조.

## 참고문헌 (핵심)
- Rombach et al., Latent Diffusion Models — 신경망 생성 모델 기반
- Shi et al., Neural Étendue Expander — DOE 최적화 관련
- 나노 임프린팅 리소그래피 공정 문헌

## 태그
`diffractive-optics`, `DOE`, `fabrication-aware`, `grayscale-lithography`, `nano-imprinting`, `large-scale`, `neural-network`, `FFT`, `SIGGRAPH`, `2025`, `arxiv`
