# Local LLM Models Recommodation
This is only a small list of recommodation for llm models under 14B which are used for translation.</br>
Depends on your languages/taste/usage/content, the results & performances **may or may not** meet your expectation.</br>

Most models below are finetune of Qwen, Gemma, Mistral series.

Explaination can be found here:
- [**FAQ-Frequent Ask Questions**](FAQ_EN.md)
  - [Models & Performance](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/FAQ_EN.md#models--performance)

## Must Read
Unless you had the knowledge.
- [LLM VRAM USAGE LISTS](OtherModels_gguf.md)
  - [**GGUF quantization types & relative quality**](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/OtherModels_gguf.md#gguf-quantization-types--relative-quality)

- [**Deploy local models**](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/README_en.md#deploying-local-models)

### Highly Recommend to Read
- [**How to choose an LLM? Online vs Local**](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/OtherModels_gguf.md#gguf-quantization-types--relative-quality)
  - [Local models](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/README_en.md#local-models-open-weight--open-source)
- [**FAQ-Frequent Ask Questions**](FAQ_EN.md)


## Recommend models
Before check the list, you need to understand some basic knowledge.
- **How to read model names?** </br>
Example: **Qwen3-8B-Thinking-2507-abliterated-Q8_0-gguf** </br>
(This model name is hypothetical for illustration.)</br>

  - **Qwen3**: base model family
  - **8B**: parameter count. Common sizes: 4B±; 8B±; 14B±; 30B±; 70B±; 100B+
    - For VRAM & params, see [**LLM VRAM USAGE LISTS**](OtherModels_gguf.md)
      
  - **Thinking**: indicates a thinking-mode model (not all thinking models are labeled).
  
  - **2507**: time tag (2025/07), often minor updates.
  
  - **abliterated**: a style of “**de-safety-filtered**” fine-tune; typically means moderation is reduced or removed.
    - You’ll also see ***uncensored*/*NSFW*/*amoral*/*evil***, etc.
   
  - **Q8_0 (gguf)**: a llama.cpp quantization type. See the link:
    - [**LLM VRAM USAGE LISTS**](OtherModels_gguf.md) 
      - **GGUF Quantization types & relative quality**

-------
> Note: </br>
> 1. Quantizations since **Q5_K** and above usually no noticing quality loss.</br>
> 2. **Larger model size** × data × compute usually means better performance (the scaling law).
>     - For example: Qwen3-4B < Qwen3-8B < Qwen3-14B < Qwen3-32B
> 3. Translation quality also depends on the **quality & amount of training data** on certain languages. 

**Only download GGUF file** unless you're not using llama.cpp (that includes LM Studio, Ollama, Kobold)

### 0~3B (Vram≤4GB)
LLMs at this scale usually have poor performance.</br>
All links are from Hugging Face.</br>
All models are choosen based on community reports, downloads and likes.

| Model Name | Languages | Base model family | Link(GGUF) | Link(Original) |
|---|---:|---:|---:|---:|
| tencent/HY-MT1.5-1.8B                             | General | HY-MT1.5 | [GGUF](https://huggingface.co/mradermacher/HY-MT1.5-1.8B-GGUF) | [Original](https://huggingface.co/tencent/HY-MT1.5-1.8B) |
| Unbabel/Tower-Plus-2B                             | General | Gemma2 | [GGUF](https://huggingface.co/DZgas/Tower-Plus-2B-GGUF) | [Original](https://huggingface.co/Unbabel/Tower-Plus-2B) |
| prithivMLmods/Qwen3-VL-2B-Instruct-abliterated-v1 | **EN**⇌XX | Qwen3 | [GGUF](https://huggingface.co/mradermacher/Qwen3-VL-2B-Instruct-abliterated-GGUF) | [Original](https://huggingface.co/prithivMLmods/Qwen3-VL-2B-Instruct-abliterated-v1) |
| Goekdeniz-Guelmez/Josiefied-Qwen3-1.7B-abliterated-v1  | General | Qwen3 | [GGUF](mradermacher/Josiefied-Qwen3-1.7B-abliterated-v1-GGUF) | [Original](https://huggingface.co/Goekdeniz-Guelmez/Josiefied-Qwen3-1.7B-abliterated-v1) |



### 4B (Vram≈4GB/6GB)

| Model Name | Languages | Base model family | Link(GGUF) | Link(Original) |
|---|---:|---:|---:|---:|
| sarvamai/sarvam-translate  （note:4B） | **22 official Indian languages** | Gemma3 | [GGUF](https://huggingface.co/mradermacher/sarvam-translate-GGUF) | [Original](https://huggingface.co/sarvamai/sarvam-translate) |  
| INSAIT-Institute/MamayLM-Gemma-3-4B-IT-v1.0 | **Ukrainian⇌EN** | Gemma3 | [GGUF](https://huggingface.co/mradermacher/MamayLM-Gemma-3-4B-IT-v1.0-GGUF) | [Original](https://huggingface.co/INSAIT-Institute/MamayLM-Gemma-3-4B-IT-v1.0) | 
| mlabonne/gemma-3-4b-it-abliterated-v2       | General | Gemma3 | [GGUF](https://huggingface.co/mradermacher/gemma-3-4b-it-abliterated-v2-GGUF) | [Original](https://huggingface.co/mlabonne/gemma-3-4b-it-abliterated-v2) | 
| Goekdeniz-Guelmez/Josiefied-Qwen3-4B-Instruct-2507-gabliterated-v2 | General | Qwen3 | [GGUF](https://huggingface.co/mradermacher/Josiefied-Qwen3-4B-Instruct-2507-gabliterated-v2-GGUF) | [Original](https://huggingface.co/Goekdeniz-Guelmez/Josiefied-Qwen3-4B-Instruct-2507-gabliterated-v2) | 
| RefalMachine/RuadaptQwen3-4B-Instruct | **RU⇌EN** | Qwen3 | [GGUF](https://huggingface.co/RefalMachine/RuadaptQwen3-4B-Instruct-GGUF) | [Original](https://huggingface.co/RefalMachine/RuadaptQwen3-4B-Instruct) | 
| DavidAU/Qwen3-4B-2507-Thinking-heretic-abliterated-uncensored (!long thinking) | General | Qwen3 | [GGUF](https://huggingface.co/mradermacher/Qwen3-4B-2507-Thinking-heretic-abliterated-uncensored-GGUF) | [Original](https://huggingface.co/DavidAU/Qwen3-4B-2507-Thinking-heretic-abliterated-uncensored) | 




  
