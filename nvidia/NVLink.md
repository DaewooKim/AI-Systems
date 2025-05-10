# What is NVLink?
NVLink는 GPU와 CPU 간 또는 GPU와 GPU 간의 데이터 전송을 고속으로 수행하도록 설계된 고속 연결 인터페이스이며 단순한 물리적 연결이 아닌, 소프트웨어 프로토콜과 하드웨어 구현이 결합된 통신 기술이다.
NVLink의 주요 이점은 PCIe를 크게 능가하는 대역폭에 있다. 4세대 NVLink는 lane 1개당 대역폭이 100Gbps로 PCIe Gen5의 대역폭인 32Gbps와 비교해 3배가 넘는다.

# NVLink Bandwdith 계산


# NVLink Generations 

| NVLink  | 1st Gen (2016) | 2nd Gen (2017)  | 3rd Gen (2020) | 4th Gen (2022)| 5th Gen (2024) | 
|:---|:---:|:---:|:---:|:---:|:---:|
| **Supported NVIDIA Architecture** | Pascal | Volta | Ampere | Hopper | Blackwell |
| **NVLink Bandwidth Per GPU (Bi-direction)** | 160GB/s| 300GB/s | 600GB/s | 900GB/s | 1800GB/s |
| **Max. # of sub-links Per GPU** | 4 | 6 | 12 | 18 | | 
| **NVLink Bandwidth Per Port** | 40GB/s | 50GB/s | 50GB/s | 50GB/s | |
| **Encoding** | x8@20Gbaud-NRZ | x8@25Gbaud-NRZ | x4@50Gbaud-NRZ | x2@50Gbaud-PAM4 | | 

![image](https://developer-blogs.nvidia.com/wp-content/uploads/2022/08/NVLink-generations-1.png)

# NVLink-Enable Server Generations
- **V100**
  - 2nd Gen NVLink + 1st Gen NVSwitch
  - 서버 내 Multi-GPU 간 High Bandwidth 및 All-to-All 연결 제공
- **A100**
  - 3rd Gen NVLink + 2nd Gen NVSwitch
- **H100**
  - 4st Gen NVLink + 3rd Gen NVSwitch

|   | DGX-1 (2016) | DGX-2 (2018)  | DGX A100 (2020) | DGX H100 (2022)|
|:---|:---:|:---:|:---:|:---:|
| **Bisection BW** | 140GB/s | 2.4TB/s | 2.4TB/s | 3.6TB/s |
| **AllReduce BW** | 40GB/s | 75GB/s | 150 GB/s | 450 GB/s |


![image](https://developer-blogs.nvidia.com/ko-kr/wp-content/uploads/sites/5/2022/11/NVLink-all-to-all-connectivity-1.png)

# NVSwitch: 

# NVLink SHARP(Scalable Hierarchical Aggregation and Reduction Protocol)



# Reference
* [1] [The NVLink-Network Switch: NVIDIA's Switch Chip For High Communication-Bandwidth SuperPods](https://hc34.hotchips.org/assets/program/conference/day2/Network%20and%20Switches/NVSwitch%20HotChips%202022%20r5.pdf)
* [2] [What is NVLink?](https://blogs.nvidia.com/blog/what-is-nvidia-nvlink/)
* [3] [NVIDIA GTC 2025 – Built For Reasoning, Vera Rubin, Kyber, CPO, Dynamo Inference, Jensen Math, Feynman](https://semianalysis.com/2025/03/19/nvidia-gtc-2025-built-for-reasoning-vera-rubin-kyber-cpo-dynamo-inference-jensen-math-feynman/#the-reasoning-token-explosion)
