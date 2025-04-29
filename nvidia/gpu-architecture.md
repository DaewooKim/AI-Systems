# Ampere Architecture

# Hopper Architecture

# Blackwell Architecture
## Overview
Blackwell 아키텍처는 데이비드 H. 블랙웰(David H. Blackwell)의 업적에서 영감을 받았으며, 그의 확률론, 게임 이론, 동적 프로그래밍 분야에 대한 심오한 기여는 현대 AI의 발전에 중요한 기반이 되었다. NVIDIA Blackwell 제품은 모든 규모의 기업이 경제적인 방식으로 LLM을 구축하고 배포하며 활용할 수 있도록 지원하며, 수십조 개의 파라미터를 갖는 모델을 실시간으로 처리할 수 있도록 설계되었다.
## Blackwell 아키텍처의 주요 혁신 사항
### 2세대 트랜스포머 엔진
* 2nd Gen Transformer Engine은 맞춤형 Tensor Core 기술과 TensorRT-LLM 및 Nemo 프레임워크의 혁신을 결합하여 LLM 및 MoE 모델의 추론 및 학습을 가속화한다.
* 고급 동적 범위 관리 알고리즘과 마이크로 텐서 스케일링 기술을 활용하여 성능과 정확도를 최적화하고 FP4를 지원한다.
### 성능 중심의 기밀 컴퓨팅 및 보안 AI
* 업계 최초로 CPU에서 GPU로 확장된 TEE(Trusted Execution Environment)을 통해 민감한 데이터를 보호하고 AI 모델의 무결성을 보장한다.
* Blackwell은 TEE I/O 기능을 갖춘 호스트와 함께 가장 성능이 뛰어난 Confidential Compuitng 솔루션을 제공하고, NVLink를 통한 인라인 보호를 제공한다. 
### 5세대 NVLink 및 NVLink 스위치
* 5세대 NVLink는 NVLink 스위치 ASIC 및 이를 기반으로 구축된 스위치를 통해 **최대 576개의 GPU**를 연결하여 대규모 컴퓨팅 클러스터를 구축할 수 있다.
* 5th Gen NVLink는 NVIDIA Hopper의 4th Gen NVLink 대비 성능을 2배 증가시켰다.
* Blackwell GPU는 18개의 5세대 NVLink 링크를 내장하여 총 1.8TB/sec(방향당 900GB/sec)의 대역폭을 제공한다. (Link 당 50 GB/sec)
* NVLink 스위치는 하나의 72개 GPU NVLink 도메인(NVL72)에서 130TB/sec의 GPU 대역폭을 제공한다. (1.8TB/sec*72=129.6TB/sec)
* FP8 지원 NVIDIA SHARP(Scalable Hierarchical Aggregation and Reduction Protocol)는 4배의 효율성을 제공한다.
### 압축 해제 엔진 (Decompression Engine)
* Blackwell의 전용 압축 해제 엔진은 데이터 분석 및 데이터 과학에서 최고 성능을 위해 데이터베이스 쿼리의 전체 파이프라인을 가속화한다.
* 최대 800GB/s의 속도로 데이터를 압축 해제할 수 있으며 최대 800GB/s의 속도로 데이터를 압축 해제할 수 있어 최대 800GB/s의 속도로 데이터를 압축 해제할 수 있어 최신 압축 방식인 LZ4, Snappy, Deflate를 지원하며 쿼리 벤치마크에서 CPU보다 18배, H100 GPU보다 6배 더 빠른 성능을 보인다.
### RAS 엔진 (Reliability, Availability, and Serviceability Engine)
* RSA 엔진은 발생 가능한 잠재적 오류를 조기에 식별하여 가동 중단 시간을 최소화하는 지능형 복원력을 제공한다.
* NVIDIA의 AI 기반 예측 관리 기능은 HW/SW 전반 수천개의 데이터 포인트를 지속적으로 모니터링하여 전반적인 상태를 파악하고 가동 중단 및 비효율성의 원인을 예측하고 차단한다.
* RSA 엔진은 교체 부품이 필요한 것으로 식별하면 대기 용량을 활성화하여 성능 저하를 최소화하여 작업을 제시간에 완료할 수 있도록 한다.
