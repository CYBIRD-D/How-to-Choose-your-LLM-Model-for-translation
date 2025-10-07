# LLM VRAM USAGE LISTS <br> LLM 显存使用表 
小模型一般对于**CPU有优化**，可以纯用CPU跑试试 <br> Small models are generally **optimized for the CPU**, try offload to cpu to test speed.

## CPU Only or less than 2/3G VRAM

### Gemma3-270M（GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q8_0 | 292 MB | ≥ 1 GB |
| Q8_K_XL | 471 MB | ≥ 1 GB |
| F16 | 543 MB | ≥ 1 GB |

### LFM2-700M (GGUF)

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q5_K_M | 538 MB | ≥ 1 GB |
| Q6_K | 612 MB | ≥ 1 GB |
| Q8 | 792 MB | ≥ 1~2 GB |
| F16 | 1.49 GB | ≥ 2 GB |

### LFM2-1.2B (GGUF)

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q5_K_M | 843 MB | ≥ 2 GB |
| Q6_K | 963 MB | ≥ 2 GB |
| Q8 | 1.25 GB | ≥ 2 GB |
| F16 | 2.34 GB | ≥ 3 GB |

-----------

## 4G~8G VRAM

### Qwen3-4B（GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 2.5 GB | ≥ 3~4 GB |
| Q5_K_M | 2.89 GB | ≥ 4 GB |
| Q6_K | 3.31 GB | ≥ 4~6 GB |
| Q8_0 | 4.28 GB | ≥ 6 GB |


### Gemma-3n-E4B-it (7B±）*（GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 4.24 GB | ≥ 6 GB |
| Q5_K_M | 4.95 GB | ≥ 6 GB |
| Q6_K | 5.7 GB | ≥ 6~8 GB |
| Q8_0 | 7.35 GB | ≥ 8 GB |

\* Good for CPU


### Qwen3-8B（GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 5.03 GB | ≥ 6 GB |
| Q5_0 | 5.72 GB | ≥ 7~8 GB |
| Q5_K_M | 5.85 GB | ≥ 7~8 GB |
| Q6_K | 6.73 GB | ≥ 8 GB |
| Q8_0 | 8.71 GB | ≥ 10~12 GB |

----------

## 12~16G VRAM

### Gemma-3-12b-it（GGUF）
| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 7.3 GB | ≥ 10~12 GB |
| Q5_K_S | 8.23 GB | ≥ 12 GB |
| Q5_K_M | 8.44 GB | ≥ 12 GB |
| Q6_K | 9.66 GB | ≥ 12~16 GB |
| Q8_0 | 12.5 GB | ≥ 16 GB |


### Qwen3-14B（GGUF）
| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 9.00 GB | ≥ 11~12 GB |
| Q5_0 | 10.3 GB | ≥ 12 GB |
| Q5_K_M | 10.5 GB | ≥ 12 GB |
| Q6_K | 12.1 GB | ≥ 14~16 GB |
| Q8_0 | 15.7 GB | ≥ 18~20 GB |

--------
## 20G VRAM and Above

### Gemma3-27B-it（GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 16.5 GB | ≥ 20 GB |
| Q5_K_M | 19.3 GB | ≥ 24 GB |
| Q6_K | 22.2 GB | ≥ 24 GB |
| Q8_0 | 28.7 GB | ≥ 32 GB |
> gemma-3-27b-it-qat-q4_0 (17.2 GB) （better）>>> usual 4bit version.

### Qwen3-32B（GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 19.8 GB | ≥ 24 GB |
| Q5_K_M | 23.2 GB | ≥ 32* GB |
| Q6_K | 26.9 GB | ≥ 32 GB |
| Q8_0 | 34.8 GB | ≥ Work Station(工作站)/Mac/AMD AI MAX |

\* NO single card GPU Between 24-32GB (Till August 2025); only 5090 (32GB)* (**NOT INCLUDED DIY VERSION**)

----------
## For Mac (M series Pro/Max/Ultra) <br> NVIDIA WORKSTATION <br> GPU Server

### Hermers-4-70B (Llama 3.1 70B) (GGUF)

| 量化<br>Quantization | 模型文件大小<br>Model file size | 
|---|---:|
| Q4_K_M | 42.5 GB | 
| Q5_K_M | 49.9 GB | 
| Q6_K | 57.9 GB |
| Q8_0 | 75 GB |

### GLM-4.5-Air (110B) （GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 
|---|---:|
| Q4_K_M | 72.9 GB | 
| Q5_K_S | 78.3 GB | 
| Q5_K_M | 83.4 GB | 
| Q6_K | 99 GB |
| Q8_0 | 117 GB |

### Qwen3-235B-A22B （GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 
|---|---:|
| Q4_K_M | 142 GB | 
| Q5_K_M | 167 GB | 
| Q6_K | 193 GB |
| Q8_0 | 250 GB |

### GLM-4.6 （357B) （GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 
|---|---:|
| Q4_K_M | 216 GB | 
| Q5_K_S | 246 GB | 
| Q5_K_M | 253 GB | 
| Q6_K | 293 GB |
| Q8_0 | 379 GB |


