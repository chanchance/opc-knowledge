# Mask Optimization Approaches in Optical Lithography Based on a Vector Imaging Model

## 메타데이터
- **저자**: Xu Ma, Yanqiu Li, Lisong Dong
- **연도**: 2012
- **게재지/학회**: Journal of the Optical Society of America A, Vol. 29, No. 7, pp. 1300–1312
- **DOI/URL**: https://doi.org/10.1364/JOSAA.29.001300
- **인용수**: 다수

## 핵심 요약
스칼라 이미징 모델(NA < 0.4)에서만 정확하던 기존 OPC/PSM 최적화의 한계를 극복하기 위해 벡터 이미징 모델 기반 픽셀화 그래디언트 OPC 및 PSM 최적화 알고리즘을 개발한다. 벡터 이미징 모델로 리소그래피 공정을 표현하는 마스크 최적화 프레임워크를 수립하고, 마스크 복잡도와 수렴 오차를 균형 잡는 일반화 웨이블릿 페널티를 제안한다.

## 주요 기여
- 벡터 이미징 모델 기반 픽셀화 그래디언트 OPC/PSM 최적화 프레임워크
- 고NA(>0.6) 리소그래피에서 편광 수차 보정 가능한 마스크 최적화
- 웨이블릿 페널티를 통한 마스크 복잡도-수렴 오차 균형
- 스칼라 vs. 벡터 모델 마스크 최적화 비교 분석

## 알고리즘/수식
**벡터 이미징 모델 강도:**
$$I(x) = \sum_k \sigma_k \sum_{\alpha \in \{x,y,z\}} \left| \int M(\mathbf{f}) H_{k,\alpha}(\mathbf{f}) e^{i2\pi \mathbf{f} \cdot x} d\mathbf{f} \right|^2$$
TE/TM/z 편광 성분 $\alpha$에 대한 pupil 함수 $H_{k,\alpha}$ 포함.

**벡터 TCC (Transmission Cross Coefficient):**
$$TCC^V(\mathbf{f}_1, \mathbf{f}_2) = \sum_k \sigma_k \sum_\alpha H_{k,\alpha}(\mathbf{f}_1) H_{k,\alpha}^*(\mathbf{f}_2)$$
편광 성분을 포함한 벡터 TCC 정의.

**마스크 최적화 비용함수:**
$$F(m) = \sum_j \left(I(x_j; m) - I_{target}(x_j)\right)^2 + \lambda_w \|W \cdot m\|_2^2$$
웨이블릿 정규화 항 $\|W \cdot m\|_2^2$ 포함.

**그래디언트 (벡터 모델):**
$$\frac{\partial F}{\partial m_p} = 2\sum_j (I_j - I_{target,j}) \cdot \frac{\partial I_j}{\partial m_p}$$

$$\frac{\partial I_j}{\partial m_p} = 4\sum_\alpha \text{Re}\left[ \left(\sum_{\mathbf{f}} H_\alpha(\mathbf{f}) e^{i2\pi \mathbf{f} \cdot x_j}\right)^* \cdot H_\alpha(\mathbf{f}_p) e^{i2\pi \mathbf{f}_p \cdot x_j} \right]$$

**일반화 웨이블릿 페널티:**
$$\Omega_{wavelet}(m) = \sum_{l,k} |w_{l,k}(m)|^p, \quad p \in [1,2]$$
웨이블릿 변환 계수 $w_{l,k}$의 $l_p$-노름으로 마스크 복잡도 제어.

## OPC 툴 SMO 구현 관련성
- SKOPC 고NA 벡터 이미징 기반 마스크 최적화 구현 시 참고
- `skopc/litho/vector_imaging.py`에 벡터 TCC 및 TE/TM/z 성분 이미징 모델 구현
- `skopc/modeling/vector_opc.py`에 벡터 이미징 기반 픽셀화 OPC 구현
- Ma et al. 2013 JOSAA 픽셀화 SMO와 함께 HKU Arce 그룹 벡터 이미징 계열 참고

## 참고문헌 (핵심)
- Ma et al., \"Pixelated SMO immersion,\" JOSAA 2013
- Li et al., \"Robust pixelbased SMO 3D imaging,\" Optics & Laser Technology 2013
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011

## 태그
`OPC`, `ILT`, `JOSAA`, `vector-imaging`, `mask-optimization`, `gradient-based`, `TCC`, `polarization`, `wavelet-penalty`, `high-NA`, `TE-TM-z`, `PSM`, `HKU`
