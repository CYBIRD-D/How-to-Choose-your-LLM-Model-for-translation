# How-to-Choose-your-LLM-Model-for-translation
This post helps beginners choose an LLM that suits their needs. 

### English | [中文-Simplified Chinese](README.md)
This article is intended to give beginners a preliminary understanding of using LLMs for translation, with visual novel (VN) translation as the primary scenario. Because the principles are similar, other translation tasks can also use it for reference.

Recommended: [LunaTranslator](https://github.com/HIllya51/LunaTranslator)


## What are the advantages of LLMs?
Compared with traditional Neural Machine Translation (NMT, usually sequence-to-sequence/Transformer systems trained specifically for translation), LLMs are not overwhelmingly better on every metric, but they do have clear advantages in several key aspects—especially context handling, glossary/constraints, and cross-lingual ability.

- **Stronger context handling**  
  LLMs’ long context windows and “context-aware prompting” help maintain discourse coherence, resolve anaphora/ellipsis, and keep terminology consistent.

- **Glossary/constraints**  
  LLMs can follow instruction-style constraints (terminology/register/tone/pronouns). For VN translation, the experience is generally much better than with traditional NMT.

- **Cross-lingual ability**  
  Because of pretraining (strong cross-lingual transfer and multi-domain generalization), newer models more easily support many languages.


## How to choose an LLM?
Your choice depends on the following trade-offs. A brief overview is below; detailed categories follow.

- **Speed/Price/quality**
  - “Cuda out of money, pls charge💸 ”
  - Whether local models or online APIs, there are cost trade-offs. Local models require a GPU; online APIs charge per use. Costs correlate with parameter size.</br>
Bigger models/faster speeds = better quality = more VRAM + more CUDA cores = higher API prices.

  - Google does provide free APIs, and Gemini 2.0 Flash is generally stronger than ~70% of small open-source models, but with quota limits. Bigger models = stricter limits.</br>
    - If you don’t have a GPU with ≥8 GB VRAM (absolute minimum 6 GB) (Mac needs 16 GB unified memory), it’s recommended to choose Google AI Studio.
    - I haven't used the AMD AI Max+ 395 series. Not sure about its compatibility or performance. Its design is similar to the unified memory of Mac, but with a smaller bandwidth.
 
- **Privacy/Moderation**
  - **Local models**: generally no privacy-leak concerns because everything runs locally. The main issue is moderation (you can choose fine-tuned models to avoid it).

  - **google api free tier**: also no privacy concerns—because there’s no privacy (lol). Google clearly states free-tier data may be used for training, and there’s no opt-out.

  - **Paid APIs**: by nature, true E2EE isn’t currently feasible, and the closest alternative (TEE) is usually not offered to regular users.</br>
Most providers only do transport + storage encryption; plaintext is visible on the server. They promise to protect and regularly delete your data and usually offer an opt-out from training.</br>
Moderation exists. Generally, the newer the model, the stricter the moderation (more advanced safety). Official APIs are typically stricter than third-party hosting.

  - **Third-party hosted open-source models**: since you can choose the model, you can pick fine-tuned variants that avoid moderation (whether the host/platform itself moderates is uncertain).

- **Multilingual capability**
  - Multilingual ability depends on the base model’s training data/model size/techniques.</br>
Fine-tuned models strengthen specific domains compared to their base model.</br>
For example, [SakuraLLM](https://github.com/SakuraLLM/SakuraLLM) continues pretraining and fine-tunes on general Japanese corpora and Chinese–Japanese data for light novels/galgames; however, it degrades significantly in other domains/language families and loses most of the base model (Qwen2.5)’s other abilities, making it suitable only for translation tasks.

- **Thinking models / chain of thought**
  - Thinking models strengthen understanding of context and instructions; in theory they do better on whole-document translation than non-thinking mode.
  - But they take longer to think, and chains of thought consume tokens.
----------

### Closed-source models
- **Price**  
Different models have different prices.</br>
A quick estimate using Gemini with a USD 10 usage budget:

| Property                  | 2.5 Pro | 2.5 Flash | Flash-Lite |
| :------------------------ | :-----: | :-------: | :--------: |
| Input limit (OR)     | ~8M     | ~33.3M    | ~100M      |
| Output limit              | ~1M     | ~4M       | ~25M       |
| Cost = input tokens × unit price + output tokens × unit price |

1. Thinking tokens are not counted here.  
2. 100 tokens ≈ 75 English words.  
3. Or assume a small chat-style call ≈ 1,000 input tokens + 500 output tokens per call.</br>
2.5 Pro: about 1,600 calls</br>
2.5 Flash: about 6,450 calls</br>
2.5 Flash-Lite or 2.0 Flash: about 33,000 calls</br>


  -  **Free API**
> Google provides a **free tier (API)**,  
> but it is subject to rate limits such as Requests per Minute (RPM), Tokens per Minute (TPM), and Requests per Day (RPD).  
> Daily quotas reset at midnight Pacific Time (PT).  

| Model                | Official API Free Tier Quota (Baseline) | AI Studio Common / Hover Observed Quota |
|-----------------------|----------------------------------------|-----------------------------------------|
| Gemini 2.5 Pro        | 5 RPM / 250k TPM / 100 RPD             | Not consistently shown                  |
| Gemini 2.5 Flash      | 10 RPM / 250k TPM / 250 RPD            | Often 10 RPM / 500 RPD; reduced to 250 RPD in some cases since 2025-06 |
| Gemini 2.5 Flash-Lite | 15 RPM / 250k TPM / 1000 RPD           | Often 15 RPM / 500 RPD                  |
| Gemini 2.0 Flash      | 15 RPM / 1M TPM / 200 RPD              | Often 15 RPM / 1500 RPD                 |
| Gemini 2.0 Flash-Lite | 30 RPM / 1M TPM / 200 RPD              | Often 30 RPM / 1500 RPD                 |

\*AI Studio vs API: AI Studio usage is always free, but its interface limits do not always match the API documentation tables.  
Google may adjust these quotas periodically (e.g., Gemini 2.5 Flash RPD observed dropping from 500 to 250).


- **Capabilities**</br>
The latest closed-source models outperform open-source ones in many areas (as of 2025/08):
  - xAI (Grok 4)
  - OpenAI (GPT-5)
  - Google (Gemini 2.5 Pro)
  - Anthropic (Claude 4)</br>
  Within a series, more parameters generally mean stronger capability (Gemini 2.5 Pro > Flash > Lite).

benchmark can be checked on [Kaggle](https://www.kaggle.com/benchmarks)

- **Moderation**
Closed-source models generally have stricter safety moderation (which is reasonable).

Moderation strength from weaker to stronger:</br>
Grok 3/4 (easy to bypass) ≤ Claude 3.7 ≤ Gemini 2.0 series < Gemini 2.5 series < OpenAI third-party API <<< OpenAI (hard to bypass)</br>
1. Gemini 2.5 free tier appears stricter.  
2. Web/client “Chat” versions are usually stricter than APIs.

- **Multilingua ablility**

| Model | Verifiable count | Basis (scope) | Notes |
|---|---:|---|---|
| **xAI Grok-3** | **27** | Official list (model) | Vendor-provided language list. |
| **xAI Grok-4** | — | — | **Undisclosed** by vendor. |
| **OpenAI GPT-4** | **26** | Evaluation coverage (translated MMLU) | 26 languages evaluated; evaluation ≠ hard limit. |
| **OpenAI GPT-4o** | Better Than GPT-4 | Openai offical claim | |
| **OpenAI GPT-5** | — | — | **Undisclosed** by vendor. |
| **Google Gemini 2.5 Pro** | **37** / **40+** | Dev prompt languages / Web app UI | Two vendor baselines: developer list (37) and UI availability (40+). |
| **Anthropic Claude 3.7 / 4 / 4.1** | **15** / **11** | Evaluation coverage / Product/UI languages | Eval≠ hard limit: EN + 14 non-EN; UI languages: 11. |
> Grok3: English, Spanish, French, Afrikaans, Arabic, Bengali, Welsh, German, Greek, Indonesian, Icelandic, Italian, Japanese, Korean, Latvian, Marathi, Nepali, Punjabi, Polish, Russian, Swahili, Telugu, Thai, Turkish, Ukrainian, Urdu, Chinese. </br>

> GPT4: English, Italian, Afrikaans, Spanish, German, French, Indonesian, Russian, Polish, Ukrainian, Greek, Latvian, Mandarin, Arabic, Turkish, Japanese, Swahili, Welsh, Korean, Icelandic, Bengali, Urdu, Nepali, Thai, Punjabi, Marathi, Telugu.</br>

> Gemini： Arabic, Bengali, Bulgarian, Chinese (Simplified/Traditional), Croatian, Czech, Danish, Dutch, English, Estonian, Persian, Finnish, French, German, Greek, Gujarati, Hebrew, Hindi, Hungarian, Indonesian, Italian, Japanese, Kannada, Korean, Latvian, Lithuanian, Malayalam, Marathi, Norwegian, Polish, Portuguese, Romanian, Russian, Serbian, Slovak, Slovenian, Spanish, Swahili, Swedish, Tamil, Telugu, Thai, Turkish, Ukrainian, Urdu, Vietnamese.

> Claude：English, Spanish, Portuguese (Brazil), Italian, French, Indonesian, German, Arabic, Chinese (Simplified), Korean, Japanese, Hindi, Bengali, Swahili, Yoruba.
-----------

### Local open-weights / open-source models
- **Where to find open-source models?**  
[Hugging Face](https://huggingface.co/)

- **How to choose a suitable parameter size**
  - GPU VRAM > Model file size + context (or offload to CPU)  
  - The larger the product of model size × data × compute, the better the performance tends to be (scaling law)
    - For example: Qwen3-4B < Qwen3-8B < Qwen3-14B < Qwen3-32B
  - Typical open-source model size tiers: 4B±; 8B±; 14B±; 32B±; 70B±; 100B+
    - Model less than 4B may have poor quality in tranlation; pls try by yourself see if works for you.
                                                                              
> Note: “Recommended VRAM” is a conservative estimate of “model file size + ~1 GB headroom”; longer context or putting the KV cache in VRAM requires more VRAM.</br>

> Overflowing VRAM (spilling into system RAM) can drastically reduce speed.</br>

> In theory, the more parameters a model has, the higher the translation quality; models from different series are hard to compare.

This section only discusses GGUF models supported by llama.cpp (can be deployed with ollama/LM Studio).</br>

**Example**: Qwen3 GGUF quantization sizes and recommended VRAM

#### Qwen3-8B (GGUF)

| Quantization | Model file size | Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 5.03 GB | ≥ 6 GB |
| Q5_0 | 5.72 GB | ≥ 8 GB |
| Q5_K_M | 5.85 GB | ≥ 8 GB |
| Q6_K | 6.73 GB | ≥ 8 GB |
| Q8_0 | 8.71 GB | ≥ 10 GB |

#### Qwen3-14B (GGUF)

| Quantization | Model file size | Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 9.00 GB | ≥ 12 GB |
| Q5_0 | 10.3 GB | ≥ 12 GB |
| Q5_K_M | 10.5 GB | ≥ 12 GB |
| Q6_K | 12.1 GB | ≥ 16 GB |
| Q8_0 | 15.7 GB | ≥ 20 GB |

\* *On Apple Mac (M1 and above), unified memory = RAM + VRAM. After subtracting the reserved 8 GB, the remainder can be roughly treated as usable “VRAM” (many optimizations require more memory).* </br>
\* *For MOE (Mixture of Experts) models (e.g., Qwen3-30B-A3B), the model size is 30B and must all be loaded into VRAM; A3B only denotes the active parameters.*</br>

- **GGUF quantization types and relative quality (llama.cpp)**

> Note: “Quality” is an **experience-based** tiering that reflects overall approximation to FP16 plus common community benchmarks (e.g., perplexity/objective evals). The same quantization can behave differently across models/tasks. `_K` denotes newer K-class quantization; `_S/_M` are different “mixture strategies,” with `_M` typically higher quality than `_S`.

| Quantization type | Theoretical bpw* | Relative quality (vs FP16) | Typical use / recommendation | Notes |
|---|---:|---|---|---|
| **Q8_0** | ≈ 8.0 | Highest (near FP16) | When VRAM is ample and you want to stay close to original precision or do rigorous evaluation | A “legacy” method, but the highest-quality quant tier; essentially no quality loss vs FP16 |
| **Q6_K** | 6.5625 | Very high (close to Q8_0) | Pursue high quality with lower VRAM | K-Quant; better quality/size efficiency than legacy at the same bit width |
| **Q5_K_M** | 5.5 | High | General 5-bit first choice; the “sweet spot” for deployment | `_M` prioritizes quality over `_S` |
| **Q5_0** | ≈ 5.0 | Medium–High | Consider only for legacy pipelines | Legacy method; usually worse than Q5_K_ |
| **Q4_K_M** | 4.5 | Medium (one of the best at 4-bit) | VRAM-tight but still need usable quality; common balance point | Community’s typical first choice within 4-bit |
| **Q4_K_S** | ≈ 4.5 | Medium-low (below `_M`) | 4-bit option when you want more speed/smaller size | `_S` is more aggressive; slightly lower quality |
| **Q4_0** | ≈ 4.0 | Medium–Low | Only for compatibility/comparison | Legacy method; generally no longer recommended* |
| **Q3_K_M** | 3.4375 | Low | Extreme memory or edge-device trade-offs | Noticeable quality drop; not recommended |

Technical article https://gist.github.com/Artefact2/b5f810600771265fc1e39442288e8ec9

\* *bpw (bits per weight) uses approximate or exact values from official/docs; some legacy methods (e.g., Q4_0/Q5_0) don’t clearly state extra overhead, hence “≈”.*</br>
\* *Special case: Gemma 3 12B Instruct QAT is q4_0, but Quantization-Aware Training (QAT) makes its quality far above a typical q4 tier.* 

- **Which models are better to use?**
  - **In most cases, the newer the better** (except llama 4). Newer models mean new training techniques/more data and are usually stronger for multilingual tasks.</br>
  - **Bigger parameter counts are better**: Within your **VRAM-supported range**, more parameters are better.
    - Comparison across parameter sizes and quantizations? For translation tasks only, **Q5_K_M** and above show no obvious quality loss, so **Qwen3-8B-Q8_0/FP16 < Qwen3-14B-Q5_K_M**.
    - For translation, **Q8** precision is generally unnecessary; **Q6_K** has no virtual quality loss.
  - **Language fine-tuning**: most models are best at English (most data). Quality in other languages depends on data quantity/quality and training methods/techniques.</br>
    Community fine-tunes (e.g., suffix “-JP”) use Japanese data, which significantly strengthens EN↔JP but usually weakens other languages.
  - **Uncensored**: if your content would be blocked by safety filters, you’ll need uncensored models.</br>
    For example: Josiefied-Qwen3-8B-abliterated-v1. Terms like abliterated; uncensored; NSFW usually indicate “safety-filter removed” fine-tunes (depending on techniques/skills, these models may degrade in quality).
-----------

#### Local model speed optimization

Using LM STUDIO as an example:
<p align="center">
  <img src="./LM%20STUDIO.png" width="800" alt="LM Studio screenshot">
</p>

1. **Context Length** </br>
Sets the maximum number of tokens the model can “remember/process” in one inference (includes the prompt and the model’s own output). Larger values allow longer texts but significantly increase (V)RAM and compute; exceeding the model/implementation’s max window may cause abnormal outputs.

2. **GPU Offload (layer offloading)** </br>
How many network layers/weights to execute on GPU (llama.cpp: `n_gpu_layers`/`-ngl`; setting `-1` or much larger than layer count usually means “offload as much as possible”). More GPU layers boost throughput but are limited by VRAM; the rest runs on CPU.

3. **CPU Thread Pool Size** </br>
Controls CPU threads during inference (llama.cpp: `n_threads`). More threads don’t scale linearly; values near physical cores or system suggestions are fine. Many wrappers default to half to all CPU cores.

4. **Evaluation Batch Size (n_batch)** </br>
Tokens fed in parallel during the prefill stage. Bigger batches usually increase throughput but use more (V)RAM; semantics/results don’t change—only speed and resource usage.

5. **RoPE Frequency Base** </br>
Adjusts the base frequency of Rotary Positional Embeddings (RoPE). Affects how position is encoded; increasing it is sometimes used to keep stability at longer contexts (limits depend on model/implementation).

6. **RoPE Frequency Scale** </br>
Scaling factor for RoPE; changes the granularity of positional encoding. Often paired with the previous setting to extend effective context or run long-context experiments.

7. **Offload KV Cache to GPU Memory** </br>
Moves attention K/V caches and related ops to GPU/VRAM to reduce CPU/RAM pressure and speed up long-context runs; availability depends on backend/hardware.

8. **Keep Model in Memory** </br>
Keeps the loaded model resident in system memory to speed up subsequent use; costs more RAM.

9. **Try mmap()** </br>
Memory-maps weights from disk on demand, typically speeding load and reducing resident memory; when the model exceeds available RAM, page thrashing may slow things down. LM Studio exposes this switch; llama.cpp uses mmap by default (can be disabled).

10. **Seed (random seed)** </br>
Controls sampling randomness for reproducible results; a fixed value yields consistent outputs given the same prompt and parameters.

11. **Flash Attention (experimental/optional)** </br>
A more efficient attention implementation that reduces memory I/O via computation reordering/blocking, lowering memory and accelerating long sequences; llama.cpp/some backends provide `--flash-attn`. Availability varies by model/hardware.

12. **K Cache Quantization Type (experimental)** </br>
Selects the precision/quantization format of the attention K-cache (implementation field `type_k`/ggml type). Quantizing KV caches can notably reduce memory/VRAM with tiny accuracy loss or speed gains in some scenarios; formats/stability vary.

13. **V Cache Quantization Type (experimental)** </br>
Same as above but for the V-cache (`type_v`). Paired with K-cache quantization for long context or low-VRAM cards to expand context/trim usage.
> In general, RoPE and the KV cache can stay at defaults; some models are prone to errors.
-----------

- **Translation tools** </br>
You can create game patches or translation files yourself.
  - [LunaTranslator](https://github.com/HIllya51/LunaTranslator) — An all-in-one translator for visual novels/galgames. Supports text capture (HOOK/OCR/clipboard/ASR/file translation), multiple online/local translation engines, pretranslation and caching, Python extensions; plus TTS, Japanese tokenization and furigana, dictionary lookup (MDICT/online), Anki flashcards, loading Yomitan and other plugins.

  - [AiNiee](https://github.com/NEKOparapa/AiNiee) — One-click AI long-text translation tool. Fits common game-text workflows (MTool, Ren’Py, Translator++, etc.) and many formats (i18next, EPUB/TXT, SRT/VTT/LRC, Word/PDF/Markdown); supports auto file/language detection, context consistency and glossaries, AI polishing/typesetting/term extraction, configurable online and local model backends.

  - [LinguaGacha](https://github.com/neavo/LinguaGacha) — “Out-of-the-box, almost zero-config” multilingual text translator. Supports subtitles/e-books/game text, compatible with many online/local models (e.g., Claude / ChatGPT), emphasizes high speed and preservation of formatting/code style; most WOLF/Ren’Py/RPGMaker/Kirikiri games can be translated and played instantly, with CLI mode and usage guides.

  - [BallonsTranslator](https://github.com/dmMaze/BallonsTranslator) — Deep-learning-assisted translation/typesetting tool for comics/webcomics. Supports one-click machine translation, WYSIWYG text editing (find/replace, batch styles), image editing/inpainting (masking/repair brush), OCR text detection; available as a Windows package or Python source, compatible with various MT/LLM and offline models.

