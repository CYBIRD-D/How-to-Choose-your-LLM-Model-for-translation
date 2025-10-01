## ENGLISH | [Simplifie-Chinese 简体中文](Model_Speed.md)

Use LM STUDIO as an example

<p align="center">
  <img src="./LM%20STUDIO.png" width="800" alt="LM Studio screenshot">
</p>

### **Context Length** </br>
“Context length” means the maximum number of **tokens** the model can “see” in a single forward/decoding pass (input + intermediate cache + generated history).

A token ≠ a character/word. A rough rule of thumb in English: 1 token ≈ 4 characters ≈ 0.75 words (varies by language). Going over the limit will result in truncation or an error.
- The larger the number, the longer the text it can handle; but it significantly increases VRAM/RAM and compute. Exceeding the model’s trained or implemented maximum window may also lead to abnormal outputs.

- The larger the model, the more VRAM/RAM the context requires; the longer the window, the more VRAM/RAM it needs. </br>
- As the used context length increases, model capability gradually degrades; beyond the trained/supported window, capability can drop sharply.
-----

### **GPU Offload** </br>
- Specifies how many layers’ weights and computation are offloaded to the GPU    
  (llama.cpp uses `n_gpu_layers` / `-ngl`; setting ≥ the total number of layers usually means “offload as much as possible to GPU”).

- Putting more layers on GPU can significantly boost throughput, but it is limited by VRAM; any excess still runs on the CPU.
------

### **CPU Thread Pool Size** </br>
In LM Studio, this is the number of CPU worker threads allocated to model inference. In SDK/API it corresponds to the `cpuThreads` field (an inference-time parameter, not a load-time parameter).
- **CPU-only inference**: more threads allow more parallelism in GGML/llama.cpp ops, but you’ll quickly hit **memory bandwidth** limits; further increases bring diminishing returns or even slowdowns.

- **With GPU offload (Vulkan/CUDA)**: many weights compute on the GPU, but some ops and sampling still run on the CPU, so `cpuThreads` still matters; however, the CPU is no longer the sole bottleneck, and setting it too high may yield smaller or even negative gains (as reported by the community).
> Set it with respect to the **number of physical cores** (not logical threads/hyper-threads). A value near the physical core count or system suggestion is usually fine.
------

### **Evaluation Batch Size (n_batch)** </br>
**Definition**: Evaluation batch size / `evalBatchSize` is how many input tokens are fed to the model and computed **in parallel** in one forward pass.
- Increasing it typically better utilizes parallel compute, improving **throughput/prefill speed**; the trade-off is higher VRAM/RAM use. Semantics/results do not change with batch size—only speed and resource usage do.

- **Relation to llama.cpp**: LM Studio is based on llama.cpp. In llama.cpp, `n_batch` (logical batch size) ≈ `evalBatchSize` here. The backend may further split into **`n_ubatch` (micro-batches)** to fit VRAM/RAM, so even if you set `evalBatchSize` high, it may still run in chunks. Hence **raising it doesn’t necessarily yield linear speedups**.
> Start conservatively (512 is a safe starting point on many machines). Watch tokens/s (generation speed) and responsiveness, then double gradually (512→1024→2048…).

--------

### **RoPE Frequency Base**  </br>
Adjusts the base frequency of Rotary Position Embeddings (RoPE). This advanced setting affects how positional information is encoded. Increasing it is sometimes used to maintain stability at longer contexts (the exact limit depends on model/implementation).
- **If you’re not sure, don’t touch this!**
-------

### **RoPE Frequency Scale** </br>
A scaling factor for RoPE; changes the “granularity” of positional encoding. Often used in tandem with the above to extend the effective context or for long-context experiments.
- **If you’re not sure, don’t touch this!**
-------

### **Offload KV Cache to GPU Memory** </br>
Keeps the K/V cache resident in GPU VRAM (instead of system RAM/CPU). This avoids PCIe round-trips when attention reads K/V, usually reducing CPU/RAM pressure and significantly speeding up long-context runs, at the cost of more VRAM usage.
- In v0.3.9, LM Studio exposed this both as a model-load option and a toggle in the GPU settings panel.
------

