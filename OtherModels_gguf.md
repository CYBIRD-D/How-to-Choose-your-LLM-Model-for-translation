**Content**
1. **LLM VRAM USAGE LISTS**/**LLM 显存使用表**
2. **[GGUF Quantization Types & Relative Quality/GGUF 量化类型与相对质量](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/OtherModels_gguf.md#gguf-quantization-types--relative-qualityeng-ver-down-below--gguf-%E9%87%8F%E5%8C%96%E7%B1%BB%E5%9E%8B%E4%B8%8E%E7%9B%B8%E5%AF%B9%E8%B4%A8%E9%87%8F)**
- [**Nvidia GPU Specification**](Nvidia_GPU_Specification.md)

> Note: Some finetune models may have different size compared to their base models. </br>
> For translation task, quantizations above `Q5` usually no noticing quality loss. 

# LLM VRAM USAGE LISTS <br> LLM 显存使用表 
> 小模型一般对于**CPU有优化**，可以查看具体模型卡页面是否有优化/纯用CPU跑试试 </br>
 Small models are generally **optimized for the CPU**, check official model card/try offload to cpu to test speed.

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

### Hemers-4-70B (Llama 3.1 70B) (GGUF)

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

---------
## GGUF quantization types & relative quality(Eng ver down below) <br> GGUF 量化类型与相对质量 

> 注：质量为**相对 FP16 的总体逼近**与社区常用基准（如困惑度/客观评测）综合判断的**经验级**分档；
> 同一量化在不同模型/任务上可能有差异。
> `_K` 为更先进的 K 类量化；`_S/_M` 为不同“混合策略”，一般 `_M` 质量高于 `_S`。

| 量化类型 | 理论 bpw* | 相对质量（对比 FP16） | 典型使用场景 / 建议 | 备注 |
|---|---:|---|---|---|
| **Q8_0** | ≈ 8.0 | 最高（接近 FP16） | VRAM 充足、要尽量贴近原精度或做严谨评测 | 属于“旧法（legacy）”，但质量最高的量化档，相较FP16基本没有质量下降 |
| **Q6_K** | 6.5625 | 很高（接近 Q8_0） | 追求高质量且希望显存更省 | K-Quant，质量/体积效率优于同位数的旧法 |
| **Q5_K_M** | 5.5 | 较高 | 5-bit 档的通用首选；综合部署的“甜点位” | `_M` 较 `_S` 更注重质量 |
| **Q5_0** | ≈ 5.0 | 中等—较高 | 仅在兼容旧工作流时考虑(相对更高量化） | 旧法，质量通常逊于 Q5_K_ |
| **Q4_K_M** | 4.5 | 中等（**4-bit 中**质量最佳之一） | 显存较紧张但仍需可用质量；常见平衡点 | 社区普遍认为 **4-bit**内首选|
| **Q4_K_S** | ≈ 4.5 | 中等偏下（低于 `_M`） | 更追求速度/更小体积时的 4-bit 选项 | `_S` 为更激进混合，质量略降 |
| **Q4_0** | ≈ 4.0 | 中等—较低 | 仅做兼容/对比用途 | 旧法（legacy），质量较低，通常不再推荐* |
| **Q3_K_M** | 3.4375 | 较低 | 极限内存或边缘设备权衡 | 质量明显劣化，不推荐 |

具体技术文章 https://gist.github.com/Artefact2/b5f810600771265fc1e39442288e8ec9

\* *bpw（bits per weight）为官方/文档给出的近似或精确数值；部分旧法（如 Q4_0/Q5_0）不明确给出额外开销，表中以“≈”表示。*</br>
\* *特殊情况：Gemma 3 12B Instruct QAT 虽为q4_0量化，但量化感知训练（Quantization-Aware Training, QAT）使其质量和速度远超q4档位</br> 

-------

> Note: “Quality” here is an **experience-based** tiering of overall closeness to FP16 + common community metrics (e.g., perplexity/objective evals).
> The same quant level can vary by model/task.
> `_K` denotes newer K-quant; `_S/_M` are mixed strategies—`_M` is usually higher quality than `_S`.

| Quantization | Theoretical bpw* | Relative quality (vs FP16) | Typical use / advice | Notes |
|---|---:|---|---|---|
| **Q8_0** | ≈ 8.0 | Highest (near FP16) | When VRAM is plenty and you want FP16-like fidelity or rigorous evals | “Legacy” method but the highest-quality quant; negligible drop vs FP16 |
| **Q6_K** | 6.5625 | Very high (near Q8_0) | Aim for very high quality while saving some VRAM | K-Quant; better quality/size than same-bit legacy |
| **Q5_K_M** | 5.5 | High | A great 5-bit default; deployment “sweet spot” | `_M` prioritizes quality over `_S` |
| **Q5_0** | ≈ 5.0 | Medium–High | Consider only for old workflows | Legacy; usually worse than Q5_K_* |
| **Q4_K_M** | 4.5 | Medium (one of the best among many 4-bit options) | Tight VRAM yet usable quality; common balance | Often the 4-bit sweet spot |
| **Q4_K_S** | ≈ 4.5 | Medium (lower than `_M`) | When you need speed/smaller size in 4-bit | More aggressive mix, slight quality drop |
| **Q4_0** | ≈ 4.0 | Medium–Low | Compatibility/contrast only | Legacy; generally not recommended* |
| **Q3_K_M** | 3.4375 | Low | Low memory/edge devices | Noticeable degradation; not recommended |

Further reading: https://gist.github.com/Artefact2/b5f810600771265fc1e39442288e8ec9

\* *bpw (bits per weight) are approximate/official numbers; some legacy formats (Q4_0/Q5_0) have extra overhead not precisely specified—shown as “≈”.*</br>
\* *Special case: Gemma 3 12B Instruct QAT is q4_0, but quantization-aware training (QAT) makes its quality/speed far above typical q4.*</br> 
