# Ampere Architecture

# Hopper Architecture

# Blackwell Architecture
## Overview
Blackwell 아키텍처는 데이비드 H. 블랙웰(David H. Blackwell)의 업적에서 영감을 받았으며, 그의 확률론, 게임 이론, 동적 프로그래밍 분야에 대한 심오한 기여는 현대 AI의 발전에 중요한 기반이 되었다. NVIDIA Blackwell 제품은 모든 규모의 기업이 경제적인 방식으로 LLM을 구축하고 배포하며 활용할 수 있도록 지원하며, 수십조 개의 파라미터를 갖는 모델을 실시간으로 처리할 수 있도록 설계되었다.
## Blackwell 아키텍처의 주요 혁신 사항
### 2세대 트랜스포머 엔진
* 새로운 4비트 부동 소수점(FP4) 정밀도를 지원하여 더 높은 정확도를 유지하면서도 컴퓨팅 및 메모리 대역폭 요구 사항을 줄여 LLM 훈련 및 추론 성능을 향상시켰다.
* 텐서RT-LLM 및 Nemo Framework와의 통합을 통해 다양한 MoE(Mixture-of-Experts) 모델을 효율적으로 처리할 수 있다.
### 성능 중심의 기밀 컴퓨팅 및 보안 AI
* CPU에서 GPU로 확장된 신뢰 실행 환경(Trusted Execution Environment, TEE)을 통해 민감한 데이터를 보호하고 AI 모델의 무결성을 보장합니다.
* 하드웨어 기반 암호화 및 TEE/I/O 기능을 통해 연합 학습(Federated Learning)과 같은 개인 정보 보호가 중요한 사용 사례를 지원합니다.
### 5세대 NVLink 및 NVLink 스위치
* 5세대 NVLink는 NVLink 스위치 ASIC 및 이를 기반으로 구축된 스위치를 통해 **최대 576개의 GPU**를 연결하여 대규모 컴퓨팅 클러스터를 구축할 수 있습니다.
* 5th Gen NVLink는 NVIDIA Hopper의 4th Gen NVLink 대비 성능을 2배 증가시켰다.
* Blackwell GPU는 18개의 5세대 NVLink 링크를 내장하여 총 1.8TB/sec(방향당 900GB/sec)의 대역폭을 제공한다. (Link 당 50 GB/sec)
* NVLink 스위치는 하나의 72개 GPU NVLink 도메인(NVL72)에서 130TB/sec의 GPU 대역폭을 제공한다. (1.8TB/sec*72=129.6TB/sec)
### 압축 해제 엔진 (Decompression Engine)
* 데이터 분석 및 과학 워크플로우에서 병목 현상을 줄이기 위해 설계된 전용 하드웨어 엔진입니다.
* 고속 압축 해제를 통해 데이터 처리 속도를 크게 향상시켜 데이터 과학자들이 더 빠르게 통찰력을 얻을 수 있도록 지원합니다. GB200 슈퍼칩에서 최대 800GB/s의 압축 해제 속도를 제공하며, 이는 기존 CPU 기반 솔루션 대비 최대 18배 빠른 성능입니다.
### RAS 엔진 (Reliability, Availability, and Serviceability Engine)
* 하드웨어 및 소프트웨어 오류를 예측하고 완화하여 시스템 가용성을 극대화하는 지능형 복원력 기능을 제공합니다.
* AI 기반 예측 관리 기능을 통해 다운타임을 최소화하고 유지 보수 작업을 효율적으로 관리할 수 있도록 지원합니다.
