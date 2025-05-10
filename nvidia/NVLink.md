# What is NVLink?
NVLink는 GPU와 CPU 간 또는 GPU와 GPU 간의 데이터 전송을 고속으로 수행하도록 설계된 고속 연결 인터페이스이며 단순한 물리적 연결이 아닌, 소프트웨어 프로토콜과 하드웨어 구현이 결합된 통신 기술이다.

# NVLink Bandwdith 계산


# NVLink Genersions 

| NVLink  | 1st Gen (2016) | 2nd Gen (2017)  | 3rd Gen (2020) | 4th Gen (2022)| 5th Gen (2024) | 
|:---|:---:|:---:|:---:|:---:|:---:|
| **Supported NVIDIA Architecture** | Pascal | Volta | Ampere | Hopper | Blackwell |
| **NVLink Bandwidth Per GPU (Bi-direction)** | 160GB/s| 300GB/s | 600GB/s | 900GB/s | 1800GB/s |
| **Max. # of sub-links Per GPU** | 4 | 6 | 12 | 18 | | 
| **NVLink Bandwidth Per Port** | 40GB/s | 50GB/s | 50GB/s | 50GB/s | |
| **Encoding** | x8@20Gbaud-NRZ | x8@25Gbaud-NRZ | x4@50Gbaud-NRZ | x2@50Gbaud-PAM4 | | 

# Reference
* [1] [The NVLink-Network Switch: NVIDIA's Switch Chip For High Communication-Bandwidth SuperPods](https://hc34.hotchips.org/assets/program/conference/day2/Network%20and%20Switches/NVSwitch%20HotChips%202022%20r5.pdf)
* [2] [What is NVLink?](https://blogs.nvidia.com/blog/what-is-nvidia-nvlink/)
* 
