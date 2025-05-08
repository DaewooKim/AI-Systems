# Hopper (2022)
## GH200 NVL32
### Overview
NVIDIA GH200 NVL32는 하이퍼스케일 데이터센터를 대상으로 NVLink를 통해 연결된 **NVIDIA GH200 Grace Hopper 슈퍼칩**을 위한 랙 스케일 레퍼런스 디자인이다.
NVIDIA GH200 NVL32는 NVIDIA MGX 섀시(chassis) 디자인과 호환되는 16개의 듀얼 NVIDIA Grace Hopper 서버 노드를 지원하며, 수냉식 냉각을 통해 컴퓨팅 밀도와 효율성을 극대화할 수 있다.
- **시스템구성**
  * 16x Dual GH200 Compute Trays
  * 9x NVLink Switch Trays
![image](https://developer-blogs.nvidia.com/wp-content/uploads/2023/11/nvidia-gh200-nvl32-diagram-front-back_-1536x1166.png)

### NVIDIA GH200 NVL2



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
* [LLM, 추천 시스템 및 GNN을 위한 하나의 거대한 슈퍼칩: NVIDIA GH200 NVL32](https://developer.nvidia.com/ko-kr/blog/one-giant-superchip-for-llms-recommenders-and-gnns-introducing-nvidia-gh200-nvl32/)
* 




