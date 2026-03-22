# Inside NVIDIA Groq 3 LPX

## 왜 LPX 같은 새로운 추론 가속기가 필요한가?
추론은 Throughput-oriented 추론과 Latency-oriented interactive 추론

### Throughput-oriented inference
- Tokens/GPU, Tokens/Watt, 전체 비용 효율, 높은 utilization이 중요
- 일괄 문서 처리, 컨텐츠 검토, 컨텐츠 삽입, 미디어 파이프라인

### Latency-oriented interactive inference
- TTFT(Time-To-First-Token), Token/s/user, Tail Latency
- Coding Assistant, Chatbot, Voice Assistant, Copilot, Interactive Agent

## Interactive 추론이 점점 더 어려워지는 이유
- Low latency
  - 사용자가 서비스 품질을 평가하는 직접 기준
- 더 긴 추론 출력
  - 모델이 더 긴 추론 과정을 생성할수록 요청의 더 큰 부분이 순차적인 token generation으로 이동
- Prefix Caching
  - 공통 prompt state를 재사용하면 prefill cost는 줄어들 수 있음
  - 그만큼 상대적으로 request-specific decode 비중이 커집니다. 즉, 남은 decode를 더 빨리 처리해야 하는 압박이 커짐
- Longer Contexts
  - context가 길어질수록 self-attention은 계산보다 data movement와 memory bandwidth에 더 크게 제약받게 됨

## Agentic AI가 왜 새로운 추론 구조를 요구하는가?
- 대화형 디코딩에서는 많은 작업이 매우 작은 배치 크기로 실행되므로 지연 시간이 스톨(Stall), 경합, 지터에 훨씬 더 민감
- agentic system은 단일 질의-응답이 아니라 inference → retrieval → tool use → reasoning의 반복 루프를 가짐
- 이 구조에서는 latency가 단계마다 누적되기 때문에, 단순 평균 처리량보다 stable per-token performance와 tail-latency behavior가 매우 중요해짐

![](https://developer-blogs.nvidia.com/wp-content/uploads/2026/03/Heterogenous-AI.gif)

## Vera Rubin NVL72 & LPX의 역할 분담

### Vera Rubin NVL72
- Prefill, Decode Attention, Long-context 처리, High Concurrency Serving을 담당

### LPX
- Decode 내부의 Latency-sensitive Execution Path 가속. 특히 FFN과 MoE Expert Execution 같은 구간

![](https://developer-blogs.nvidia.com/wp-content/uploads/2026/03/LPX05-Rubin_GPU_and_Groq_3_LPU.webp)

### Decode 단계

- Attention-FFN Disaggregation
  - 디코딩 내에서 Attention과 FFN을 분리하고 각 토큰에 대한 중간 Activation을 교환하여 각 엔진이 가장 적합한 루프 부분을 실행
  - GPU: 누적된 KV 캐시를 활용해 전체 컨텍스트 어텐션과 같이 처리량과 대용량 메모리가 가장 중요한 디코딩 작업을 처리
  - LPX: Sparse MoE expert FFN과 다른 pointwise operation과 같은 Latency-sensitive execution을 가속 

- Rack 규모 이상에서 LPX는 긴밀하게 조정된 컴퓨팅 단위로 작동하도록 설계되어 조정 오버헤드를 최소화하고 Jitter를 줄임

![](https://developer-blogs.nvidia.com/wp-content/uploads/2026/03/Decode-Loop-1536x792.png)

### LPX를 활용한 Speculative Decoding


## LPX의 기본 Specs

### LPX Rack-scale System

- LPX 시스템은 256개의 상호 연결된 NVIDIA Groq 3 LPU accerators를 중심으로 구성됨
- Rubin과 LPX를 결합하면 up to 35x higher inference throughput per megawatt를 제공

- Specs
  - AI inference compute: 315 PFLOPS
  - Total SRAM capacity: 128 GB
  - On-chip SRAM bandwidth: 40 PB/s
  - Scale-up density: 256 chips
  - Scale-up bandwidth: 640 TB/s
 
### 

### 
