# FAQ 常见问题
关于一系列常见问题以及一个简单的文档前瞻目录（省流版）
## 简体中文  | [ENGLISH](FAQ_EN.md)

 <details>
 <summary>  
  
 ## 模型
 关于模型的一系列问答
</summary>

### 1. 最好的翻译模型？ </br>
**没有最好的**翻译模型，只有最适合你的翻译模型：
1. 模型训练**语料**
 - 模型是否使用**你的语言**/**源语料**经过训练？</br>
   德语法语西班牙语等等等等
   - 训练语料是否均匀？大部分模型对于**英文**支持最好（英文数据最多），别的语言质量则取决于训练数据数量与质量/训练方式与技术

-------

### 2. 模型是否使用***高质量语料**/ **特定语料**？
- **特定语料**一般存在于已微调模型，例如根据视觉小说（vn）；新闻；网络文章；学术文献；代码等微调</br>
        根据其微调语料微调语料的**特定类别**和**语种**，模型会大幅增强相关方面能力，但同时削弱其他方面能力；
  - 例如（微调）语料聚焦于视觉小说，则其新闻/学术翻译方面能力会减弱；</br>
    社区微调模型（例如尾缀带-JP）一般是用日语数据进行微调，会显著加强EN-JP能力，但针对性微调通常会削弱其他所有语言的能力
    - 因其训练语料在不同语言上的不均衡及模型容量/分词问题; 基底模型多语言语料越少，模型越小，这种现象越明显

--------

### 3. 模型规模
- 模型规模×数据×算力越大，通常效果越好 (scaling law)
  - 例如Qwen3-4B<Qwen3-8B<Qwen3-14B<Qwen3-32B
  - [**LLM显存使用表**](OtherModels_gguf.md)

-------

### 4. 模型名称解释
例如 **Qwen3-8B-Thinking-2507-abliterated-Q8_0-gguf** </br>
（模型并不存在，仅为举例）</br>

  - **Qwen3**: 基底模型系列名称
    
  - **8B**：模型参数大小，常见为4B±；8B±；14B±；30B±；70B±；100B+
    - **MoE**架构模型（例如30B-A3B) 30B为总参数，A3B仅为活跃参数
    - 不同参数对应显存使用量请看下文 **量化与GPU显存对照举例**
      
  - **Thinking**: 模型为或具有thinking mode（思维模型），并非所有思维模型都会标注
  
  - **2507**：时间版本号（2025/07），通常为小版本更新
  
  - **abliterated**: 去安全审核的一种方式，通常意味着此微调模型已去审核
    - 常见还有 uncensored; NFSW; amoral（不一定为尾缀）等
   
  - **Q8_0 (gguf)**: llama.cpp的量化方式， 具体请查看链接或下文
    - [**LLM显存使用表**](OtherModels_gguf.md)
      -  **量化与GPU显存对照举例**
      - **GGUF量化类型与相对质量**
 
     

</details>

---------

<details>
<summary>  

 ## 本地&在线API
 本地大模型好还是在线api好？
</summary>

### 1. 在线api是什么
在线api本质就是服务器提供商使用其服务器运行模型，并通过端口，网络流式传输到你的电脑。</br>
本质仍是本地模型在GPU服务器上运行,只是需要通过网络为用户提供服务

### 2. 本地vs在线
[如何选择LLM？在线 VS 本地](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/blob/main/README.md#%E5%A6%82%E4%BD%95%E9%80%89%E6%8B%A9llm%E5%9C%A8%E7%BA%BF-vs-%E6%9C%AC%E5%9C%B0)


</details>

---------

<details>
<summary>  
  
 ## 部署
 如何部署本地模型模型；常见部署平台
</summary>

1. 常见[**本地部署平台**](https://github.com/CYBIRD-D/How-to-Choose-your-LLM-Model-for-translation/tree/main#%E9%83%A8%E7%BD%B2%E6%9C%AC%E5%9C%B0%E6%A8%A1%E5%9E%8B)有：
- [**LM Studio**](https://lmstudio.ai/docs/app/basics)
  - 可以直接在[huggingface](https://huggingface.co/models)搜索模型，复制模型名字再在LM studio下载

- [**Ollama**](https://docs.ollama.com/quickstart)
  - 需要对命令行/代码的基本理解</br>

-------

2. 常见**在线部署平台**
- 免费？请查看[**Free LLM API**](Freellmapi.md)

- **付费**中间平台
  -  [Huggingface](https://huggingface.co/docs/inference-endpoints/index)
  -  [OpenRouter](https://openrouter.ai/docs/quickstart)



</details>
