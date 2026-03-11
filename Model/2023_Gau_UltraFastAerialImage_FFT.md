# Ultra-Fast Aerial Image Simulation Algorithm Using Wavelength Scaling and Fast Fourier Transformation

## 메타데이터
- **저자**: Tsai-Sheng Gau, Po-Hsiung Chen, Burn J. Lin, Fu-Hsiang Ko, Chun-Kung Chen, Anthony Yen
- **연도**: 2023
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 22, No. 2, 023201
- **DOI/URL**: https://doi.org/10.1117/1.JMM.22.2.023201

## 핵심 요약
파장 스케일링(wavelength scaling)과 고속 푸리에 변환(FFT)을 활용하여 공중 이미지(aerial image) 시뮬레이션 속도를 기존 대비 3자리 이상(4000~5000배) 향상시키는 알고리즘을 제안한다. 강도 편차는 약 3%로 매우 낮다.

## 주요 기여
1. 193nm 파장을 2의 거듭제곱 수로 스케일링하는 파장 스케일링 기법 고안
2. 완전 FFT 기반 공중 이미지 강도 계산 알고리즘 구현
3. 기존 FT(Fourier Transform) 대비 4000~5000배 계산 속도 향상 달성
4. 강도 편차 약 3% 이하로 실용적 정확도 유지
5. OPC 및 레이아웃 최적화용 풀칩 시뮬레이션 가속 기반 제공

## 모델 수식/아키텍처
- **파장 스케일링**: λ_eff = λ_193nm × (2^n / λ_193nm) → FFT 격자와 정렬
- **마스크 스케일링**: 파장 스케일 팩터에 따라 마스크 크기 조정
- **FFT 회절 스펙트럼**: M(fx, fy) = FFT(mask(x,y))
- **역 FFT 이미지**: I(x,y) = |IFFT(M × pupil)|²
- **이미지 역스케일**: 원래 좌표계로 강도 맵 복원
- Hopkins TCC 기반 부분 가간섭 시스템에 적용

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC LithoEngine의 공중 이미지 계산 코어를 FFT 기반으로 교체 시 수천 배 속도 향상
- 풀칩 OPC 런타임 병목인 이미지 시뮬레이션 단계 직접 가속
- OPC 모델 교정(calibration) 시 대규모 게이지 데이터 시뮬레이션 속도 향상
- TorchLitho 백엔드와 결합 가능한 FFT 기반 이미지 계산 구조

## 태그
`Model`, `Optical`, `AerialImage`, `FFT`, `Simulation`, `Speed`, `Hopkins`, `SPIE`, `JMM`
