# FAQ Frequent Ask Questions
Regarding a series of common questions and a simple forward of contents for the document

## ENGLISH | [简体中文](FAQ.md)

<details>
 <summary>  
  
 ## Concept
Basic concept of Proper Noun。
</summary>

- **NMT**: Neural Machine Translation
  - like google translation


- **(Generative) LLMs**: Large Language Models
  - Today's new AI, chatbot are usally based on this
  - Like GPT-5; Gemini 3; Grok 4; Claude 4, etc.



- **API**: Application Programming Interface
  -  A connection between computers or between computer programs. It is a type of software interface, offering a service to other pieces of software.
  -  For llms, it is a port provide service through a server which runs the model (could be your server and hardware if it is local llms) and send to your interface

- [**What are LLMs good at?**](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/README_en.md#what-are-llms-good-at)


</details>

------------

<details>
<summary>  
  
 ## Models
 A series of Q&As about models
</summary>

### 1. The “best” translation model? </br>
There is **no single “best”** translation model—only the one that’s most suitable for you:
1. Training **corpus**
 - Was the model trained on **your language**/**your source domain**?</br>
   German, French, Spanish, etc., and so on
   - Is the training corpus balanced? Most models support **English** best (because there’s the most English data). Quality for other languages depends on the amount and quality of training data / training methods and techniques.

-------

### 2. Has the model used ***high-quality corpora** / **domain-specific corpora**?
- **Domain-specific corpora** are typically present in fine-tuned models—for example, fine-tuned on visual novels (VN); news; web articles; academic literature; code, etc.</br>
        Depending on the **specific categories** and **language(s)** of the fine-tuning data, the model will substantially improve in those areas while weakening in others;
  - For example, if the (fine-tuning) corpus focuses on visual novels, its ability in news/academic translation may be reduced;</br>
    Community fine-tuned models (e.g., with a -JP suffix) are generally fine-tuned on Japanese data, which significantly strengthens EN↔JP ability, but targeted fine-tuning often weakens abilities in all other languages.
    - Due to data imbalance across languages and issues like model capacity/tokenization; the fewer multilingual corpora in the base model and the smaller the model, the more pronounced this effect is.

--------

### 3. Model size
- Larger model size × data × compute usually yields better performance (the scaling law).
  - For example: Qwen3-4B < Qwen3-8B < Qwen3-14B < Qwen3-32B
  - [**LLM VRAM Usage Table**](OtherModels_gguf.md)

-------

### 4. How to read a model name
For example: **Qwen3-8B-Thinking-2507-abliterated-Q8_0-gguf** </br>
(This model does not exist; it’s just an example.)</br>

  - **Qwen3**: Name of the base model series
    
  - **8B**: Parameter count; common sizes include ~4B; ~8B; ~14B; ~30B; ~70B; 100B+
    - For **MoE** architectures (e.g., 30B-A3B) 30B is total parameters; A3B are the active parameters.
    - For VRAM needs at different parameter counts, see **Quantization vs GPU VRAM examples** below.
      
  - **Thinking**: Indicates the model is or has a “thinking mode”; not all thinking-style models explicitly mark this.
  
  - **2507**: Version timestamp (2025/07), usually a minor update.
  
  - **abliterated**: A way to remove safety moderation; typically means this fine-tuned model has moderation disabled.
    - Other common terms include “uncensored”, “NSFW”, “amoral” (not necessarily as suffixes), etc.
   
  - **Q8_0 (gguf)**: A llama.cpp quantization format; see the link or section below.
    - [**LLM VRAM Usage Table**](OtherModels_gguf.md)
      -  **Quantization & GPU VRAM examples**
    - **GGUF quantization types and relative quality**
 
     

</details>

---------

<details>
<summary>  

 ## Local & Online APIs
 Which is better: local large models or hosted online APIs?
</summary>

### 1. What is an online API?
Essentially, an online API means a service provider runs the model on their servers and streams results to your machine via ports and the network.</br>
In essence, it’s still a locally running model—just running on a GPU server and served to users over the network.

### 2. Local vs. Online
[How to choose an LLM? Online VS Local](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/README_en.md#how-to-choose-an-llm-online-vs-local)


</details>

---------

<details>
<summary>  
  
 ## Deployment
 How to deploy local models; common deployment platforms
</summary>

### 1. Common [**local deployment platforms**](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/README_en.md#deploying-local-models) include:
- [**LM Studio Guide**](https://lmstudio.ai/docs/app/basics)
  - You can search for models directly on [huggingface](https://huggingface.co/models), copy the model name, and then download it in LM Studio.

- [**Ollama Guide**](https://docs.ollama.com/quickstart)
  - Requires a basic understanding of the command line/code.</br>

-------

### 2. Common **online deployment platforms**
- Free? Please see [**Free LLM API**](Freellmapi.md)

- **Paid** intermediary platforms
  -  [Hugging Face](https://huggingface.co/docs/inference-endpoints/index)
  -  [OpenRouter](https://openrouter.ai/docs/quickstart)



</details>
