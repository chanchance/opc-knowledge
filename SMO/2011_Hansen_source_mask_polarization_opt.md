# Source Mask Polarization Optimization

## 메타데이터
- **저자**: Steven G. Hansen
- **연도**: 2011
- **게재지/학회**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 10, No. 3, 033003
- **DOI/URL**: https://doi.org/10.1117/1.3607424
- **인용수**: 확인 필요

## 핵심 요약
소스-마스크-편광 최적화(SMPO, Source Mask Polarization Optimization)의 핵심 측면을 분석하여, XY 또는 TE와 같은 친숙한 편광 조건 이외에도 비통상적인 편광 상태가 이미징 성능에 유익한 경우를 규명한다. 감쇠 위상 시프트 마스크(attenuated PSM)와 홀 패턴, 다크 필드 조명에서 특이 편광 조건의 효과를 0차 회절광과 고차 회절광 간섭 관점에서 분석한다.

## 주요 기여
- 소스-마스크-편광 최적화(SMPO) 프레임워크의 편광 차원 분석
- 비통상적 편광(XY/TE 이외) 상태가 이미지 형성에 유익한 조건 규명
- 감쇠 PSM + 홀 패턴에서 편광 최적화 효과 분석
- 다크 필드 조명에서 편광 상태 선택의 영향 체계화

## 알고리즘/수식
**벡터 이미징 모델 (Jones 행렬):**
$$\mathbf{E}_{wafer}(x) = \int P(\mathbf{f}) \cdot M(\mathbf{f}) \cdot \mathbf{J}_{pol}(\mathbf{f}) \, e^{i2\pi \mathbf{f} \cdot x} \, d\mathbf{f}$$
편광 Jones 행렬 $\mathbf{J}_{pol}$을 포함하는 벡터 이미징 적분.

**편광 상태 매개변수화:**
$$\mathbf{J}_{pol} = \begin{pmatrix} \cos\phi & -\sin\phi \\ \sin\phi & \cos\phi \end{pmatrix}$$
편광 각도 $\phi$로 매개변수화된 선형 편광.

**SMPO 강도 이미지:**
$$I(x) = \int \sigma(\mathbf{f}_s) \left| \sum_{\mathbf{f}} M(\mathbf{f}-\mathbf{f}_s) \mathbf{J}_{pol}(\mathbf{f}_s) H(\mathbf{f}) e^{i2\pi \mathbf{f} \cdot x} \right|^2 d\mathbf{f}_s$$

**0차/고차 회절광 간섭 분석:**
$$I_{interference} = 2 \text{Re}\left[ E_0^* \cdot E_{\pm 1} \right] \cdot \cos(\Delta\phi_{pol})$$
편광 상태에 따른 회절차수 간 간섭 변화 분석.

**다크 필드 조명 편광 최적화:**
$$\sigma_{optimal} = \arg\max_{\sigma, \phi} NILS(\sigma, \phi)$$
편광 각도 $\phi$를 소스 분포 $\sigma$와 함께 공동 최적화.

## OPC 툴 SMO 구현 관련성
- SKOPC 편광 최적화 기능 구현 시 SMPO 이론적 기반으로 참고
- `skopc/smo/polarization_smo.py`에 SMPO 편광 매개변수화 구현
- 감쇠 PSM + 홀 패턴에서 특이 편광 상태 활용 시 참고
- Ma et al. 2015 그래디언트 기반 SPMO와 함께 편광 최적화 계열로 활용

## 참고문헌 (핵심)
- Socha et al., \"Simultaneous SMO,\" Optical Microlithography 2005
- Rosenbluth et al., \"Global illumination optimization,\" SPIE 2006
- Ma et al., \"Gradient-based joint SPMO,\" JM3 2015

## 태그
`SMO`, `JM3`, `SPIE`, `polarization`, `SMPO`, `source-mask-polarization`, `vector-imaging`, `dark-field`, `attenuated-PSM`, `Jones-matrix`, `diffraction-interference`
