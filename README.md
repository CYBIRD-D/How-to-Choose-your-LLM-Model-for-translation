# How-to-Choose-your-LLM-Model-for-translation
**如何选择适合你的大语言模型 （用于翻译）**  
This is a post for beginners to choose the LLM Models suit themselves. 

### 简体中文  | [English](README_en.md)
此文为了帮助初学者对于LLM model翻译有一个初步的了解，主要场景为翻译visual novel（vn）。当然因为原理相同别的翻译任务也可参考。

在此推荐[LunaTranslator](https://github.com/HIllya51/LunaTranslator)


## LLM的优势？
LLM（大语言模型）相较传统神经机器翻译NMT（通常指专门为翻译训练的序列到序列/Transformer 系统）并非在所有指标上全面碾压，但在若干关键方面具有明显优势，尤其是上下文，术语表与跨语言能力等
- **更强的上下文能力** LLM 的长上下文窗口与“上下文感知提示”，有助于保持篇章连贯、指代/省略消解、术语一致

- **术语表** LLM 能理解指令化约束（术语/语域/语气/代词），在vn翻译上体验会远高于传统神经机器翻译

- **跨语言能力** 因为LLM的特性（LLM 预训练的跨语言迁移与多域泛化能力强），较新的模型更容易支持多语言

## 如何选择LLM？
如何选择模型取决于你对于以下因素的需求和取舍，这里做一个简单的介绍，后文有细致分类：
- **速度/价格/性能**
  - "Cuda out of money, pls charge💸 "
  - 无论是本地模型还是在线api，都有价格取舍的问题。本地模型需要显卡，在线api需要按量付费，这些价格取决于模型参数大小</br>
更大的模型/更快的速度=更好的效果=更多的显存+更多的cuda core=更贵的api价格

  - 谷歌确实在aistudio提供免费的api，且gemini 2.0flash已通常强于70%开源小模型，但有额度限制 更大的模型=更多的限制</br>
    - 如果没有8G及以上显卡（最低条件6G）（Mac为16G统一内存），建议选择google aistudio
    - 笔者没有使用过AMD AI Max+ 395系列，不确定其兼容性或性能，其设计类似Mac统一内存，但带宽更小

  - 目前（2025/08）最大的非商业服务器单体设备应为
    - M3 ULTRA （最大512G统一内存）
    - 单卡显存
      - RTX PRO 6000（Blackwell） 96G
      - H200 141GB 
 
- **隐私/审查**
  -  **本地模型**：一般不用担心隐私泄露，都是在本地跑，唯一的问题是审查（可选择微调模型避免）。

  -  **google aistudio（free）** 也不用担心隐私泄露，因为没有隐私（笑）。谷歌明确free tier的数据会用于模型训练，没有关闭的选项。
  -  **付费api**：因为其性质暂时无法做到E2EE端到端加密，相对接近的TEE一般也不对普通用户提供。</br>
绝大多数服务商只做传输加密与存储加密，服务端可见明文。承诺保护你的数据并定时删除，且有关闭数据用于训练的选项。</br>
审查存在.一般越新的模型越严格（安全审查更先进）,官方api一般比第三方托管严格
  - **第三方托管开源模型**：因为可选模型缘故，用户可选择已经过微调的模型来避免模型审查（托管方/平台是否有审查 笔者不能确定）

- **多语言能力**
  - 多语言能力取决于基础模型训练的语料/模型大小/技术能力</br>
特定的微调模型相比其基础模型会在特定领域进一步加强</br>
例如[SakuraLLM](https://github.com/SakuraLLM/SakuraLLM) 针对通用日文语料与轻小说/Galgame等领域的中日语料上进行继续预训练与微调，但在其他领域和语系能力会显著下降，且失去基础模型（Qwen2.5）其余的大部分能力，仅能用于翻译任务

- **思维模型/思维链**
  - thinking模型因理解上下文和用户指令能力进一步加强，理论上对于整篇的翻译会优于non-thinking mode
  - 但思考时间长，且思维链也需要消耗token 
---------

### 闭源模型
- **价格**  
不同模型的价格不同</br>
以gemini 10USD使用量为例做一个快速的估算：

| 特性         | 2.5 Pro | 2.5 Flash | Flash-Lite |
| :----------- | :-----: | :-------: | :--------: |
| 输入上限(或） | ~8M     | ~33.3M     |~100M      |
| 输出上限     | ~1M     |     ~4M    | ~25M       |
| 成本= 输入token* 单价+输出token*单价                |
1. 这里没有计算thinking token
2. 100token≈75 words(English)
3. 或者假设小型聊天式调用≈每次 1,000 个输入 token + 500 个输出 token.</br>
2.5 Pro：约 1,600 次调用</br>
  2.5 Flash：约 6,450 次调用</br>
  2.5 Flash-Lite 或 2.0 Flash：约 33,000 次调用</br>
  
- **性能**</br>
新闭源模型能力多方面优于开源模型，代表为（截至2025/08）
  - xai（grok 4）
  - Openai （GPT-5)
  - Google (Gemini 2.5pro)
  - Anthropic (Claude 4)</br>
  同系列模型之间参数越大，能力越强 （gemini2.5 pro>flash>lite)

多项测评（benchmark）可在[Kaggle](https://www.kaggle.com/benchmarks)查看

- **审查**  
闭源模型普遍存在较严格的安全审查机制（也很合理）

审查机制由弱到强为</br>
grok3/4(容易绕过）≤ claude 3.7 ≤ gemini 2.0 series < gemini 2.5 series < openai第三方api <<< openai(难以绕过）
1. Gemini 2.5 free tier审查疑似更严重
2. 各模型网页/客户端Chat版本审核强于api

- **跨语言/多语言能力**  
领先的闭源模型通常有强大的跨语言能力

| 模型 | 可核实数量 | 依据（范围） | 备注 |
|---|---:|---|---|
| **xAI Grok-3** | **27** | 官方清单（模型） | 厂商列出的文本语言列表。 |
| **xAI Grok-4** | — | — | **未披露**（无官方数据）。 |
| **OpenAI GPT-4** | **26** | 评测覆盖（翻译版 MMLU） | 评测含 26 种语言；评测≠能力上限。 |
| **OpenAI GPT-4o** | **超过GPT-4** | 官方宣称 |   |
| **OpenAI GPT-5** | — | — | **未披露**（无官方数据）。 |
| **Google Gemini 2.5 Pro** | **37** / **40+** | 开发者提示语言 / Web 应用 UI | 两套口径：开发者清单 37；Web 应用 UI 为 40+。 |
| **Anthropic Claude 3.7 / 4 / 4.1** | **15** / **11** | 官方评测覆盖 / 产品/UI 语言 | 评测：英语+14 种非英语（共 15）；UI 语言：11。 |
> Grok3: English（英语）、Spanish（西班牙语）、French（法语）、Afrikaans（南非荷兰语）、Arabic（阿拉伯语）、Bengali（孟加拉语）、Welsh（威尔士语）、German（德语）、Greek（希腊语）、Indonesian（印尼语）、Icelandic（冰岛语）、Italian（意大利语）、Japanese（日语）、Korean（韩语）、Latvian（拉脱维亚语）、Marathi（马拉地语）、Nepali（尼泊尔语）、Punjabi（旁遮普语）、Polish（波兰语）、Russian（俄语）、Swahili（斯瓦希里语）、Telugu（泰卢固语）、Thai（泰语）、Turkish（土耳其语）、Ukrainian（乌克兰语）、Urdu（乌尔都语）、Chinese（中文） </br>

> GPT-4：English（英语）、Italian（意大利语）、Afrikaans（南非荷兰语）、Spanish（西班牙语）、German（德语）、French（法语）、Indonesian（印尼语）、Russian（俄语）、Polish（波兰语）、Ukrainian（乌克兰语）、Greek（希腊语）、Latvian（拉脱维亚语）、Mandarin（中文）、Arabic（阿拉伯语）、Turkish（土耳其语）、Japanese（日语）、Swahili（斯瓦希里语）、Welsh（威尔士语）、Korean（韩语）、Icelandic（冰岛语）、Bengali（孟加拉语）、Urdu（乌尔都语）、Nepali（尼泊尔语）、Thai（泰语）、Punjabi（旁遮普语）、Marathi（马拉地语）、Telugu（泰卢固语） </br>

> Gemini: 阿拉伯语、孟加拉语、保加利亚语、中文（简体/繁体）、克罗地亚语、捷克语、丹麦语、荷兰语、英语、爱沙尼亚语、波斯语、芬兰语、法语、德语、希腊语、古吉拉特语、希伯来语、印地语、匈牙利语、印尼语、意大利语、日语、卡纳达语、韩语、拉脱维亚语、立陶宛语、马拉雅拉姆语、马拉地语、挪威语、波兰语、葡萄牙语、罗马尼亚语、俄语、塞尔维亚语、斯洛伐克语、斯洛文尼亚语、西班牙语、斯瓦希里语、瑞典语、泰米尔语、泰卢固语、泰语、土耳其语、乌克兰语、乌尔都语、越南语

> Claude: English（英语，基线）、Spanish（西班牙语）、Portuguese（Brazil）（巴西葡萄牙语）、Italian（意大利语）、French（法语）、Indonesian（印尼语）、German（德语）、Arabic（阿拉伯语）、Chinese（Simplified）（简体中文）、Korean（韩语）、Japanese（日语）、Hindi（印地语）、Bengali（孟加拉语）、Swahili（斯瓦希里语）、Yoruba（约鲁巴语）

-------
### 本地开放权重/开源模型
- **哪里寻找开源模型？**
[Huggingface](https://huggingface.co/)

- **如何选择适合的模型参数大小**
  - 通常GPU显存 > 模型文件大小 + 上下文占用
  - 模型规模×数据×算力越大，通常效果越好(scaling law)
    - 例如Qwen3-4B<Qwen3-8B<Qwen3-14B<Qwen3-32B
  - 通常开源模型规模分布：4B±；8B±；14B±；32B±；70B±；100B+
    - 小于4B的模型往往翻译质量不佳，可在Huggingface自行寻找测试 
> 说明：推荐显存为“模型文件大小 + 1k余量”的保守估算；更长上下文或将 KV cache 放入显存时需要更多 VRAM。</br>

> 爆显存（即超过显存大小导致占用内存）会大幅降低速度（统一内存架构除外） </br>

> 理论上模型参数越大，翻译质量越高；不同系列难以对比

这里仅讨论支持llama.cpp的GGUF模型（可由ollama/LM studio等平台布置）（MLX类似）</br>
例子： 以Qwen3 GGUF 量化尺寸与推荐显存为例（llama.cpp）

#### Qwen3-8B（GGUF）

| 量化 | 模型文件大小 | 推荐显存（仅权重+余量） |
|---|---:|---:|
| Q4_K_M | 5.03 GB | ≥ 6 GB |
| Q5_0 | 5.72 GB | ≥ 8 GB |
| Q5_K_M | 5.85 GB | ≥ 8 GB |
| Q6_K | 6.73 GB | ≥ 8 GB |
| Q8_0 | 8.71 GB | ≥ 10 GB |

#### Qwen3-14B（GGUF）

| 量化 | 模型文件大小 | 推荐显存（仅权重+余量） |
|---|---:|---:|
| Q4_K_M | 9.00 GB | ≥ 12 GB |
| Q5_0 | 10.3 GB | ≥ 12 GB |
| Q5_K_M | 10.5 GB | ≥ 12 GB |
| Q6_K | 12.1 GB | ≥ 16 GB |
| Q8_0 | 15.7 GB | ≥ 20 GB |

\* *Apple Mac(M1版本及以上）统一内存为RAM+VRAM，扣除8G剩余可近似看为显存（多数优化方式需更多内存）。*</br>
\* *MOE（混合专家）（例如Qwen3-30b-A3b）其大小为30b, 需全部装入显存，A3b只为活跃参数</br>

- **GGUF 量化类型与相对质量（llama.cpp）**

> 注：质量为**相对 FP16 的总体逼近**与社区常用基准（如困惑度/客观评测）综合判断的**经验级**分档；同一量化在不同模型/任务上可能有差异。`_K` 为更先进的 K 类量化；`_S/_M` 为不同“混合策略”，一般 `_M` 质量高于 `_S`。

| 量化类型 | 理论 bpw* | 相对质量（对比 FP16） | 典型使用场景 / 建议 | 备注 |
|---|---:|---|---|---|
| **Q8_0** | ≈ 8.0 | 最高（接近 FP16） | VRAM 充足、要尽量贴近原精度或做严谨评测 | 属于“旧法（legacy）”，但质量最高的量化档，相较FP16基本没有质量下降 |
| **Q6_K** | 6.5625 | 很高（接近 Q8_0） | 追求高质量且希望显存更省 | K-Quant，质量/体积效率优于同位数的旧法 |
| **Q5_K_M** | 5.5 | 较高 | 5-bit 档的通用首选；综合部署的“甜点位” | `_M` 较 `_S` 更注重质量 |
| **Q5_0** | ≈ 5.0 | 中等—较高 | 仅在兼容旧工作流时考虑 | 旧法（legacy），质量通常逊于 Q5_K_ |
| **Q4_K_M** | 4.5 | 中等（4-bit 中质量最佳之一） | 显存较紧张但仍需可用质量；常见平衡点 | 社区普遍认为 4-bit内首选|
| **Q4_K_S** | ≈ 4.5 | 中等偏下（低于 `_M`） | 更追求速度/更小体积时的 4-bit 选项 | `_S` 为更激进混合，质量略降 |
| **Q4_0** | ≈ 4.0 | 中等—较低 | 仅做兼容/对比用途 | 旧法（legacy），质量较低，通常不再推荐* |
| **Q3_K_M** | 3.4375 | 较低 | 极限内存或边缘设备权衡 | 质量明显劣化，不推荐 |

具体技术文章 https://gist.github.com/Artefact2/b5f810600771265fc1e39442288e8ec9

\* *bpw（bits per weight）为官方/文档给出的近似或精确数值；部分旧法（如 Q4_0/Q5_0）不明确给出额外开销，表中以“≈”表示。*</br>
\* *特殊情况：Gemma 3 12B Instruct QAT 虽为q4_0量化，但量化感知训练（Quantization-Aware Training, QAT）使其质量和速度远超q4档位 

- **哪些模型更适合使用？**
  - **大多数情况下，越新越好**： （除了llama4）新模型意味着新训练技术/更多语料，在多语言方面通常更强。</br>
  - **模型参数越大越好**： 在你的**显存可支持范围内**，参数越大越好
    - 不同参数不同量化之间对比？仅针对翻译任务而言，**Q5_K_M**及以上级别量化不会有明显质量损失，所以 Qwen3-8B-Q8_0/FP16 < Qwen3-14B-Q5_K_M
    - 针对翻译和指令遵循一般无需**Q8**精度，**Q6_K**及以上基本无质量损失。
  
  - **语言微调**：大部分模型对于英文支持最好（英文数据最多），别的语言质量则取决于训练数据数量与质量/训练方式与技术。</br>
    社区微调模型（例如尾缀带-JP）一般是用日语数据进行微调，会显著加强EN-JP能力，但通常会削弱其他所有语言的能力
  - **无审查**：如果你需要翻译的内容会被模型安全审核，则需要找无审查模型。</br>
    例如：Josiefied-Qwen3-8B-abliterated-v1，其中abliterated;uncensored;NSFW等都代表去安全审核微调（取决于技术和能力，这些模型可能会有质量下降）。
-----------
    
#### 优化本地模型速度

这里以LM STUDIO为例
<p align="center">
  <img src="./LM%20STUDIO.png" width="800" alt="LM Studio 截图">
</p>

1. **Context Length（上下文长度）** </br>
设定一次推理中模型可“记住/处理”的最大 token 数（包含提示词与模型生成的回复本身）。数值越大，能处理的长文本越多，但显著增加显存/内存与计算开销，超过模型训练或实现允许的最大窗口还可能导致输出异常。
2. **GPU Offload（GPU 分层卸载）** </br>
指定将多少层网络权重与计算卸载到 GPU 上执行（llama.cpp 对应 n_gpu_layers/-ngl；设为 -1 或远大于层数通常意味着尽量全卸载）。更多层在 GPU 上可显著提升吞吐，但受显存限制；不足部分仍会在 CPU 上跑
3. **CPU Thread Pool Size（CPU 线程池大小）** </br>
控制推理时使用的 CPU 线程数（llama.cpp 参数 n_threads）。线程数越高不一定线性提速，通常接近物理核数或系统建议值即可；很多封装默认取系统 CPU 数的一半到全部。
4. **Evaluation Batch Size（评估批大小 / n_batch）** </br>
预填充阶段一次并行送入模型的 token 数。批越大，通常吞吐更高但占用内存/显存也更大；结果与语义不会因批大小改变，只影响速度与资源占用。
5. **RoPE Frequency Base（RoPE 频率基数）** </br>
调整旋转位置编码（RoPE）的基频。该进阶参数影响模型如何编码位置信息；适当调大常用于尝试在更长上下文下保持稳定性（具体极限取决于模型/实现）。
6. **RoPE Frequency Scale（RoPE 频率缩放）** </br>
RoPE 的缩放因子；改变位置编码的“粒度”，常与上项配合，用于扩展有效上下文或做长上下文实验。
7. **Offload KV Cache to GPU Memory（将 KV 缓存卸载到 GPU）** </br>
把注意力的 K/V 缓存及相关 KQV 运算放到 GPU/显存中，可降低 CPU/RAM 压力并提升上下文的速度；是否可用取决于后端与硬件。
8. **Keep Model in Memory（将模型常驻内存）** </br>
使已加载的模型不被自动移出系统内存，换取更快的再次调用与交互体验；代价是占用更多 RAM。
9. **Try mmap()（尝试内存映射）** </br>
通过内存映射从磁盘“按需”映射权重，通常能加快加载并减少常驻内存占用；但当模型大于可用 RAM 时可能产生频繁页换而降速。LM Studio 提供该开关；llama.cpp 默认使用 mmap，可按需要禁用。
10. **Seed（随机种子）** </br>
控制采样中的随机性以便复现实验结果；设定固定值可让同一提示在同参数下产生一致输出。
11. **Flash Attention（实验性/可选）** </br>
一种对注意力计算的高效实现，通过重排计算与分块把大量显存读写转化为片上缓存操作，从而显著降低内存占用并加速长序列推理；llama.cpp/部分后端提供 --flash-attn 开关，具体可用性取决于模型与硬件。
12. **K Cache Quantization Type（K 缓存量化类型，实验性）** </br>
选择注意力中 K（Key）缓存的存储精度/量化格式（对应实现里的 type_k/ggml 类型）。量化 KV 缓存可明显降低内存/显存占用以换取极小精度损失或在部分场景带来速度收益；可用格式与稳定性依实现与硬件而异。
13. **V Cache Quantization Type（V 缓存量化类型，实验性）** </br>
同上，但作用于 V（Value）缓存（实现字段 type_v）。与 K 缓存配合量化常用于长上下文或小显存卡以扩大可用窗口/降低占用。
> 一般情况下RoPE；kv cache可保持默认状态，部分模型容易出错。
---------

- **翻译工具？** </br>
可自制游戏补丁或翻译文件
  - [LunaTranslator](https://github.com/HIllya51/LunaTranslator) —— 面向视觉小说/galgame 的一体化翻译器。支持文本抓取（HOOK/OCR/剪贴板/语音识别/文件翻译）、多种在线/本地翻译引擎、预翻译与缓存、Python 扩展；并提供 TTS 合成、日语分词与假名注音、词典查词（MDICT/在线）、Anki 生词卡、加载 Yomitan 等插件。

  - [AiNiee](https://github.com/NEKOparapa/AiNiee) —— 一键式 AI 长文本翻译工具。适配常见游戏文本工作流（MTool、Ren’Py、Translator++ 等）与多格式（i18next、EPUB/TXT、SRT/VTT/LRC、Word/PDF/Markdown）；支持自动识别文件与语种、上下文一致性与术语表、AI 润色/排版/术语提取，在线与本地模型接口可配置。

  - [LinguaGacha](https://github.com/neavo/LinguaGacha) —— “开箱即用、几乎零配置”的多语言文本翻译器。支持字幕/电子书/游戏文本等类型，兼容多家在线或本地模型（如 Claude / ChatGPT 等），强调高速度与格式/代码样式保留；多数 WOLF/Ren’Py/RPGMaker/Kirikiri 游戏可即翻即玩，并提供命令行模式与使用教程。

  - [BallonsTranslator](https://github.com/dmMaze/BallonsTranslator) —— 面向漫画/条漫的深度学习辅助翻译与排版工具。支持一键机翻、所见即所得的文本编辑（查找替换、批量样式）、图像编辑与修复（掩膜/修复画笔）、OCR 文本检测；可用 Windows 打包版或 Python 源码运行，兼容多种机翻/LLM 与离线模型。

    
