# Ampere Architecture
## Key features
### TF32를 갖춘 3rd Gen Tensor Core
A100 3rd Gen Tensor Core는 연산 피연산 공유를 강화하고 효율성을 개선하며, 다음과 같은 강력한 새로운 데이터 유형을 추가하였다.
* **TF32 Tensor Core 명령**
  * A100 GPU의 Tensor Core에서 실행되는 TF32는 전 세대(Volta GPU)의 FP32 연산보다 최대 10배 빠른 속도를 제공한다.
  * Structural Sparsity와 결합하면 Volta 대비 최대 20배의 성능 향상을 얻을 수 있다.
* **IEEE 호환 FP64 Tensor Core 명령**
  * HPC를 위한 기능이며, 이전 세대보다 HPC 애플리케이션의 연산 성능을 최대 2.5배 향상시켰다.
* **BF16 Tensor Core 명령**
  * FP16과 동일한 처리량을 제공한다.
### Multi-Instance GPU(MIG)
* 단일 A100 GPU를 최대 7개의 개별 GPU로 분할할 수 있다.
* 이를 통해 다양한 크기의 작업에 필요한 연산 성능을 제공하여 최적의 활용률과 투자 수익을 극대화한다.
### 3rd Gen NVLink
* 서버에서 효율적인 성능 향상을 제공하기 위해 GPU 간의 고속 연결을 2배로 향상시킨다.
### Structural Sparsity
* A100 Tensor Core의 새로운 Sparisty 지원은 딥러닝 네트워크의 미세한 Structured Sparsity을 활용하여 Tensor Core 연산처리량을 2배로 증가시킬 수 있다. 

