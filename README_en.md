# How to Choose Your LLM?
**How to choose the right large language model (for translation)**  </br>

This guide is for beginners who want to use LLMs for translation.

If it helps, please consider giving the repo a star. Thanks.

### English | [中文-Simplified Chinese](README.md)
This article gives beginners a first overview of using large language models (LLMs) for translation.</br>
The main example is translating visual novels (VN), but the same ideas work for most other translation tasks.

Recommended tools and resources:
- [**LunaTranslator**](https://github.com/HIllya51/LunaTranslator)
- [PDFMathTranslate](https://github.com/PDFMathTranslate/PDFMathTranslate-next)
- [AiNiee](https://github.com/NEKOparapa/AiNiee)
- [**Free LLM API Provider**](https://github.com/CYBIRD-D/FREE-LLM-API-Provider)

--------

### [FAQ-Frequent Ask Questions](FAQ_EN.md) & Fast guide

These are Questions related to 
- Basic Concept
- Models & Performance
- Local VS Online
- Deployment & [**GPU Specification**](Nvidia_GPU_Specification.md)

which is a fast **guide** on how to read this article.
</br>

------

## What are LLMs good at?
Compared with traditional Neural Machine Translation (NMT — classic seq2seq / Transformer models trained only for translation),    
LLMs are not better at everything. </br>

But LLMs are clearly stronger in several important areas, especially: </br>
**Context handling**, **Controlling proper nouns / glossary**, and **Cross-lingual ability**:

- **Context Handling**</br>
 LLMs usually have **long context windows**. With suitable prompts, they can:
    - Keep the story or conversation coherent
    - Resolve pronouns and omitted parts (“he / she / that person / there”)
    - Maintain consistent terminology and style over long texts

- **Controlling proper nouns/glossary/GPT-DICTIONARY** (Proper Noun Translation) </br>
 LLMs are good at following user instructions, such as:

    - Terminology rules
    - Tone and style
    - Pronouns (he / she / they)
    - Custom dictionary explanations

 For VN translation (or any task where context matters), LLMs often **feel better overall** than traditional NMT.

    They can understand your prompts/instructions (depending on the model) and adjust translation accordingly.
    
    Traditional NMT usually cannot handle pronouns correctly even with a dictionary, because it does not truly “understand” context.
    
  - LLMs can read explanations like:</br>
    `James: A man's name`

  and treat that as context, so later they are more likely to use **“he”** instead of **“she”**.

    You can also control style via prompt (formal, casual, cute, etc.), depending on the model’s ability.

- **Cross-lingual ability**</br>
  Because modern LLMs are pretrained on large multilingual datasets, newer models usually:

  - Support more languages easier
  - Transfer knowledge across languages
  - Work across different domains (everyday language, games, documents, etc.)


## How to choose an LLM? Online vs Local
What you choose depends on your needs and trade-offs across the following factors. Here’s a quick guide:</br>

- Only Want to use local models but unsure about the Vram: </br>
[**LLM VRAM USAGE LISTS**](OtherModels_gguf.md) 

LLMs can be:
- **Local models**
- **Online models**
  - **Official APIs** (online)
  - **Third-party hosted APIs** (online)

---------

<details>
  <summary>Speed / Price / Performance  </br>
  "CUDA out of money, pls charge💸"</summary>   </br>

  
**Local (self-hosted)** means you run the LLM on your **own machine**.  
How large a model you can run mainly depends on:

- GPU memory bandwidth
- VRAM size
- Compute (CUDA cores, etc.)

Whether you use **local** or **online API**, there are cost considerations:

- **Local**: you "pay" for hardware (GPU, electricity, etc.).
- **Online**: you "pay per token" to API providers.  
  (Tokens ≈ pieces of text; more text → more tokens.)

In general:

> Bigger / newer models → better quality and/or speed → need more VRAM locally

Google offers a **free-tier API**. For example, Gemini 2.0 / 2.5 Flash often performs better than most small open models, but:

- Free-tier has quota limits (requests per minute/day, tokens per minute/day).
  - Larger models usually have tighter limits.
- newer models have more strict censorship.(explained in the next section)

If you do **NOT** have an 8GB+ GPU,  
- (6GB is often the bare minimum; on Mac no less than 16GB **unified memory** is recommended)
  - M series, not intel CPU
 
you can consider platforms like:

- [**Free LLM API Provider**](https://github.com/CYBIRD-D/FREE-LLM-API-Provider)

Some CN platforms also provide limited free tokens （check the article above).

With a **6GB+ VRAM GPU**, you may try local deployment. See:

- [**Nvidia GPU Specification**](Nvidia_GPU_Specification.md)
- [**LLM VRAM USAGE LISTS**](OtherModels_gguf.md)
- [**Deployment & GPU Specification**](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/FAQ_EN.md#deployment--gpu-specification)

Usually:

- Models smaller than **~4B parameters** struggle with high translation quality.
- Around **8B** is a good “sweet spot” between quality and resource usage.


 </details>

------------

 <details>
  <summary>Privacy / Moderation</summary>  

  - **Local models**  
      - Data stays on your machine (no external upload).  
      - Only moderation/censorship comes from the model itself; you can choose fine-tuned models with weaker or almost no moderation.
  
  -  **Google AI Studio / free-tier [API](https://github.com/CYBIRD-D/FREE-LLM-API-Provider)**:
      -  privacy isn’t a concern because there’s no private at all (lol).
          -  Google states free-tier data may be used for training; there’s no opt-out.
      
  -  **Paid APIs**: </br>
    True end-to-end encryption (E2EE) is not yet standard for LLM inference. TEE/Confidential Computing (CC-ON) depends on the cloud provider.
      -  Most providers offer:
          - Encryption in transit (HTTPS)
          - Encryption at rest
              - But plaintext is visible in memory on the server while the model runs.
    
      - Providers usually promise to:
          - Protect data
          - Delete it regularly
          - Offer opt-out from training
  
  - **Third-party hosted open-source models**:
      - You can choose fine-tuned variants that reduce or disable moderation.  
      - Platform-level logging and moderation depend on the host.

 </details>

------------


 <details>
  <summary>Multilingual / Cross-lingual ability</summary>  
   
 - Multilingual strength depends on:
    - The base model’s training data (which languages and domains)
    - Model size
    - Training techniques and fine-tuning

- Domain-/language-tuned models strengthen some areas compared with their base model.
    - Example: [SakuraLLM](https://github.com/SakuraLLM/SakuraLLM)
        - Continues pretraining and fine-tuning on general Japanese and light-novel / Galgame bilingual (ZH–JP) data.
        - Performance improves sharply in these domains (e.g. VN translation, EN↔JP).
            - But performance in other domains/languages is dramatically degraded, loses most of the base model (Qwen2.5) other capabilities.</br>
              Which only can be used for translation tasks in those specific areas.
</details>

-----------

<details> 
  <summary>Thinking models</summary>  
  
 - **Thinking** mode aims to strengthen:
    - Contextual understanding
    - Instruction following

In theory, this means better whole-document translation when long-range context is important (compared with non-thinking mode).
> Actual quality still largely depends on data and training.

- However, thinking mode （often **chain-of-thought**) requires extra tokens, </br> 
  This increases token usage and latency, so it is usually **not** ideal for real-time translation.

  
</details>

---------
</br>

### Online models (Closed-source models)

<details> 
  <summary>Price & Free API</br>
Different models have different prices</summary>  

Using a $10 usage budget on Gemini official API as a quick estimate:

| Feature       | 2.5 Pro | 2.5 Flash | 2.5 Flash-Lite |
| :----------- | :-----: | :-------: | :------------: |
| Input limit (or) | ~8M | ~33.3M | ~100M |
| Output limit | ~1M | ~4M | ~25M |
| Cost = input tokens * unit price + output tokens * unit price |

1. Thinking tokens not included here  
2. 100 tokens ≈ 75 English words  
3. Or assume a small chat-style call ≈ 1,000 input + 500 output tokens per call.</br>
2.5 Pro: ≈ 1,600 calls</br>
2.5 Flash: ≈ 6,450 calls</br>
2.5 Flash-Lite or 2.0 Flash: ≈ 33,000 calls</br>

> Google provides a [**free-tier API**](https://github.com/CYBIRD-D/FREE-LLM-API-Provider) (check details in the link).  
> But it’s limited by:
> - Requests per minute (RPM)
> - Tokens per minute (TPM)
> - Requests per day (RPD)  
> Daily quota resets at midnight Pacific Time.


Check the above link for rate limit details.

\* AI Studio vs API: AI Studio usage is “free forever,” but its UI quotas don’t always match the API docs exactly; Google adjusts them periodically (e.g., 2.5 Flash RPD observed dropping from 500 to 250).
</details>
  
<details> 
  <summary>Performance</br>  
New closed-source models outperform open models in many areas</summary> 

Check [**Timeline**](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/TIMELINE%201.jpg) here
  
Representatives (as of 2025/11):
  - xAI (Grok-4/4.1)
  - OpenAI (GPT-5/5.1 Thinking)
  - Google (Gemini 2.5 Pro/3 Pro)
  - Anthropic (Claude 4/4.1)</br>
  Within a family, larger models are stronger (Gemini 2.5 Pro > Flash > Lite).

See various benchmarks on [Kaggle](https://www.kaggle.com/benchmarks).
</details>

<details> 
  <summary>Moderation</br>    
Closed-source models generally implement stricter safety moderation (which is reasonable)</summary> 

**Rough moderation strictness (weaker → stronger):**</br>
Grok-3/4 (easier to bypass) ≤ Claude 3.7 ≤ Gemini 2.0 series < Gemini 2.5 series < OpenAI third-party APIs <<< OpenAI (newer the model, harder the bypass)
1. Gemini 2.5 free tier appears stricter.
2. Web/client Chat versions are stricter than APIs.
3. Third-party hosting tends to be less strict than official APIs.

</details>

<details>
  <summary>Multilingual / Cross-lingual ability</br>   
Leading closed-source models are typically strong across languages</summary> 

| Model | Verifiable count | Basis (scope) | Notes |
|---|---:|---|---|
| **xAI Grok-3** | **27** | Official language list (model) | Vendor-listed supported text languages. |
| **xAI Grok-4** | — | — | **Undisclosed**. |
| **OpenAI GPT-4** | **26** | Evaluation coverage (translated MMLU) | Eval includes 26 languages; eval ≠ upper bound. |
| **OpenAI GPT-4o** | **More than GPT-4** | Official statement |   |
| **OpenAI GPT-5** | — | — | **Undisclosed**. |
| **Google Gemini 2.5 Pro** | **37** / **40+** | Dev prompt languages / Web app UI | Two counts: dev list 37; Web UI “40+”. |
| **Anthropic Claude 3.7 / 4 / 4.1** | **15** / **11** | Official eval coverage / Product/UI languages | Eval: English + 14 non-English (15 total); UI languages: 11. |

<details> 
  <summary>Grok-3</summary> 
  
> English, Spanish, French, Afrikaans, Arabic, Bengali, Welsh, German, Greek, Indonesian, Icelandic, Italian, Japanese, Korean, Latvian, Marathi, Nepali, Punjabi, Polish, Russian, Swahili, Telugu, Thai, Turkish, Ukrainian, Urdu, Chinese </br>
  
</details>

<details> 
  <summary>GPT-4</summary> 
  
> English, Italian, Afrikaans, Spanish, German, French, Indonesian, Russian, Polish, Ukrainian, Greek, Latvian, Mandarin (Chinese), Arabic, Turkish, Japanese, Swahili, Welsh, Korean, Icelandic, Bengali, Urdu, Nepali, Thai, Punjabi, Marathi, Telugu </br>
</details>

<details> 
  <summary>Gemini</summary>  
> Arabic, Bengali, Bulgarian, Chinese (Simplified/Traditional), Croatian, Czech, Danish, Dutch, English, Estonian, Persian, Finnish, French, German, Greek, Gujarati, Hebrew, Hindi, Hungarian, Indonesian, Italian, Japanese, Kannada, Korean, Latvian, Lithuanian, Malayalam, Marathi, Norwegian, Polish, Portuguese, Romanian, Russian, Serbian, Slovak, Slovenian, Spanish, Swahili, Swedish, Tamil, Telugu, Thai, Turkish, Ukrainian, Urdu, Vietnamese
</details>

<details> 
  <summary>Claude</summary> 
  
> English (baseline), Spanish, Portuguese (Brazil), Italian, French, Indonesian, German, Arabic, Chinese (Simplified), Korean, Japanese, Hindi, Bengali, Swahili, Yoruba
</details>

</details>

-------
### Local models (Open-weight / Open-source)

<details> 
  <summary>What open-source & open-weight means</summary> 

  - Today, “open-source models” usually means **open-weight**.  </br>
  - **Open-weight**: the model weights are released; anyone can use/modify/fine-tune/commercialize them under a license (e.g., MIT). </br>
  - **Truly open-source**: training/inference code & pipeline, model architecture, weights, and data sources are published, sufficient for full reproduction.
</details>

- **Where to find models?** </br>
[Hugging Face](https://huggingface.co/)  
  - CN platforms include ModelScope (魔搭社区).

- **How to read model names?** </br>
Example: **Qwen3-8B-Thinking-2507-abliterated-Q8_0-gguf** </br>
(This model name is hypothetical for illustration.)</br>

  - **Qwen3**: base model family
    
  - **8B**: parameter count. Common sizes: 4B±; 8B±; 14B±; 30B±; 70B±; 100B+
    - **MoE** models (e.g., 30B-A3B): 30B is total params; A3B are the active params.
    - For VRAM vs params, see [**LLM VRAM USAGE LISTS**](OtherModels_gguf.md)
      
  - **Thinking**: indicates a thinking-mode model (not all such models are labeled).
  
  - **2507**: time tag (2025/07), often minor updates.
  
  - **abliterated**: a style of “**de-safety-filtered**” fine-tune; typically means moderation is reduced or removed.
    - You’ll also see ***uncensored*/*NSFW*/*amoral*/*evil***, etc.
   
  - **Q8_0 (gguf)**: a llama.cpp quantization type. See the link:
    - [**LLM VRAM USAGE LISTS**](OtherModels_gguf.md) 
      - **GGUF Quantization types & relative quality**

--------

<details> 
  <summary>Choosing an appropriate parameter size</summary> 
  
  - Typically, GPU VRAM > model file size + context memory usage.
      - Context can be stored in ram with slower token speed.
     
  - Larger model × more data × more compute → better results (scaling law).
    - For example: Qwen3-4B < Qwen3-8B < Qwen3-14B < Qwen3-32B
  
  - Common open-model size tiers: 4B±; 8B±; 14B±; 32B±; 70B±; 100B+
    - <4B models often means poor translation quality—you can still test on Hugging Face or LMArena if curious.
    - For MoE, consider the **total** parameter count.

> Note: A conservative VRAM estimate is “model file size + ~1GB headroom.” Longer context or placing KV cache on-GPU requires more VRAM.</br>
>
> If you exceed VRAM (spilling into system RAM), speed drops sharply (except on unified-memory systems).</br>
>
> In theory, larger models translate better; family-to-family comparisons are tricky.

</details>

<details> 
  <summary>Quantization & VRAM guide (examples)</summary> 
  
Using Qwen3 GGUF sizes with llama.cpp as examples.</br>
Here we only discuss GGUF models supported by llama.cpp (deployable via Ollama / LM Studio etc.). (MLX is similar.)</br>

#### Qwen3-8B (GGUF)

| Quantization | Model file size | Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 5.03 GB | ≥ 6 GB |
| Q5_0 | 5.72 GB | ≥ 7/8 GB |
| Q5_K_M | 5.85 GB | ≥ 7/8 GB |
| Q6_K | 6.73 GB | ≥ 8 GB |
| Q8_0 | 8.71 GB | ≥ 10 GB |

#### Qwen3-14B (GGUF)

| Quantization | Model file size | Recommended VRAM (weights + headroom) |
|---|---:|---:|
| Q4_K_M | 9.00 GB | ≥ 11/12 GB |
| Q5_0 | 10.3 GB | ≥ 12 GB |
| Q5_K_M | 10.5 GB | ≥ 12 GB |
| Q6_K | 12.1 GB | ≥ 14/16 GB |
| Q8_0 | 15.7 GB | ≥ 18/20 GB |

See more examples for other sizes | [**LLM VRAM USAGE LISTS**](OtherModels_gguf.md)    
\* *On Apple Mac (M1+), unified memory = RAM + VRAM. After subtracting 6–8GB for system/apps, the remainder approximates usable VRAM (many optimizations may need more memory).*</br>
\* *For MoE (e.g., Qwen3-30B-A3B): total params = 30B, all must load; A3B are just the active params.*</br>
</details>

<details> 
  <summary>GGUF quantization types & relative quality</summary> 

> Note: “Quality” here is an **experience-based** tiering of overall closeness to FP16 + common community metrics (e.g., perplexity/objective evals). The same quant level can vary by model/task. `_K` denotes newer K-quant; `_S/_M` are mixed strategies—`_M` is usually higher quality than `_S`.

| Quantization | Theoretical bpw* | Relative quality (vs FP16) | Typical use / advice | Notes |
|---|---:|---|---|---|
| **Q8_0** | ≈ 8.0 | Highest (near FP16) | When VRAM is plenty and you want FP16-like fidelity or rigorous evals | “Legacy” method but the highest-quality quant; negligible drop vs FP16 |
| **Q6_K** | 6.5625 | Very high (near Q8_0) | Aim for high quality while saving VRAM | K-Quant; better quality/size than same-bit legacy |
| **Q5_K_M** | 5.5 | High | A great 5-bit default; deployment “sweet spot” | `_M` prioritizes quality over `_S` |
| **Q5_0** | ≈ 5.0 | Medium–High | Consider only for old workflows | Legacy; usually worse than Q5_K_* |
| **Q4_K_M** | 4.5 | Medium (best among many 4-bit options) | Tight VRAM yet usable quality; common balance | Often the 4-bit go-to |
| **Q4_K_S** | ≈ 4.5 | Medium–Low (lower than `_M`) | When you need speed/smaller size in 4-bit | More aggressive mix, slight quality drop |
| **Q4_0** | ≈ 4.0 | Medium–Low | Compatibility/contrast only | Legacy; generally not recommended* |
| **Q3_K_M** | 3.4375 | Low | Extreme memory/edge devices | Noticeable degradation; not recommended |

Further reading: https://gist.github.com/Artefact2/b5f810600771265fc1e39442288e8ec9

\* *bpw (bits per weight) are approximate/official numbers; some legacy formats (Q4_0/Q5_0) have extra overhead not precisely specified—shown as “≈”.*</br>
\* *Special case: Gemma 3 12B Instruct QAT is q4_0, but quantization-aware training (QAT) makes its quality/speed far above typical q4.*</br> 
</details>

</details>

<details> 
  <summary>Which models are better to use?</summary> 

  - **In most cases, newer is better**: newer training techniques/more data → generally stronger multilingual ability.</br>
  - **Bigger is better (within your VRAM)**:
    - Different ***parameters*** at different ***quant*** levels?  
      For translation, **Q5_K_M** and above show little loss.</br>
      So, Qwen3-8B-Q8_0/FP16 < Qwen3-14B-Q5_K_M (for translation quality).
      - QAT (Quantization-Aware Training), e.g., Gemma 3 12B Instruct QAT q4, can outperform traditional q4 on both quality and speed.

    - For translation & instruction following you usually **don’t need Q8**; **Q6_K** and above are typically good enough in quality.
  
  - **Language fine-tunes**: English is usually best supported (most data). Other languages depend on data quantity/quality and training methods.</br>
    Community fine-tunes (suffix like -JP) use Japanese data to significantly strengthen EN↔JP, but targeted fine-tunes often weaken other languages.
    > Due to uneven multilingual corpora, tokenizer effects, and limited capacity, the fewer the multilingual data and the smaller the model, the more pronounced this trade-off.
    
  - **Unmoderated**: If your content trips safety filters, choose an unmoderated model, e.g.:
    - Qwen3-8B-abliterated
    - gemma-3-27b-it-abliterated
    - Llama-3-70b-Uncensored
    - Dhanishtha-nsfw
    - amoral-gemma3-12B </br>
    *Just for example, not really recommendation</br>
    (Suffixes like abliterated / uncensored / NSFW / amoral indicate de-moderation; others include “evil”, etc.)  
    Depending on technique, these may sacrifice some quality.

</details>

-----------
</br>
    
### [Optimize local model speed](Model_Speed.md) </br>
<details> 
  <summary>Quick notes here—see the link above for details</summary>   </br>
    
Using LM STUDIO as an example:
<p align="center">
  <img src="./LM%20STUDIO.png" width="800" alt="LM Studio screenshot">
</p>

1. **Context Length** </br>
Max tokens the model can “remember/process” per run (prompt + generated output). Larger windows handle longer texts but require much more RAM/VRAM and compute; exceeding the true max can cause odd outputs.
2. **GPU Offload** </br>
How many layers run on GPU (llama.cpp `n_gpu_layers` / `-ngl`; `-1` or >#layers ≈ full offload). More GPU layers boost throughput but are VRAM-limited; the rest runs on CPU.
3. **CPU Thread Pool Size** </br>
Number of CPU threads during inference (`n_threads`). More threads ≠ linear gains; near physical cores/system default is typical.
4. **Evaluation Batch Size (n_batch)** </br>
How many tokens are fed in parallel during prefill. Larger batch → higher throughput but more RAM/VRAM; semantics unaffected.
5. **RoPE Frequency Base** </br>
Controls rotary position encoding base frequency; sometimes increased for longer-context stability (model/impl dependent).
6. **RoPE Frequency Scale** </br>
Scaling factor for RoPE; used with the above for extending effective context.
7. **Offload KV Cache to GPU Memory** </br>
Put K/V cache and KQV ops on GPU to ease CPU/RAM pressure and speed up long contexts; availability varies.
8. **Keep Model in Memory** </br>
Avoid unloading weights between calls for snappier reuse; costs RAM.
9. **Try mmap()** </br>
Map weights from disk on demand; speeds loading and reduces resident memory. (llama.cpp uses mmap by default; can disable if needed.)
10. **Seed** </br>
Fix randomness for reproducibility.
11. **Flash Attention (experimental/optional)** </br>
A more efficient attention implementation that reduces memory traffic and speeds long-sequence inference; availability varies.
12. **K Cache Quantization Type (experimental)** </br>
Quantize the K cache to cut memory/VRAM with minimal loss; stability varies by backend/hardware.
13. **V Cache Quantization Type (experimental)** </br>
Same idea for the V cache; often paired with K quantization for long contexts on small GPUs.
14. **Speculative Decoding** | [**LM STUDIO intro**](https://lmstudio.ai/blog/lmstudio-v0.3.10) </br>
Use a small, fast “draft” model to propose tokens that the large “main” model quickly verifies; improves speed without changing the final distribution.
> In most cases, keeping RoPE/KV defaults is fine; some models are sensitive.

</details>   

---------

<details> 
  <summary>
   
   ### Translation tools?</br>
  
Make fan-patches or translation files</summary> 

  - [**LunaTranslator**](https://github.com/HIllya51/LunaTranslator) — an all-in-one translator for visual novels/galgames. Supports text hooking (HOOK/OCR/clipboard/ASR/file translation), multiple online/local engines, pre-translation & caching, Python extensions; plus TTS, Japanese tokenization & furigana, dictionaries (MDICT/online), Anki flashcards, Yomitan plugins, etc.

  - [**AiNiee**](https://github.com/NEKOparapa/AiNiee) — one-click AI long-text translator. Fits common game text workflows (MTool, Ren’Py, Translator++), and many formats (i18next, EPUB/TXT, SRT/VTT/LRC, Word/PDF/Markdown). Auto file & language detection, context consistency & glossary, AI polishing/layout/term extraction; configurable for online and local models.

  - [LinguaGacha](https://github.com/neavo/LinguaGacha) — “nearly zero-config” multi-language text translator. Supports subtitles/ebooks/game texts, compatible with many online/local models (Claude/ChatGPT/etc.), emphasizes speed and preservation of format/code style. Many WOLF/Ren’Py/RPGMaker/Kirikiri games can be “translate-and-play,” with CLI and guides.

  - [BallonsTranslator](https://github.com/dmMaze/BallonsTranslator) — DL-assisted translation & typesetting for comics/webtoons. One-click MT, WYSIWYG text editing (find/replace, batch styles), image editing & inpainting (masks/heal), OCR detection; Windows packaged build or Python source; compatible with many MT/LLM and offline models.

</details>    

-----------
### Deploying local models
Quantized-model deployment example (llama.cpp). </br>
Below are common, practical platforms:

**Possible platforms** 
- [**LM Studio**](https://lmstudio.ai/)  </br>
  - [**Guide**](https://lmstudio.ai/docs/app/basics)
  - All-in-one: local desktop app + OpenAI-compatible local server; easy setup (“install and go”). </br>
  - Built-in model discovery/download (Hugging Face); LAN sharing.</br>
  - Includes RAG, MCP integrations, and multiple GPU runtimes (CUDA/Metal/Vulkan/ROCm). </br>

- [**koboldcpp**](https://github.com/LostRuins/koboldcpp)  </br>
  - Focused on writing/RP/fan-fic workflows; ships KoboldAI Lite UI (memory, world facts, character cards, scenes, etc.), multiple modes (chat/adventure/instruct/storywriter).</br>
  - Beyond text, includes TTS/ASR and Stable Diffusion image generation; multiple compatible APIs (OpenAI/Ollama compatible).</br>
  - Provides OpenAI/Ollama/Kobold compatible endpoints.</br>

- [**Ollama**](https://ollama.com/) </br>
  - [**Guide**](https://docs.ollama.com/quickstart)
    - [**API Reference**](https://docs.ollama.com/api/introduction)
  - “Docker-for-models” local/LAN runtime and CLI/REST API. Supports Modelfile customization and model management.</br>
  - In 2025, official GUI (Win/mac) lowers the CLI barrier; offers unified cloud + local options.
    - [**Ollama cloud models**](https://github.com/CYBIRD-D/FREE-LLM-API-Provider?tab=readme-ov-file#ollama-)

**Model size / quantization spec choices**  </br>
See [**LLM VRAM USAGE LISTS**](OtherModels_gguf.md) 

**Which model should I pick?** </br>
See above: 
 - **“How to choose an LLM?”**
 - **“Open-weight/Open-source local models——Which models are better to use?”** </br>

--------
## [AI Timeline](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/TIMELINE%201.jpg)
