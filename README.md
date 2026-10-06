# CUDA Path Tracer

CMPE214 project: a CUDA path tracer optimized step by step and profiled with Nsight.

## Benchmark platform

All official benchmark numbers are collected on **Ubuntu 24.04 LTS**, so differences come from the GPU and not the OS.

| Owner | GPU | Architecture | Compute capability |
|---|---|---|---|
| Eugene | RTX 2070 Super | Turing (RT cores gen 1) | sm_75 |
| Harsha | RTX 5070 | Blackwell (RT cores gen 4) | sm_120 |

Requirements on both machines:
- CUDA Toolkit 12.8 or newer (needed for sm_120)
- NVIDIA driver 570 or newer; the RTX 5070 requires the open kernel modules (`-open` driver packages)