### **Keep Model in Memory** </br>
Prevents an already loaded model from being evicted from system memory, yielding **faster subsequent calls and a snappier experience**; the trade-off is higher RAM usage.

---------
### **Try mmap()** </br>
Memory-maps weights from disk on demand, which often **speeds up loading and reduces resident memory**; however, if the model exceeds available RAM, frequent page faults can cause slowdowns.
- LM Studio provides this toggle; llama.cpp uses mmap by default and allows disabling it as needed.

--------
### **Seed** </br>
Controls randomness in sampling to reproduce results; setting a fixed value makes the same prompt produce identical outputs under the same parameters.

--------
### **Flash Attention (experimental/optional)** </br>
**Definition**: Flash Attention (FA) is an I/O-aware, **exact** attention implementation. By tiling Q·Kᵀ → softmax → ·V on the GPU and keeping intermediates in on-chip SRAM, it drastically reduces HBM (VRAM) traffic and intermediate activations, thus significantly accelerating long sequences/high throughput without approximation.
- Official docs: **Enabling it can reduce memory usage and speed up generation, especially for long sequences.**

- FA is available on CUDA and Metal backends; community discussions also confirm this (SYCL/ROCm are still in progress/partial). Therefore, NVIDIA and Mac (M-series) users benefit the most.
------
### **K Cache Quantization Type (experimental)** </br>
Selects the storage precision/quantization format for the K (Key) cache in attention (corresponds to `type_k`/ggml type in implementations). Quantizing the KV cache can noticeably reduce RAM/VRAM usage with minimal quality loss and sometimes speed benefits; availability and stability vary by backend/hardware.
- Because model quantization is involved, **if you’re not sure, don’t touch this**.
-------
### **V Cache Quantization Type (experimental)** </br>
Same idea but for the V (Value) cache (implementation field `type_v`). Quantizing both K and V caches is often used for long contexts or small-VRAM GPUs to expand the usable window and lower memory.
- Because model quantization is involved, **if you’re not sure, don’t touch this**.
---------
### Speculative Decoding (推测/投机解码) [LM STUDIO Intro](https://lmstudio.ai/blog/lmstudio-v0.3.10)  
In LM Studio, Speculative Decoding accelerates inference by running two models: a smaller, faster **draft model** first proposes a span of candidate tokens in parallel, then the larger **main model** quickly verifies them and accepts only those that match what it would have generated anyway—thus **improving speed without changing the output distribution/quality**.
- The draft model predicts several upcoming tokens at once; the main model computes distributions at those positions in parallel. If they match, the whole span is accepted; otherwise it rolls back to the first mismatch and continues normal decoding. After accepting the last draft token, the main model emits **one extra token** to ensure an unbiased distribution.
  - **Compatibility**: the draft model should share a sufficiently consistent vocabulary/tokenizer with the main model. LM Studio auto-checks this and indicates valid pairings in the UI.
  
- **Pairing tips**: Prefer a smaller model from the **same family** as the draft, for example:  
Llama 3.1 8B ↔ Llama 3.2 1B; Qwen 2.5 14B ↔ Qwen 2.5 0.5B  

- Size ratios (from LM Studio’s guidance)

| Main model size | Suggested draft size |
|---|---:|
| 3–7B | ≤ 1B |
| 14B | ≤ 3B |
| 32B | ≤ 7B |
| | **If acceptance rate is OK </br>smaller draft is better** |

- **API usage**: The local server supports this too; set the draft model in the server UI, or add a `draft_model` field in your request.
> Why speed is **sometimes very fast** and **sometimes only moderate**:
> 1. The smaller/faster the draft model is **relative** to the main model, the better.
> 2. The draft’s **acceptance rate** for the current prompt needs to be high. Smaller draft + higher acceptance → bigger speedup.
> 3. **Prompt-dependent**: factual/structured tasks (e.g., formulas/code) are easier for the main model to accept in long spans; open-ended creative writing branches a lot, causing more rejections and smaller gains.
> 4. **Resource trade-off**: running two models increases VRAM/RAM and compute; if the draft is too large or acceptance is low, it can even be slower.
