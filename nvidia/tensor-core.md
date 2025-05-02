# Tensor Core Overview

## Tensor Core 정의
* V100의 Tensor Core는 행렬 곱셈 및 누산(MMA, Matrix Multiply-Accumulate) 전용 연산 유닛으로, **최대 125 TFLOPS**의 성능을 제공하며, 딥러닝 **학습과 추론**에 최적화되어 있다.
  
## 구성
* V100 GPU에는 총 **640개의 Tensor Core**가 포함되어 있으며, 각 SM(Stream Multiprocessor)당 8개 내장되었다.

## 연산 구조
* 각 Tensor Core는 **4×4×4 행렬 연산**을 수행하며, `D = A × B + C` 형태의 계산을 처리한다.
* 입력 행렬 A, B는 **FP16**, 누산 행렬 C, D는 **FP16 또는 FP32** 형식을 지원한다.

![image](https://developer-blogs.nvidia.com/wp-content/uploads/2017/05/image4-625x155.png)

* 각 Tensor Core는 **클럭당 64개의 혼합정밀도 (FP16 입력 곱셈 + FP32 누산) floating point FMA 연산**을 수행할 수 있다.
* FP16 곱셈 결과는 **Full Precsion**의 결과로 계산되며, 이 결과는 동일한 **Dot Product** 내의 다른 항들과 함께 FP32로 누산된다. **(4x4x4 행렬 곱셈 연산)**
![image](https://developer-blogs.nvidia.com/wp-content/uploads/2017/05/image11.png)

## 성능 향상
* SM 하나는 **클럭당 총 1024개 연산** 수행하며 Pascal 대비 8배 향상시켰다.
* **V100**은 **Pascal P100** 대비 처리량이 12배 증가하였다.

* FP16 연산을 사용하지만 결과는 **FP32 정밀도로 누산**, 정확도와 성능을 모두 확보하였다.

## CUDA 연동
* Tensor Core는 **CUDA C++의 WMMA API**를 통해 warp 단위 행렬 연산으로 접근 가능하다.
* 프로그래머는 **행렬 로드, 곱셈 및 저장 연산을 전용 API**로 효율적으로 구현 가능하다.

## 전력 최적화
* 클럭 게이팅(clock gating)을 적극 활용하여 전력 효율성을 높인다.

