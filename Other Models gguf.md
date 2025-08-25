## 小于2-4B的小模型一般对于CPU有优化，可以纯用CPU跑试试 <br> Small models less than 2-4B are generally optimized for the CPU, try offload to cpu to test speed.

## Gemma-270M（GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q8_0 | 292 MB | ≥ 1 GB |
| Q8_K_XL | 471 GB | ≥ 1 GB |
| Q8_0 | 543 GB | ≥ 1 GB |

## LFM2-700M (GGUF)

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q5_K_M | 538 MB | ≥ 1 GB |
| Q6_K | 612 MB | ≥ 1 GB |
| Q8 | 792 MB | ≥ 1~2 GB |
| F16 | 1.49 GB | ≥ 2 GB |

## LFM2-1.2B (GGUF)

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q5_K_M | 843 MB | ≥ 2 GB |
| Q6_K | 963 MB | ≥ 2 GB |
| Q8 | 1.25 MB | ≥ 2 GB |
| F16 | 2.34 GB | ≥ 3 GB |

## Qwen3-4B（GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 2.5 GB | ≥ 4 GB |
| Q5_K_M | 2.89 GB | ≥ 4 GB |
| Q6_K | 3.31 GB | ≥ 6 GB |
| Q8_0 | 4.28 GB | ≥ 6 GB |

--------
## Gemma3-27B（GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 16.5 GB | ≥ 20 GB |
| Q5_K_M | 19.3 GB | ≥ 24 GB |
| Q6_K | 22.2 GB | ≥ 24 GB |
| Q8_0 | 28.7 GB | ≥ 32 GB |
> gemma-3-27b-it-qat-q4_0 (17.2 GB) >>> 4bit version.

## Qwen3-32B（GGUF）

| 量化<br>Quantization | 模型文件大小<br>Model file size | 推荐显存（仅权重+余量）<br>Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 19.8 GB | ≥ 24 GB |
| Q5_K_M | 23.2 GB | ≥ 32* GB |
| Q6_K | 26.9 GB | ≥ 32 GB |
| Q8_0 | 34.8 GB | ≥ Work Station/工作站GPU/MAC/AMD AI MAX |

\* NO single card GPU Between 24-32GB (Till August 2025); only 5090 (32GB)*

