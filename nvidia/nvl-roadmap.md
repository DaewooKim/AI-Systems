# Hopper (2022)
## GH200 NVL32
### 시스템 구성
NVIDIA GH200 NVL32는 하이퍼스케일 데이터센터를 대상으로 NVLink를 통해 연결된 **NVIDIA GH200 Grace Hopper 슈퍼칩**을 위한 랙 스케일 레퍼런스 디자인이다.
NVIDIA GH200 NVL32는 NVIDIA MGX 섀시(chassis) 디자인과 호환되는 16개의 듀얼 NVIDIA Grace Hopper 서버 노드를 지원하며, 수냉식 냉각을 통해 컴퓨팅 밀도와 효율성을 극대화할 수 있다.
- **16x Dual GH200 Compute Trays**
- **9x NVLink Switch Trays**
![image](https://developer-blogs.nvidia.com/wp-content/uploads/2023/11/nvidia-gh200-nvl32-diagram-front-back_-1536x1166.png)

### Key Features
- **일관된 NVLink-C2C 메모리 공간**
  - GH200은 **NVLink-C2C**를 통해 CPU(Grace)와 GPU(Hopper) 간 **coherent memory address space**를 구성
  - **LPDDR5X + HBM3e** 통합 메모리 구조로 **고대역폭 + 저전력** 시스템 제공
  - 모델 프로그래밍 간소화 및 전체 시스템 성능 균형 최적화

- **NVLink를 통한 멀티 노드 메모리 공유**
  - **NVLink 패시브 구리 케이블**로 각 GH200 노드 간 직접 연결
  - 총 **32개 GH200 노드 → 32 × 624GB = 19.5TB**의 NVLink addressable memory 공유

- **NVLink Switch 시스템 구성**
  - **3세대 NVSwitch 칩**이 포함된 **9개 NVLink 스위치** 사용
  - **Fat-tree 토폴로지**로 32개의 GH200 GPU를 완전 연결 (fully connected)
  - 모든 GPU 간 **고속 직접 연결** 지원 → 낮은 지연, 높은 대역폭

- **대규모 시스템 확장성**
  - **400 Gb/s InfiniBand** 또는 **Ethernet**으로 외부 네트워크와 연동 가능
  - 대규모 AI 슈퍼컴퓨터로 확장 시에도 **성능 및 에너지 효율성 극대화**

- **소프트웨어 생태계 지원**
  * **NVIDIA HPC SDK**, **CUDA**, **CUDA-X**, **Magnum IO** 등 지원
  * **3,000개 이상의 GPU 애플리케이션** 가속 가능

### NVIDIA GH200 NVL2
NVIDIA GH200 NVL2는 단일 노드에서 NVLink C2C 기술을 통해 두 개의 GH200 Superchip을 연결하였다. GH200 NVL2는 Grace CPU 2개와 Hopper GPU 2개를 결합하여 단일 노드에서 8 Peta FLOPS의 AI 성능을 제공한다.

![image](https://developer-blogs.nvidia.com/wp-content/uploads/2024/09/GH200-NVL2-Top-Down-blog-1024x768.jpg)

- **GH200 NVL2 설계 목표**
  - 개발자가 시스템 메모리를 쉽게 사용하고 접근할 수 있도록 설계됨 → 개발자는 명시적인 메모리 관리 대신 알고리즘에 집중할 수 있음
- **Unified Memory Model**
  - GH200을 NVLink-C2C을 사용하여 Unified Memory Model을 구현함
  - CPU와 GPU가 동일한 주소 공간을 공유하며, 데이터 전송 속도는 PCIe Gen 5 시스템의 7배
  - Memory oversubscription, on-demand paging, data consistency 등을 원활하게 처리 가능하게 함
- **High-bandwidth access**
  - NVLink-C2C는 최대 900 GB/s 대역폭을 제공, 기존 서버 아키텍처보다 7배 빠름
  - GPU가 CPU 메모리를 직접 사용하여 메모리 복사 오버헤드 감소
- **Interconnect**
  - CPU-GPU NVLink-C2C: 900 GB/s
  - CPU-CPU NVLink-C2C: 600 GB/s
  - GPU-GPU NVLink: 900 GB/s
- **Memory Coherency**
  - ATS(주소 변환 서비스) 메커니즘을 통해 GH200 NVL2는 일관된 메모리 모델을 지원
  - CPU와 GPU에서 모두 원자적 연산(공유 메모리에 대한 읽기-수정-쓰기 작업)을 지원하며, 이는 명시적인 메모리 관리 및 복사의 필요성을 줄임 
- **Oversubscription of GPU Memory**
  - GH200 아키텍처는 NVIDIA Grace CPU 메모리를 고대역폭으로 사용하여 GPU 메모리를 초과 구독할 수 있게 설계됨
  - 각 Grace Hopper 슈퍼칩은 최대 480GB의 LPDDR5X와 144GB의 HBM3e를 제공, 총 1248GB의 메모리를 지원. 이는 HBM만 사용하는 시스템에 비해 훨씬 더 많은 메모리를 접근할 수 있게 함
  - GPU가 CPU 메모리에 접근함으로써 메모리 복사의 필요성이 더욱 줄어듬
- **Accelerated Bulk Transfers**
  - NVIDIA Hopper DMA는 NVLink-C2C와 지원하여 페이지 가능 메모리의 대량 전송을 가속화
  - DMA는 호스트와 디바이스 간의 메모리 복사 오버헤드를 줄여주는 기술로, 시스템 내 메모리 이동을 효율적으로 처리

# Blackwell (2024)
## GB200 NVL72


# Blackwell Ultra (2025)
## GB300 NVL72
* GB300 NVL72 대비 연산 성능: 1.5x, 메모리 용량: 1.5x


# Vera Rubin (2026)
## Vera Rubin NVL144
- GB300(Blackwell Ultra) NVL72 대비 연산 성능: 3.3x, 메모리 용량: 1.6x, NVLink 성능: 2x
- **(Note) Blackwell 제품군은 칩 개수로 작명하였으나, Rubin부터는 GPU die의 개수로 작명**


# Rubin Ultra (2027)
## Rubin Ultra NVL576
- GB300(Blackwell Ultra) NVL72 대비 연산 성능: 14x, 메모리 용량: 8x, NVLink 성능: 12x


# Feynman (2028)

# NVL Roadmap
|  |  2023       | 2024        | 2025        | 2026         | 2027         | 
|:---|:---:|:---:|:---:|:---:|:---:|
| **NVL**  | GH200 NVL32 | GB200 NVL72 | GB300 NVL72 | VR200 NVL144 | VR300 NVL576 |
| **# of GPU Packages** | 32x GH200 | 36x GB200 | 36x GB300 | 72x VR200 | 144x VR300 |
| **HBM Size** | 32x144GB=4.6TB | 36x192GB=13.8TB | 72x288GB=20.7TB | 72x288GB=20.7TB  | 144x1024GB=147TB |
| **HBM BW** | 32x4.9TB/s=157TB/s | 72x8TB/s=576TB/s | 72x8TB/s=576TB/s | 72x13TB/s=936TB/s | 144x32TB/s=4608TB/s |
| **LPDDR5 Size** | 32x480GB=15.4TB | 36x480GB=17.3TB | 40TB | 75TB | 365TB |
| **FLOPS(FP16)** | 32P | 180P | 180P | - | - |
| **FLOPS(FP8)** | 64P | 360P | 360P | 1200P  | 5000P |
| **FLOPS(INT8)** | 64P | 360P | 23P | - | - |
| **FLOPS(FP4)** | - | 720P | 1080P | 3600P | 15000P |
| **NV Switch System**| Gen3-64 Port/NVSwitch, 9x L1 NVSwitch Tray | Gen3-64 Port/NVSwitch, 9x L1 NVSwitch Tray | Gen3-64 Port/NVSwitch, 9x L1 NVSwitch Tray | - | - |
| | | | | | |
| | | | | | |
| | | | | | |







# Reference
* [One Giant Superchip for LLMs, Recommenders, and GNNs: Introducing NVIDIA GH200 NVL32](https://developer.nvidia.com/blog/one-giant-superchip-for-llms-recommenders-and-gnns-introducing-nvidia-gh200-nvl32)
* [NVIDIA GH200 Grace Hopper Superchip Delivers Outstanding Performance in MLPerf Inference v4.1](https://developer.nvidia.com/blog/nvidia-gh200-grace-hopper-superchip-delivers-outstanding-performance-in-mlperf-inference-v4-1/)
* [NVIDIA Grace Hopper Superchip Architecture In-Depth](https://resources.nvidia.com/en-us-grace-cpu/nvidia-grace-hopper-2)