## A100 GPU hardware architecture
NVIDIA GA100 GPU는 Multiple GPU Processing Clusters(GPUs), Texture Processing Clusters(TPCs), Streaming Multiprocessors(SMs), HBM2 메모리 컨트롤러로 구성되어 있다.
GA100 GPU는 128 SMs를 가지며, A100는 GA100를 기반으로 108 SMs를 가진다. 
![image](https://developer-blogs.nvidia.com/wp-content/uploads/2021/guc/gaEfOQD6l3q8p4TzybT7gMVZc8YQkni-0-9ClI9Ei4epE4aHSLjg9-3ON8bkRFZxvm1G-nOCZ9CPy_zqw-EmBWje-sOiSem0oFWA4J7HnhdVdF5RUbrLB7n5-XGKDGznfh6R3xna.png)

| 항목                           | GA100 (Full Implementation) | A100 (Actual Product)       |
|:--------------------------------|-----------------------------------------:|-----------------------------------------:|
| GPCs(GPU Processing Clusters)   | 8                            | 7                            |
| TPCs(Texture Processing Clusters) per GPC                   | 8                            | 7 또는 8                     |
| SMs per TPC                     | 2                            | 2                            |
| SMs per GPC                     | 16                           | 최대 16                      |
| 총 SM 수 (Total SMs)            | 128                          | 108                          |
| FP32 CUDA 코어 per SM           | 64                           | 64                           |
| 총 FP32 CUDA 코어 수            | 8192 (128×64)               | 6912 (108×64)               |
| 3세대 Tensor 코어 per SM        | 4                            | 4                            |
| 총 Tensor 코어 수               | 512 (128×4)                 | 432 (108×4)                 |
| HBM2 메모리 스택 수             | 6                            | 5                            |
| 메모리 컨트롤러 (512-bit)       | 12                           | 10                           |

## A100 SM architecture
A100의 SM(Stream Multiprocessor)은 Volta 및 Turing의 SM 설계를 기반으로 하여 성능이 크게 향상되었고, 새로운 기능들이 대폭 추가되었다.
![image](https://developer-blogs.nvidia.com/wp-content/uploads/2021/guc/raD52-V3yZtQ3WzOE0Cvzvt8icgGHKXPpN2PS_5MMyZLJrVxgMtLN4r2S2kp5jYI9zrA2e0Y8vAfpZia669pbIog2U9ZKdJmQ8oSBjof6gc4IrhmorT2Rr-YopMlOf1aoU3tbn5Q.png)

### Tensor Core 성능 개선
* A100의 3세대 Tensor Core는 FP16/FP32 혼합 정밀도 FMA 연산을 클럭당 256회 수행하며, SM당 총 4개가 탑재되어 있어 SM 하나에서 클럭당 1024 연산이 가능하다. (Volta/Turing 대비 2배).
* 다양한 데이터 타입(FP16, BF16, TF32, FP64, INT8, INT4, Binary)을 지원하며, sparsity 기능을 통해 연산 성능을 2배까지 향상시켰다.
### 성능 비교 (V100 대비)
* FP16: 2.5 배 (sparsity 활용 시, 5배)
* FP64: 2.5 배  
* INT8: 10 배 (sparsity 활용 시, 20배)
* TF32: FP32 대비 10 배 (sparsity 활용 시, 20배) 
![image](https://developer-blogs.nvidia.com/wp-content/uploads/2020/05/Sparse-Tensor-Core-Quad-White-1024x576.png)
### TF(TensorFloat-32) 도입
* TF32(TensorFloat-32)는 FP32와 동일한 **범위(8비트 지수)**를 가지면서, **FP16과 같은 정밀도(10비트 가수)**를 제공한다.
* A100은 TF32를 통해 FP32 입력/출력을 유지하면서도 Tensor 연산을 가속할 수 있으며, 기존 DL/HPC 프레임워크에 손쉽게 통합 가능하다.
* 사용자는 기존 FP32 학습 코드를 변경하지 않고도 자동으로 가속 가능하다.
* TF32는 내부 연산에서 FP32보다 낮은 정밀도를 사용하나, 출력은 IEEE 표준 FP32로 제공한다.
![image](https://developer.nvidia.com/blog/wp-content/uploads/2020/05/TensorFloat32-TF32.jpg)
### 메모리 및 캐시
* 공유 메모리 + L1 캐시 통합 용량: 192KB, V100 대비 1.5배
* 비동기 복사 명령어: 글로벌 메모리에서 공유 메모리로 직접 로딩 (L1 캐시 우회 가능)
* 비동기 barrier 유닛: 비동기 복사 명령어와 함께 사용
* L2 캐시 관리 및 상주 제어를 위한 새로운 명령어
* CUDA Cooperative Groups를 위한 warp-level reduction 명령어 추가
* 소프트웨어 복잡도를 줄이기 위한 다양한 프로그래밍 개선

# Hopper Architecture
## Key Features
### 새로운 Streaming Multi-processor(SM)
* **4th Gen Tensor Cores**
  * 새로운 4th Gen Tensor Core는 A100 대비 칩 간 연산 속도가 최대 6배 빠르며, SM 단위 성능 향상, SM 수 증가, H100의 클럭 속도 증가 등을 포함한다.
  * SM 단위 기준으로, Tensor Core는 동등한 데이터 타입에서 A100 대비 2배의 MMA 연산 속도를 제공하며 새로운 FP8 데이터 타입 사용 시 A100 대비 4배의 속도를 달성한다.
  * Sparsity 기능은 딥러닝 네트워크의 세밀한 Structured Sparsity을 활용해 Tensor Corre 연산 성능을 2배 향상시킨다.
* **DPX 명령어**
  * 새로운 DPX 명령어는 A100 GPU 대비 동적 프로그래밍 알고리즘을 최대 7배 빠르게 가속한다.
  * 예시로는 유전체 분석을 위한 Smith-Waterman 알고리즘, 동적 창고 환경에서 다수의 로봇 경로 최적화를 위한 Floyd-Warshall 알고리즘 등이 있다.
* **3배 더 빠른 IEEE FP64 & FP32**
  * IEEE FP64 및 FP32 연산 속도는 칩 간 기준 A100 대비 3배 빠르며, 이는 SM당 클럭당 성능이 2배 향상된 것과 추가된 SM 수 및 H100의 더 높은 클럭 속도 때문이다.
* **새로운 쓰레드 블록 클러스터**
  * 새로운 쓰레드 블록 클러스터 기능은 단일 SM 내의 쓰레드 블록보다 더 큰 수준의 지역성을 프로그래밍 방식으로 제어할 수 있게 해준다.
  * 이는 CUDA 프로그래밍 모델에 ‘쓰레드’, ‘쓰레드 블록’, ‘쓰레드 블록 클러스터’, ‘그리드’라는 새로운 계층 구조를 추가한다.
  * 클러스터는 여러 SM에 걸쳐 동시에 실행 중인 여러 쓰레드 블록이 동기화 및 협업적으로 데이터 접근과 교환을 할 수 있게 해준다.
* **분산 공유 메모리**
  * 분산 공유 메모리는 여러 SM의 공유 메모리 블록 간의 load, store, atomic 연산을 통한 직접 통신을 가능하게 한다.
* **새로운 비동기 실행**
  * 새로운 비동기 실행 기능에는 Tensor Memory Accelerator(TMA) 유닛이 포함되어 있으며, 이는 글로벌 메모리와 공유 메모리 간의 대규모 데이터 블록 전송을 효율적으로 처리한다.
  * TMA는 클러스터 내 쓰레드 블록 간 비동기 복사도 지원합니다. 또한 원자적 데이터 이동 및 동기화를 위한 새로운 비동기 트랜잭션 배리어도 제공된다.
### **Transformer 엔진**
* 새로운 Transformer 엔진은 소프트웨어와 NVIDIA Hopper 전용 텐서 코어 기술을 결합해 트랜스포머 모델의 학습 및 추론을 가속화한다.
* 이 엔진은 FP8과 16비트 연산 사이를 지능적으로 선택하고 각 계층에서 FP8과 16비트 간의 re-casting과 scaling을 자동으로 처리하여 A100 대비 최대 9배 빠른 AI 학습 속도, 최대 30배 빠른 AI 추론 속도를 제공한다.
### **HBM3 메모리 서브시스템**
* HBM3 메모리 서브시스템은 이전 세대 대비 거의 2배에 달하는 대역폭을 제공한다.
* H100 SXM5 GPU는 세계 최초로 HBM3 메모리를 탑재한 GPU이며, 업계 최고 수준인 3TB/sec 메모리 대역폭을 지원한다.
### **50MB L2 캐시 아키텍처**
* 50MB L2 캐시 아키텍처는 모델과 데이터셋의 큰 부분을 캐시에 저장해 반복 접근 시 HBM3로의 왕복을 줄인다.
### **2nd Gen MIG(Multi-Instance GPU)**
* 2세대 MIG(Multi-Instance GPU) 기술은 A100 대비 GPU 인스턴스당 약 3배의 연산 성능과 거의 2배의 메모리 대역폭을 제공한다.
* 이제 최초로 MIG 수준의 TEE(신뢰 실행 환경)를 포함한 Confidential Computing 기능도 제공한다.
* 최대 7개의 독립적인 GPU 인스턴스를 지원하며, 각 인스턴스는 전용 NVDEC 및 NVJPG 유닛을 포함하고 NVIDIA 개발자 도구와 연동되는 자체 성능 모니터 세트를 갖는다.
### **Confindential Computing**
* 새로운 Confidential Computing 기능은 사용자 데이터를 보호하고 HW 및 SW 공격으로부터 방어하며, 가상화 및 MIG 환경에서 가상 머신(VM) 간 격리와 보호 기능을 향상시킨다.
* H100은 세계 최초의 네이티브 Confidential Computing GPU를 구현하였으며, CPU와 함께 완전한 PCIe 속도로 TEE를 확장한다.
### **4th Gen NVIDIA NVLink**
* 4세대 NVIDIA NVLink는 all-reduce 연산에서 3배의 대역폭, 일반 대역폭은 이전 세대 NVLink 대비 50% 증가한다.
* 다중 GPU 간 입출력에서 PCIe Gen 5 대비 7배 빠른 총 900GB/sec의 대역폭을 제공한다.
### **3rd Gen NVSwitch**
* 3세대 NVSwitch 기술은 서버, 클러스터, 데이터 센터 환경에서 여러 GPU를 연결하기 위해 노드 내부 및 외부에 스위치를 포함한다.
* 노드 내부의 각 NVSwitch는 4세대 NVLink 링크를 위한 64개의 포트를 제공하여 다중 GPU 연결을 가속화한다.
* 총 스위치 처리량은 이전 세대의 7.2 Tbit/sec에서 13.6 Tbit/sec로 증가했다.
* 새로운 NVSwitch는 multicast 및 NVIDIA SHARP in-network reduction을 포함한 집합 연산을 하드웨어 가속한다.
### **NVLink Switch System**
* 새로운 NVLink 스위치 시스템 상호연결 기술과 3세대 NVSwitch 기반의 2단계 NVLink 스위치는 주소 공간의 격리와 보호 기능을 제공하여, 최대 32개 노드 또는 256개의 GPU를 2:1 테이퍼드 fat-tree 토폴로지로 연결할 수 있다.
* 이 구성은 57.6TB/sec의 all-to-all 대역폭과 FP8 Sparse AI 연산에서 1 엑사플롭(exaFLOP)에 달하는 연산 성능을 제공한다.
### **PCIe Gen 5**
* PCIe Gen 5는 총 128GB/sec 대역폭(양방향 각각 64GB/sec)을 제공하며, 이는 Gen 4 PCIe의 총 64GB/sec(32GB/sec씩 양방향)보다 두 배이다.
* PCIe Gen 5는 H100이 최고 성능의 x86 CPU, SmartNIC 또는 DPU와 인터페이스할 수 있도록 한다.
### **Others**
* 이외에도 강력한 확장성 향상, 지연 시간 및 오버헤드 감소, GPU 프로그래밍 간소화를 위한 다양한 기능이 추가되었다.

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
